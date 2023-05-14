**Ansible简介：**



**Ansible安装：**



**Ansible配置文件：**



**Ansible的inventory文件：**

  inventory文件在ansible中是比较重要的，一般我们会在这里定义主机，主机组等。默认的ansible配置文件是`/etc/ansible/hosts`。如果有主机清单文件在其他地方，则可以通过配置文件中`inventory = /xxx/hosts`选项来修改如下：

```shell
[root@ansible ansible]# grep  inventory ansible.cfg
inventory      = inventories/hosts
```

  如果只是临时使用一个inventory文件，则不需要修改这个配置文件，可以使用`-i`参数来临时定义，如下：

```shell
ansible -i /path/hosts
ansible-playbook -i  /path/hosts
```

  inventory文件可以采用ini配置格式，当然如果你的ansible版本大于2.4，则可以使用yaml格式。下面就让我们来看看具体的hosts文件中的内容。

```shell
[root@ansible ~]# cat hosts.yml
test01
192.168.1.1
192.168.1.2 ansible_port=8000
test02 ansible_host=192.168.1.3
192.168.1.4:8888
192.168.1.[5:7] ansible_port=9999
```

  从上面的第一行中**test01**，是ansible第一个主机，ansible连接时会通过DNS解析此主机名，寻找ip地址进行ssh连接。

  第二行**192.168.1.1**，ansible连接时直接使用ip地址，不会做DNS解析。

  第三行**192.168.1.2 ansible_port=8000**，ansible连接时会将默认的ssh端口改为8000。

  第四行**test02 ansible_host=192.168.1.3**，ansible连接时不会做DNS解析，直接使用**ansible_host**变量中的主机ip地址连接。

  第五行**192.168.1.4:8888**，ansible连接时会将默认ssh端口改为8888。

  第六行**192.168.1.[5:7] ansible_port=9999**，ansible会将此行解析为如下，并一一链接。

```shell
192.168.1.5 ansible_port=9999
192.168.1.6 ansible_port=9999
192.168.1.7 ansible_port=9999
```

  从上面可以，ansible支持填充缩写，如下：

```shell
a[1:3] # a1,a2,a3
a[a:c] # aa,ab,ac
[0-5] # 0,1,2,3,4,5
```

前面用到的**ansible_port**，这些是主机变量，它可以直接定义在hosts文件中的主机列表后面，这些变量是ansible在连接时会使用的变量，常用的变量如下：

| inventory变量                | 含义                                                         |
| ---------------------------- | ------------------------------------------------------------ |
| ansible_host                 | ansible 连接节点时的 IP 地址                                 |
| ansible_port                 | 连接对方的端口号，ssh 连接时默认为 22                        |
| ansible_user                 | 连接对方主机时使用的主机名。不指定时，将使用执行 ansible 或 ansible-playbook 命令的用户 |
| ansible_password             | 连接时的用户密码                                             |
| ansible_connection           | 连接类型，有效值包括 smart、ssh、paramiko、local、docker、winrm，默认为 smart。smart 表示智能选择 ssh 和 paramiko，当 SSH 支持 ControlPersist (即持久连接) 时使用 ssh，否则使用 paramiko。local 和 docker 是非基于 ssh 连接的方式，winrm 是连接 windows 的插件 |
| ansible_ssh_private_key_file | 指定密钥认证 ssh 连接时的私钥文件                            |
| ansible_ssh_common_args      | 提供给 ssh、sftp、scp 命令的额外参数                         |
| ansible_become               | 允许进行权限提升                                             |
| ansible_become_method        | 指定提升权限的方式，例如可使用 sudo/su/runas 等方式          |
| ansible_become_user          | 提升为哪个用户的权限，默认提升为 root                        |
| ansible_become_password      | 提升为指定用户权限时的密码                                   |

**inventory中的普通变量：**

 **inventory**配置文件除了使用ansible内部默认的变量，还可以自定义变量，在执行ansible任务的时候调用它，如下：

