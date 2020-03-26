#### [轻量级RPC长连接脚手架](https://github.com/fdisk123/original/tree/snapshot2.11)
[![](https://camo.githubusercontent.com/f50b84e13fdbb61d847742c34259c58469c7d2b2/68747470733a2f2f7472617669732d63692e6f72672f70616765732d7468656d65732f6172636869746563742e7376673f6272616e63683d6d6173746572)](https://github.com/fdisk123/original/tree/snapshot2.11)  
```` 
基于netty 长连接 zookeeper/consul自发现HA 结构，序列化自由实现。
以动态代理为核心，支持注解、手工配置xml。

````
#### 导入在git里的maven仓库引用(引jar)

````
只需在pom加入私有库信息
	<repositories>
		<repository>
			<id>original-maven-repository</id>
			<!-- 直接把fdisk123/original/snapshot2.11换为你自己的GIT库路径即可-->
			<url>https://raw.github.com/fdisk123/original/snapshot2.11</url>
		</repository>
	</repositories>
	
	<!--引入依赖包-->
	<dependency>
		<groupId>com.cheuks.bin</groupId>
		<artifactId>original-rmi</artifactId>
		<version>0.0.1-SNAPSHOT</version>
	</dependency>
````

#### [Redis多机集群-5.0](https://github.com/fdisk123/original/tree/2.20/original-cache)
[![](https://camo.githubusercontent.com/f50b84e13fdbb61d847742c34259c58469c7d2b2/68747470733a2f2f7472617669732d63692e6f72672f70616765732d7468656d65732f6172636869746563742e7376673f6272616e63683d6d6173746572)](https://github.com/fdisk123/original/tree/2.20/original-cache)  
````
	2、Redis高可用集群搭建

l redis安装

下载地址：http://redis.io/download 安装步骤：

# 安装gcc yum install gcc

# 把下载好的redis-5.0.2.tar.gz放在/usr/local文件夹下，并解压

wget http://download.redis.io/releases/redis-5.0.2.tar.gz tar xzf redis-5.0.2.tar.gz

cd redis-5.0.2

# 进入到解压好的redis-5.0.2目录下，进行编译与安装 make & make install # 启动并指定配

置文件 src/redis-server redis.conf（注意要使用后台启动，所以修改redis.conf里的daemonize改为yes) # 验证启动是否成功 ps -ef | grep redis # 进入redis客户端 /usr/local/redis/bin/redis-cli # 退出客户端 quit # 退出redis服务： （1）pkill redis-server （2）kill 进程号 （3）src/redis-cli shutdown

l redis集群搭建

redis集群需要至少要三个master节点，我们这里搭建三个master节点，并且给每个master再搭建一个slave节点，总共6个redis节点，这里用三台机器部署6个redis实例，每台机器一主一从，搭建集群的步骤如下：

第一步：在第一台机器的/usr/local下创建文件夹redis-cluster，然后在其下面分别创建2个文件夾如下 （1）mkdir -p /usr/local/redis-cluster （2）mkdir 8001、 mkdir 8004 第一步：把之前的redis.conf配置文件copy到8001下，修改如下内容： （1）daemonize yes （2）port 8001（分别对每个机器的端口号进行设置） （3）dir /usr/local/redis-cluster/8001/（指定数据文件存放位置，必须要指定不同的目录位置，不然会丢失数据） （4）cluster-enabled yes（启动集群模式） （5）cluster-config-file nodes-8001.conf（集群节点信息文件，这里800x最好和port对应上） （6）cluster-node-timeout 5000

(7) # bind 127.0.0.1（去掉bind绑定访问ip信息）

(8) protected-mode no （关闭保护模式） （9）appendonly yes

如果要设置密码需要增加如下配置：

（10）requirepass zhuge (设置redis访问密码)

（11）masterauth zhuge (设置集群节点间访问密码，跟上面一致) 第三步：把修改后的配置文件，copy到8002，修改第2、3、5项里的端口号，可以用批量替换：

:%s/源字符串/目的字符串/g

第四步：另外两台机器也需要做上面几步操作，第二台机器用8002和8005，第三台机器用8003和8006

第五步：分别启动6个redis实例，然后检查是否启动成功 （1）/usr/local/redis-5.0.2/src/redis-server /usr/local/redis-cluster/800*/redis.conf （2）ps -ef | grep redis 查看是否启动成功

第六步：用redis-cli创建整个redis集群(redis5以前的版本集群是依靠ruby脚本redis-trib.rb实现) 
/usr/local/redis-5.0.2/src/redis-cli -a zhuge --cluster create --cluster-replicas 1 192.168.0.61:8001 192.168.0.62:8002 192.168.0.63:8003 192.168.0.61:8004 192.168.0.62:8005 192.168.0.63:8006 代表为每个创建的主服务器节点创建一个从服务器节点 
第七步：验证集群： 
（1）连接任意一个客户端即可：./redis-cli -c -h -p (-a访问服务端密码，-c表示集群模式，指定ip地址和端口号）
    如：/usr/local/redis-5.0.2/src/redis-cli -a zhuge -c -h 192.168.0.61 -p 800* 
（2）进行验证： cluster info（查看集群信息）、cluster nodes（查看节点列表） 
（3）进行数据操作验证 
（4）关闭集群则需要逐个进行关闭，使用命令： /usr/local/redis/bin/redis-cli -a zhuge -c -h 192.168.0.60 -p 800* shutdown
````

#### [Redis多机集群-3.0](https://github.com/fdisk123/original/tree/2.20/original-cache)
[![](https://camo.githubusercontent.com/f50b84e13fdbb61d847742c34259c58469c7d2b2/68747470733a2f2f7472617669732d63692e6f72672f70616765732d7468656d65732f6172636869746563742e7376673f6272616e63683d6d6173746572)](https://github.com/fdisk123/original/tree/2.20/original-cache)  
````
	部署档案记录。
	对应的java 集群客户端整合在original-cache包
	注意：真集群只有使用lua脚本才能做到一性操作。
		一般抢购/红包，秒杀，都会在redis里做操作合理性校验。
````

#### [一些常用的Dockerfile](https://github.com/CheukBinLi/DockerHub)
方便自己方便别人 apache httpd  /  nginx  / tomcat 8 / jenkins + docker离线安装，部署脚本
