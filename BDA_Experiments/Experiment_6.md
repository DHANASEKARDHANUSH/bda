## EXP.NO:6  INSTALLATION OF HBASE ALONG WITH PRACTICE EXAMPLES

DATE:

AIM:
To install HBase using a virtual machine and perform some operations in HBase.

ALGORITHM:
Step 1: Install a Virtual Machine
• Download and install VirtualBox or VMware.
• Create a new virtual machine and install Ubuntu or CentOS.

Step 2: Set up the Virtual Machine
• Launch the VM and install the operating system.
• Ensure internet connectivity for downloading packages.

Step 3: Install Java
```bash
sudo apt update
sudo apt install default-jdk
java -version
```

Step 4: Download and install HBase
```bash
sudo tar -xvf <hbase_archive_name>.tar.gz
sudo mv <hbase_extracted_directory> /opt/hbase
```

Step 5: Configure HBase
Open the configuration file:
```bash
sudo nano /opt/hbase/conf/hbase-site.xml
```

Add the required properties:

```xml
<configuration>
  <property>
    <name>hbase.rootdir</name>
    <value>file:///var/lib/hbase</value>
  </property>
  <property>
    <name>hbase.zookeeper.property.dataDir</name>
    <value>/var/lib/zookeeper</value>
  </property>
</configuration>
```

Step 6: Start HBase
```bash
sudo /opt/hbase/bin/start-hbase.sh
```

HBASE PRACTICE EXAMPLES:

1. Start HBase shell
```bash
hbase shell
```

2. Create a table
```bash
create 'my_table', 'cf'
```

3. Insert data
```bash
put 'my_table', 'row1', 'cf:column1', 'value1'
put 'my_table', 'row1', 'cf:column2', 'value2'
```

4. Get data
```bash
get 'my_table', 'row1'
```

5. Scan data
```bash
scan 'my_table'
```

6. Delete data
```bash
delete 'my_table', 'row1'
```

7. Disable and drop table
```bash
disable 'my_table'
drop 'my_table'
```

RESULT:
Thus, the installation of HBase using a virtual machine was completed successfully.
