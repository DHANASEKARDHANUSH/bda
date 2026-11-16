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