```shell
cat /etc/ansible/hosts # 在hosts文件中写入变量如下：
192.168.2.70 node_var="test"

ansible 192.168.2.70 -m debug -a 'var=node_var' # 使用ad-hoc查看变量，打印如下：
192.168.2.70 | SUCCESS => {
    "node_var": "test"
}
```

**inventory主机分组：**

  上面hosts文件中每一行都是一个主机虽然很简单，但是却不利于管理，好在ansible可以使用主机分组来定义。每个主机组可以定义多个主机，一个主机也可以加入多个主机组，这样在操作时可以直接操作一个主机组，例子如下：

```shell
cat hosts # 打印如下：
[nginx]
192.168.2.6[7:8]
192.168.2.69 host_var="I am 69"

[sql]
192.168.2.70 ansible_password='www.itgroup.com'

[nginx:vars]
host_var="test"

[lnmp:children]
nginx
sql
```

  从上面打印输出来看，我们定义了三个主机组，分别是nginx、sql、lnmp。其中nginx主机组包含了192.168.2.67-69三个主机，sql包含了一个主机，lnmp主机组比较特殊，它包含了nginx主机组和sql主机组，由此可以看出主机组可以嵌套，只要使用children关键字即可。上面的nginx主机组定义了一个全组变量，使用vars关键字，它定义了host_var变量。

  验证nginx主机组变量：

```shell
ansible nginx -m debug -a 'var=host_var' # 打印如下：

192.168.2.67 | SUCCESS => {
    "host_var": "test"
}
192.168.2.69 | SUCCESS => {
    "host_var": "I am 69"
}
192.168.2.68 | SUCCESS => {
    "host_var": "test"
}

```

  由此我们可以看出来，ansible在主机单独定义的变量会覆盖主机组的变量，而没有自定义变量的主机默认使用主机组定义的变量。

  测试lnmp嵌套主机组：

```shell
ansible lnmp -m ping # 使用ping模块测试连通性，打印如下：

192.168.2.68 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
192.168.2.69 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
192.168.2.70 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
192.168.2.67 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```













**Ansible简单使用—ad-hoc：**



**Ansible的灵魂—playbook：**

  前面我们介绍了ansible的ad-hoc内容，有些同学可能会觉得ad-hoc内容已经很方便了，只需要再熟悉模块的具体使用就能掌握ansible了。其实前面的ad-hoc使用只能算是ansible的开胃菜，因为ad-hoc大部分都是可以通过shell来实现，完全没有体现出ansible的自动化能力，所以现在请继续学习ansible的第一个“正餐”——playbook的使用。

  在学习playbook之前，有必要介绍一下什么是playbook。playbook直译为剧本，这个翻译其实没问题，因为ansible自动化工具就像是一个剧本，剧本里面的东西都是写好的，只需要演员(inventory)正常出演即可。

  playbook里面有两个重要的概念：

1. play
2. task

  **play**可以把他理解为一个剧本桥段，**task**可以把它理解为剧本中的每一个动作。而playbook将task组织起来，并将一些有关联的动作归纳为一个play(桥段)。各个paly又组成了一个完整的playbook(剧本)。总结起来如下：

- playbook中包含了一个或多个的paly
- play中包含了一个或多个的task，有两种特殊的task
  - pre_tasks：执行普通task任务之前执行的任务列表
  - post_tasks：普通task任务执行完之后执行的任务
- 每个play都需要指定一个hosts(演员)
- 每个play都可以设置改play的特有的行为，例如定义play级别的变量等。





**了解yaml语法：**

  ansible采用了playbook的语法，通常以`.yml`或者`.yaml`作为文件名后缀。

  yaml基本语法如下：

- 使用缩进表示层级关系，但是缩进不能使用Tab键；
- 缩进空格个数不重要，但同一级别下的元素缩进要一致；
- 通常在文件开头已`---`作为文档开始。(如果没有也不会有影响)
- `#`表示注释，从字符一直到行尾；
- 字符串不用加引号，但在可能产生歧义的时候需要加引号；
- 布尔值非常灵活，不区分大小写：true/false,yes/no,on/off,y/n,0/1均可

  yaml有三种数据结构：

