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

---

## EXP.NO:2  HADOOP IMPLEMENTATION OF FILE MANAGEMENT TASKS, SUCH AS ADDING FILES AND DIRECTORIES, RETRIEVING FILES, AND DELETING FILES

DATE:

AIM:
To implement file management tasks in Hadoop such as adding files and directories, retrieving files, and deleting files.

1. Create a directory in HDFS at the given path(s)
Usage:
```bash
hadoop fs -mkdir <paths>
```
Example:
```bash
hadoop fs -mkdir /user/saurzcode/dir1 /user/saurzcode/dir2
```

2. List the contents of a directory
Usage:
```bash
hadoop fs -ls <args>
```
Example:
```bash
hadoop fs -ls /user/saurzcode
```

3. Upload and download a file in HDFS
Upload:
```bash
hadoop fs -put <localsrc> ... <HDFSdestPath>
```
Example:
```bash
hadoop fs -put /home/saurzcode/Samplefile.txt /user/saurzcode/dir3/
```

Download:
```bash
hadoop fs -get <hdfsSrc> <localdst>
```
Example:
```bash
hadoop fs -get /user/saurzcode/dir3/Samplefile.txt /home/
```

4. View contents of a file
Usage:
```bash
hadoop fs -cat <path/filename>
```
Example:
```bash
hadoop fs -cat /user/saurzcode/dir1/abc.txt
```

5. Copy a file from source to destination
Usage:
```bash
hadoop fs -cp <source> <dest>
```
Example:
```bash
hadoop fs -cp /user/saurzcode/dir1/abc.txt /user/saurzcode/dir2
```

6. Copy a file from local file system to HDFS
Usage:
```bash
hadoop fs -copyFromLocal <localsrc> <URI>
```
Example:
```bash
hadoop fs -copyFromLocal /home/saurzcode/abc.txt /user/saurzcode/abc.txt
```

7. Copy a file from HDFS to local file system
Usage:
```bash
hadoop fs -copyToLocal [-ignorecrc] [-crc] <URI> <localdst>
```
Example:
```bash
hadoop fs -copyToLocal /user/saurzcode/abc.txt /home/saurzcode/
```

8. Move a file from source to destination
Usage:
```bash
hadoop fs -mv <src> <dest>
```
Example:
```bash
hadoop fs -mv /user/saurzcode/dir1/abc.txt /user/saurzcode/dir2
```

9. Remove a file or directory in HDFS
Usage:
```bash
hadoop fs -rm <arg>
```
Example:
```bash
hadoop fs -rm /user/saurzcode/dir1/abc.txt
```

Recursive delete:
```bash
hadoop fs -rmr <arg>
```
Example:
```bash
hadoop fs -rmr /user/saurzcode/
```

10. Display last few lines of a file
Usage:
```bash
hadoop fs -tail <path/filename>
```
Example:
```bash
hadoop fs -tail /user/saurzcode/dir1/abc.txt
```

11. Display the aggregate length of a file
Usage:
```bash
hadoop fs -du <path>
```
Example:
```bash
hadoop fs -du /user/saurzcode/dir1/abc.txt
```

RESULT:
Thus, the Hadoop implementation of file management tasks, such as adding files and directories, retrieving files, and deleting files, was executed successfully.

---

## EXP.NO:3  IMPLEMENTATION OF MATRIX MULTIPLICATION WITH HADOOP MAPREDUCE

DATE:

AIM:
To write a MapReduce program that implements matrix multiplication.

ALGORITHM:
We assume that the input matrices are already stored in HDFS in a suitable format such as CSV or TSV, where each row represents a matrix element. The matrices are compatible for multiplication (the number of columns in the first matrix equals the number of rows in the second matrix).

STEP 1: Mapper
The mapper takes the input matrices and emits key-value pairs for each element in the result matrix. The key is the (row, column) index of the result element, and the value is the corresponding element value.

STEP 2: Reducer
The reducer receives the key-value pairs emitted by the mapper and calculates the partial sum for each element in the result matrix.

STEP 3: Main Driver
The main driver class sets up the Hadoop job configuration and specifies the input and output paths for the matrices.

STEP 4: Running the job
To run the MapReduce job, package the classes into a JAR file and then submit it to Hadoop using the `hadoop jar` command.

PROGRAM:

```java
import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;

public class MatrixMultiplicationDriver {

    public static class MatrixMultiplicationMapper
            extends Mapper<LongWritable, Text, Text, IntWritable> {

        @Override
        protected void map(LongWritable key, Text value, Context context)
                throws IOException, InterruptedException {

            String[] elements = value.toString().split(",");
            int row = Integer.parseInt(elements[0]);
            int col = Integer.parseInt(elements[1]);
            int val = Integer.parseInt(elements[2]);

            context.write(new Text(row + "," + col), new IntWritable(val));
        }
    }

    public static class MatrixMultiplicationReducer
            extends Reducer<Text, IntWritable, Text, IntWritable> {

        @Override
        protected void reduce(Text key, Iterable<IntWritable> values, Context context)
                throws IOException, InterruptedException {

            int result = 0;
            for (IntWritable value : values) {
                result += value.get();
            }

            context.write(key, new IntWritable(result));
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "Matrix Multiplication");

        job.setJarByClass(MatrixMultiplicationDriver.class);
        job.setMapperClass(MatrixMultiplicationMapper.class);
        job.setReducerClass(MatrixMultiplicationReducer.class);
        job.setInputFormatClass(TextInputFormat.class);
        job.setOutputFormatClass(TextOutputFormat.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);

        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));

        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

Run the program:
```bash
hadoop jar matrixmultiplication.jar MatrixMultiplicationDriver <input_path> <output_path>
```

RESULT:
Thus, the matrix multiplication program using Hadoop MapReduce was implemented successfully.

---

## EXP.NO:4  RUN A BASIC WORD COUNT MAPREDUCE PROGRAM TO UNDERSTAND THE MAPREDUCE PARADIGM

DATE:

AIM:
To write a basic Word Count program to understand the MapReduce paradigm.

ALGORITHM:
The entire MapReduce program can be divided into three parts:
• Mapper phase code
• Reducer phase code
• Driver code

STEP 1: Mapper code
We create a class `Map` that extends the `Mapper` class defined in the MapReduce framework.
• Input key: offset of each line in the text file (`LongWritable`)
• Input value: each individual line (`Text`)
• Output key: tokenized word (`Text`)
• Output value: hardcoded 1 (`IntWritable`)

STEP 2: Reducer code
We create a class `Reduce` that extends `Reducer`.
• Input key: unique word after sorting and shuffling (`Text`)
• Input value: list of integers corresponding to each key (`IntWritable`)
• Output key: unique word (`Text`)
• Output value: number of occurrences (`IntWritable`)

STEP 3: Driver code
We set the job configuration, specify the mapper and reducer classes, and define input and output paths.

PROGRAM:

```java
import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;

public class WordCount {

    public static class Map extends Mapper<LongWritable, Text, Text, IntWritable> {
        @Override
        public void map(LongWritable key, Text value, Context context)
                throws IOException, InterruptedException {

            String line = value.toString();
            StringTokenizer tokenizer = new StringTokenizer(line);

            while (tokenizer.hasMoreTokens()) {
                String word = tokenizer.nextToken();
                context.write(new Text(word), new IntWritable(1));
            }
        }
    }

    public static class Reduce extends Reducer<Text, IntWritable, Text, IntWritable> {
        @Override
        public void reduce(Text key, Iterable<IntWritable> values, Context context)
                throws IOException, InterruptedException {

            int sum = 0;
            for (IntWritable value : values) {
                sum += value.get();
            }
            context.write(key, new IntWritable(sum));
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "My Word Count Program");

        job.setJarByClass(WordCount.class);
        job.setMapperClass(Map.class);
        job.setReducerClass(Reduce.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        job.setInputFormatClass(TextInputFormat.class);
        job.setOutputFormatClass(TextOutputFormat.class);

        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));

