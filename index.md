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

#### [Redis多机集群](https://github.com/fdisk123/original/tree/2.20/original-cache)
[![](https://camo.githubusercontent.com/f50b84e13fdbb61d847742c34259c58469c7d2b2/68747470733a2f2f7472617669732d63692e6f72672f70616765732d7468656d65732f6172636869746563742e7376673f6272616e63683d6d6173746572)](https://github.com/fdisk123/original/tree/2.20/original-cache)  
````
	部署档案记录。
	对应的java 集群客户端整合在original-cache包
	注意：真集群只有使用lua脚本才能做到一性操作。
		一般抢购/红包，秒杀，都会在redis里做操作合理性校验。
````

#### [一些常用的Dockerfile](https://github.com/CheukBinLi/DockerHub)
方便自己方便别人 apache httpd  /  nginx  / tomcat 8 / jenkins + docker离线安装，部署脚本