1.  对象：key/value格式，也称为哈希结构，字典结构或关联数组
2. 数组：也称为列表
3. 标量：单个的值

**对象：**

  一组键值对表示，中间使用`:`隔开，注意冒号后必须至少一个空格

  例子如下：

```yaml
---
name: xiaoawng
age: 18
```

**数组：**

  数组也是列表，是ansible常用的格式，例子如下：

```yaml
---
# 一个水果清单
- apple
- banana
- strawberry
```

  也可以使用行内数组的写法：

  ```yaml
  ---
  - kernel1: Shell
  - kernel2: Per1
  - kernel3: Python
  - kernel4: Java
  ```

  还可以将对象和数组混合使用：

```yaml
---
languages:
  - Shell
  - Perl
  - Java
```

**字典：**

```yaml
---
person1:
  name: xiaowang
  age: 19
  school: UTS
  
person2:
  name: hong
  age: 20
  school: UVS
```

将对象、数组、字典混合使用：

```yaml
---
- persion1:
  name: xiaowang
  age: 18
  langs:
    - Java
    - Python
    
- person2:
  name: hong
  age: 20
  langs:
    - Shell
    - C
```

字符串格式：

```yaml
str: hello
  world
  hello world
```

  上面本质上是一行，转为json格式后如下：

```json
{
    "str": "hello world hello world"
}
```

还可以使用`>`和`|`换行，如下：

```yaml
that: >
  fool
  bar

this: |
  fool
  bar
```

只不过使用`|`时，会保留换行符，上面转为json格式如下：

```json
{
    'that': "fool bar",'this': "fool\nbar\n"
}
```

**playbook的写法：**

  了解YAML写法之后，就可以来写Playbook了。

  前面介绍了Playbook与play、task的关系，一个Playbook可以包含多个play，一个play可以包含多个task，而且每个play都要指定play的目标主机。现在再来看之前的playbook例子：

```yaml
- name: play1
  hosts: nginx
  gether_facts: true
  tasks:
    - name: task1 in play1
      debug:
        msg: "This is task1 in play1"

- name: play2
  hosts: sql
  gether_facts: true
  tasks:
    - name: task1 in play2
      debug:
        msg: "This is task1 in play2"
```

通过学习yaml语言后的格式可以清楚明白，再playbook中，每个play都需要放在数组中，所在playbook的顶层使用`- name:`或者直接`- hosts:`不使用name，来表示这是一个play。

  每个play都必须包含`hosts:`和`tasks:`指令。

  `hosts`指令用来指定要执行该play的目标主机，这个可以是主机名、主机组等。

  `tasks`指令用来确定这个play中包含的任务，可以是一个或者多个任务，所以tasks下的任务也要是一个数组，使用`- xx`表示每一个任务。

  `gather_facts`指令是一个特殊的指令，它是一个play级别的设置，主要是在执行play之前收集目标节点的信息，由setup模块提供，默认情况下，每个play默认都要执行。如果想节省时间，不收集目标节点信息则可以使用`gather_facts: false`来禁止收集任务。





**Ansible小试牛刀：**

  使用ansible来自动化配置主机免密：

```shell
cat hosts.yml # 打印如下

[nginx]
192.168.2.6[7:8]
192.168.2.70

cat playbook.yml # 查看playbook配置

---
- name: config key
  hosts: nginx
  gether_facts: false
  connection: local
  tasks:
    - name: 配置免密
      shell: |
        ssh-keyscan {{inventory_hostname}} >> ~/.ssh/known_hosts
        sshpass -p 'XXX' ssh-copy-id root@{{inventory_hostname}}
```

  上面的 ssh-keyscan命令是用来免输入yes，其实我们完全可以通过ssh或者更改ansible配置文件来修改，在ansible.cfg配置文件中将`host_key_checking=false`取消注释即可；







**Ansible的杀手锏—Role：**



