# yisheng2019-Big-Data
易盛实验室2019大数据
hadoop集群配置：

1.参考的教程是
https://www.cnblogs.com/hopelee/p/7049819.html

2.主要的文件java和hadoop分别放在了根目录下的/usr/opt/java和/usr/opt/hadoop;

3.局域网内主机名与IP地址的映射关系:
192.168.3.14 Master
192.168.3.11 Slave4
192.168.3.12 Slave2
192.168.3.13 Slave3

4.安装ssh，配置不用主机间的免密钥登陆:
各服务器可实现root免密登录；
Master可免密登录Slave2和Slave3，同时Slave2可免密登录Slave3；//可能与密钥配置有关，目前仅可实现到这一步（Slave1尚未配置）

5.完全分布式集群配置文件：

	*配置各主机的hadoop文件：	
	1.usr/opt/hadoop/hadoop-2.8.5/etc/hadoop/hadoop-env.sh
　　  export JAVA_HOME=/usr/java/jdk1.8.0_221					//添加java环境变量
	
	2.usr/opt/hadoop/hadoop-2.8.5/etc/hadoop/core-site.xml					//以Master为例
	  <configuration>
		<property>
			<name>hadoop.tmp.dir</name>
			<value>/root/hadoop/tem</value>
			<description>Abase for other temporary directories.</description>
		</property>
		<property>
			<name>fs.default.name</name>
			<value>hdfs://192.168.3.14:9000</value>
		</property>
		<property>
			<name>hadoop.native.lib</name>
			<value>false</value>
			<description>Should native hadoop libraries, if present, be used.</description>
		</property>
	</configuration>
	第一个资源声明的是访问hdfs的web浏览器地址
	第二个资源声明的是在格式化分布式文件系统时所产生的临时文件的存储地址
	
	3.usr/opt/hadoop/hadoop-2.8.5/etc/hadoop/hdfs-site.xml
	  <configuration>
		<property>
			<name>dfs.name.dir</name>
			<value>/root/hadoop/dfs/name</value>
			<description>Path on the lacal filesystem where theNameNode stores the namespace and transactions logs persistently.</description>
		</property>
		<property>
			<name>dfs.data.dir</name>
			<value>/root/hadoop/dfs/data</value>
			<description>Comma separated list of paths on the localfilesystem of a DataNode where it should store its block.</description>
		</property>
		<property>
			<name>dfs.replication</name>
			<value>2</value>
		</property>
		<property>
			<name>dfs.permissions</name>
			<value>true</value>
			<description>need not permissions</description>
		</property>
	 </configuration>
	 声明数据块的备份个数
	 
	 4.usr/opt/hadoop/hadoop-2.8.5/etc/hadoop/mapred-site.xml.template
	  <configuration>
		<property>
			<name>mapred.job.tracker</name>
			<value>192.168.3.14:9001</value>
		</property>
		<property>
			<name>mapred.local.dir</name>
			<value>/root/hadoop/var</value>
		</property>
		<property>
			<name>mapreduce.framework.name</name>
			<value>yarn</value>
		</property>
	 </configuration>
	 声明jobtracker节点，为Master主机，端口为9001
	 
	 5.在Master中 usr/opt/hadoop/hadoop-2.8.5/etc/hadoop/slaves
	  Slave2
	  Slave3
	  Slave4

6.在Master下，启动hadoop服务：

1. 格式化hdfs系统

　　bin/hadoop namenode -format

2.启动dfs服务

　　sbin/start-dfs.sh

3.启动yarn服务

　　sbin/start-yarn.sh
	
	 
	  
	
	











