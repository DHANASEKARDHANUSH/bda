# BDA Lab Manual – Corrected and Separated Experiments

## EXP.NO:1  DOWNLOADING AND INSTALLING HADOOP; UNDERSTANDING DIFFERENT HADOOP MODES, STARTUP SCRIPTS, AND CONFIGURATION FILES

DATE:

AIM:
To download and install Hadoop; understand different Hadoop modes, startup scripts, and configuration files.

PREREQUISITES TO INSTALL HADOOP ON WINDOWS
• Virtual Box (for Linux): Used for installing the operating system on it.
• Operating system: You can install Hadoop on Windows or Linux-based operating systems. Ubuntu and CentOS are commonly used.
• Java: You need to install the Java 8 package on your system.
• Hadoop: You require the latest Hadoop version.

1. Install Java
• Java JDK Link to download: https://www.oracle.com/java/technologies/javase-jdk8-downloads.html
• Extract and install Java in C:\Java
• Open cmd and type: javac -version

2. Download Hadoop
https://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz

• Extract to C:\Hadoop

3. Configure environment variables
Set the following system variables:
• JAVA_HOME = C:\Java
• HADOOP_HOME = C:\Hadoop-3.3.0
• PATH = %JAVA_HOME%\bin; %HADOOP_HOME%\bin; %HADOOP_HOME%\sbin

4. Edit configuration files
Edit file C:\Hadoop-3.3.0\etc\hadoop\core-site.xml and paste the following code:

```xml
<configuration>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost:9000</value>
  </property>
</configuration>
```

Rename `mapred-site.xml.template` to `mapred-site.xml` and edit `C:\Hadoop-3.3.0\etc\hadoop\mapred-site.xml`:

```xml
<configuration>
  <property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
  </property>
</configuration>
```

Create the following directories under `C:\Hadoop-3.3.0`:
• `data`
• `data\datanode`
• `data\namenode`

Edit `C:\Hadoop-3.3.0\etc\hadoop\hdfs-site.xml`:

```xml
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>1</value>
  </property>
  <property>
    <name>dfs.namenode.name.dir</name>
    <value>C:/Hadoop-3.3.0/data/namenode</value>
  </property>
  <property>
    <name>dfs.datanode.data.dir</name>
    <value>C:/Hadoop-3.3.0/data/datanode</value>
  </property>
</configuration>
```

Edit `C:\Hadoop-3.3.0\etc\hadoop\yarn-site.xml`:

```xml
<configuration>
  <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
  </property>
  <property>
    <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
    <value>org.apache.hadoop.mapred.ShuffleHandler</value>
  </property>
</configuration>
```

Edit `C:\Hadoop-3.3.0\etc\hadoop\hadoop-env.cmd` and replace:

```cmd
set JAVA_HOME=C:\Java
```

5. Hadoop configuration
Download:
https://github.com/brainmentorspvtltd/BigData/blob/master/Hadoop%20Configuration.zip
or
https://github.com/s911415/apache-hadoop-3.1.0-winutils

• Copy the `bin` folder and replace the existing `bin` folder in `C:\Hadoop-3.3.0\bin`
• Format the NameNode
• Open cmd and type:

```cmd
hdfs namenode -format
```

6. Testing
• Open cmd and change directory to `C:\Hadoop-3.3.0\sbin`
• Type:

```cmd
start-all.cmd
```

(Or you can start them separately)

```cmd
start-dfs.cmd
start-yarn.cmd
```

Make sure these apps are running:
• Hadoop NameNode
• Hadoop DataNode
• YARN Resource Manager

Open:
• http://localhost:8088
• http://localhost:9870

RESULT:
Thus, Hadoop was downloaded and installed successfully, and the different Hadoop modes, startup scripts, and configuration files were understood.