        Path outputPath = new Path(args[1]);
        outputPath.getFileSystem(conf).delete(outputPath, true);

        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

Run the MapReduce code:
```bash
hadoop jar hadoop-mapreduce-examples.jar wordcount /sample/input /sample/output
```

RESULT:
The basic Word Count program was executed successfully to understand the MapReduce paradigm.

---

## EXP.NO:5  INSTALLATION OF HIVE ALONG WITH PRACTICE EXAMPLES

DATE:

AIM:
To install Hive along with practice examples.

PREREQUISITES:
• Java Development Kit (JDK) installed and the JAVA_HOME environment variable set.
• Hadoop installed and configured on your Windows system.

STEP-BY-STEP INSTALLATION:
1. Download Hive from the official Apache Hive website.
2. Extract the archive to a directory on your Windows machine, for example `C:\hive`.
3. Configure Hive by setting the required properties in the Hive configuration file under `conf`.
4. Add the Hive binary directory to the `PATH` variable.
5. Set `HIVE_HOME` to the installation directory.
6. Start the Hive Metastore service.
7. Start the Hive shell using the `hive` command.

Example configuration:

```xml
<configuration>
  <property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:derby:;databaseName=C:/hive/metastore_db;create=true</value>
    <description>JDBC connect string for a JDBC metastore.</description>
  </property>
</configuration>
```

EXAMPLES:

1. Create a database:
```sql
CREATE DATABASE mydatabase;
```

2. Use a database:
```sql
USE mydatabase;
```

3. Show databases:
```sql
SHOW DATABASES;
```

4. Create a table:
```sql
CREATE TABLE mytable (
    id INT,
    name STRING,
    age INT
);
```

5. Show tables:
```sql
SHOW TABLES;
```

6. Describe a table:
```sql
DESCRIBE mytable;
```

7. Insert data into a table:
```sql
INSERT INTO TABLE mytable (id, name, age) VALUES (1, 'John Doe', 25);
```

8. Select data from a table:
```sql
SELECT * FROM mytable WHERE age > 20;
```

RESULT:
Thus, the installation of Hive was completed successfully.

---

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

---

## EXP.NO:7  INSTALLATION OF THRIFT

DATE:

AIM:
To install Apache Thrift on Windows OS.

ALGORITHM:
Step 1: Download Apache Thrift
• Visit the Apache Thrift website: https://thrift.apache.org/
• Go to the Downloads section and download the latest Windows binary distribution.

Step 2: Extract the ZIP file
• Extract the ZIP file to a directory of your choice.
• This directory will be referred to as `<THRIFT_DIR>` in the following steps.

Step 3: Set up environment variables
• Open the System Properties window and select Environment Variables.
• Under System variables, select `Path` and click Edit.
• Add the following paths:

```text
<THRIFT_DIR>\bin
<THRIFT_DIR>\lib
```

Step 4: Verify the installation
Open a new Command Prompt and run:

```cmd
thrift --version
```

If everything is set up correctly, the installed version of Thrift is displayed.

RESULT:
Thus, Apache Thrift was installed successfully on Windows.

---

## EXP.NO:8  PRACTICE IMPORTING AND EXPORTING DATA FROM VARIOUS DATABASES

DATE:

AIM:
To import and export data from various databases using Sqoop.

ALGORITHM:
Step 1: Install Sqoop
• Install Sqoop on your Hadoop cluster or machine.
• Download the latest version from the Apache Sqoop website: http://sqoop.apache.org/

Step 2: Importing data from a database
Use the following syntax:

```bash
sqoop import \
  --connect jdbc:<DB_TYPE>://<DB_HOST>:<DB_PORT>/<DB_NAME> \
  --username <DB_USERNAME> \
  --password <DB_PASSWORD> \
  --table <TABLE_NAME> \
  --target-dir <HDFS_TARGET_DIR> \
  -m <NUMBER_OF_MAP_TASKS>
```

Example:
```bash
sqoop import \
  --connect jdbc:mysql://localhost:3306/testdb \
  --username root \
  --password root123 \
  --table employee \
  --target-dir /user/hadoop/employee \
  -m 1
```

Step 3: Exporting data to a database
Use the following syntax:

```bash
sqoop export \
  --connect jdbc:<DB_TYPE>://<DB_HOST>:<DB_PORT>/<DB_NAME> \
  --username <DB_USERNAME> \
  --password <DB_PASSWORD> \
  --table <TABLE_NAME> \
  --export-dir <HDFS_EXPORT_DIR> \
  --input-fields-terminated-by <DELIMITER>
```

Example:
```bash
sqoop export \
  --connect jdbc:mysql://localhost:3306/testdb \
  --username root \
  --password root123 \
  --table employee \
  --export-dir /user/hadoop/employee \
  --input-fields-terminated-by ','
```

RESULT:
Thus, the import and export of data from various databases using Sqoop were executed successfully.
