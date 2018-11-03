# 学习hadoop的笔记

这篇记录将关联在学习hadoop家族不同软件中的过程。

## Hadoop软件的安装

参考官方文档* [HADOOP官方](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/SingleCluster.html#Standalone_Operation)

## 基本流程
### 下载软件
安装java-11 hadoop-3.1.1，
### 进行配置
可以export $JAVA_HOME $HADOOP_HOME, 也可以进入hadoop中的hadoop-env.sh配置，该文件自己去find。
我的配置基本就这一句：export JAVA_HOME=/usr/lib/jvm/jdk-11
然后配置core-site.xml, mapred-site.xml, hdfs-site.xml, yarn-site.xml。具体配置如下：
core-site.xml
```
<configuration>
        <!-- 指定HDFS老大（namenode）的通信地址 -->
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
    <!-- 指定hadoop运行时产生文件的存储路径 -->
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/usr/hadoop/tmp</value>
    </property>
</configuration>
```
mapred-site.xml
`‵‵
<configuration>
    <property>
        <name>mapred.job.tracker</name>
        <value>hdfs://localhost:9001</value>
</property>
<property>
    <name>mapreduce.cluster.local.dir</name>
    <value>/usr/local/hadoop/mapred/local</value>
  </property>
</configuration>
```
hdfs-site.xml
`‵‵
<configuration>
<property>
            <name>dfs.namenode.name.dir</name>
            <value>/usr/local/hadoop/data/nameNode</value>
    </property>

    <property>
            <name>dfs.datanode.data.dir</name>
            <value>/usr/local/hadoop/data/dataNode</value>
    </property>

    <property>
            <name>dfs.replication</name>
            <value>1</value>
    </property>
</configuration>
```
yarn-site.xml
`‵‵
<configuration>

<!-- Site specific YARN configuration properties -->
 <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>
```

### 免密码登陆
ssh localhost
  $ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
  $ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
  $ chmod 0600 ~/.ssh/authorized_keys
 
### 启动
$ bin/hdfs namenode -format
$ sbin/start-dfs.sh
$ jps


