# yisheng2019-Big-Data
易盛实验室2019大数据
hadoop集群配置：

1.主要参考的教程是
https://www.cnblogs.com/hopelee/p/7049819.html

2.主要的文件java和hadoop分别放在了根目录下的/usr/opt/java和/usr/opt/hadoop;

3.局域网内主机名与IP地址的映射关系:
192.168.3.14 Master
192.168.3.11 Slave1
192.168.3.12 Slave2
192.168.3.13 Slave3

4.安装ssh，配置不用主机间的免密钥登陆:
各服务器可实现root免密登录；
Master可免密登录Slave2和Slave3，同时Slave2可免密登录Slave3；//可能与密钥配置有关，目前仅可实现到这一步（Slave1尚未配置）

5.各配置文件尚未配置；
