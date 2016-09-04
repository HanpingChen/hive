# hive
安装hive
在安装hive之前需要保证hadoop能够正常的运行
首先需要做的事情是下载hive，在官网下载之后传到想要的位置解压，然后在conf文件下，创建hive-site.xml
配置如下：
```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
        <property>
                <name>javax.jdo.option.ConnectionURL</name>
                <value>jdbc:mysql://114.215.133.63:3306/hive</value>
        </property>
        <property>
                <name>javax.jdo.option.ConnectionDriverName</name>
                <value>com.mysql.jdbc.Driver</value>
        </property>
        <property>
                <name>javax.jdo.option.ConnectionUserName</name>
                <value>root</value>
        </property>
        <property>
                <name>javax.jdo.option.ConnectionPassword</name>
                <value>yourpasswd</value>
        </property>
        <property>
                 <name>hive.insert.into.multilevel.dirs</name>
                <value>true</value>
        </property>
</configuration>
```

这个配置文件是参照官网上配置数据源的文档，这里是用的MySQL，配置了MySQL的地址和jdbc驱动，登录的用户名和密码等信息

## 安装MySQL
由于hive远程模式，是使用MySQL作为远程数据库存储数据，所以需要用到MySQL数据库，我们可以在一台用来安装数据库的服务器上，
安装上MySQL
在Ubuntu命令行输入命令
```
apt-get mysql.server,mysql.client
```
就会自动安装好MySQL,还会设置好root用户的账户和密码
要使用MySQL还需要将jdbc的驱动的jar包，拷贝在hive的lib目录下

导入完jar包之后就可以在hive的bin目录下，先初始化，当然只有第一次需要
```
./schematool -dbType mysql -initSchema
```
完成初始化之后，再执行hive命令，就可以进入hive提示符了。
