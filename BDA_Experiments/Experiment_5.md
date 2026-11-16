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
