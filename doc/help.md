# Trinity Beta V0.2版本试用指引

## 试用指引索引
0. Trinity 源码包获取
1. Trinity 运行环境准备工作
2. Trinity 网关节点部署
3. Trinity 钱包节点部署
4. TestNet TNC水龙头
5. Trinity 网络浏览器
6. Channel交互


## Trinity 源码包获取

克隆Trinity源码:

```
    git clone https://github.com/trinity-project/trinity.git [User-Path]
      * User-Path： 用户指定的目录
```


## Trinity 运行环境准备工作

* `Ubuntu 1604桌面版或服务器版`

```
    安装系统库

        sudo apt-get install screen libleveldb-dev libssl-dev g++

    安装mongodb

        sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
        echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list

        sudo apt-get install mongodb-org
```

* `Python3.6 运行环境`

```
    安装python3.6

        添加python3.6安装包

            sudo apt-get install software-properties-common
            sudo add-apt-repository ppa:jonathonf/python-3.6

            sudo apt-get update

        安装python3.6

            sudo apt-get install python3.6 python3.6-dev

    安装pip3.6

        wget https://bootstrap.pypa.io/get-pip.py
        python3.6 get-pip.py

    安装virtualenv

        pip3.6 install virtualenv

    安装Trinity运行所依赖的python库：

        进入trinity源码所在的目录，通过pip3.6安装lib库

            pip3.6 install -r requirements
```

* `启动系统服务`

```
    启动mongodb数据库服务

        sudo service mongod start
```

* `系统环境变量设置`

```
    在某些特定系统中，需要设置PYTHONPATH。（若运行Trinity服务过程中，出现找不到文件的问题，可以尝试本节内容）
    进入Trinity源码所在目录，执行以下命令，或者将下述命令添加到.bashrc 文件中

    export PYTHONPATH=$PWD
```


## Trinity 网关节点部署

配置
打开trinity/gateway/config.py文件，配置 cg_public_ip_port字段值的ip地址部分为自己节点的公网ip地址，端口号不变。

进入trinity/gateway目录，执行如下命令启动trinity 网络节点：

```
python3.6 start.py -->null &
```
## Trinity CLI 钱包部署

打开trinity/wallet/config.py文件，通过修改Configure属性的Fee字段的值来设置该钱包节点的路由手续费，当前默认收取0.01TNC的手续费。

进入trinity/wallet目录，执行如下命令启动trinity CLI钱包：

```
python3.6 prompt.py
```

等待trinity CLI钱包进行区块同步，区块同步完成之后再继续进行后续操作。

注意：
1、钱包需要持续保持打开状态。
2、钱包区块同步完成之后再进行channel相关操作。

## TestNet TNC水龙头
TNC水龙头是基于NEO TestNet的，以便大家在NEO TestNet上进行Trinity试用，每个地址每次可获得10个TNC。

水龙头地址：

http://106.15.91.150

## Trinity 网络浏览器
Trinity网络浏览器可以实时查看trinity网络节点的详细信息及状态。

浏览器地址：

http://106.15.91.150:8033


## Channel节点交互

trinity CLI钱包区块同步完成之后，即可在钱包控制台进行钱包及通道的相关操作了。

钱包控制台输入help查看所有trinity CLI钱包命令。

这里仅介绍几个和通道相关的命令：

1. 使用状态通道前，需要先使用create wallet 命令创建一个地址。

2. 使用channel open命令进行channel功能的使能，只有使能channel功能之后才能进行状态通道相关的其他操作。

3. 使用channel create命令进行状态通道的创建操作。

4. 使用channel tx命令进行状态通道的链下交易操作。

5. 使用channel close命令进行状态通道的结算删除工作。
