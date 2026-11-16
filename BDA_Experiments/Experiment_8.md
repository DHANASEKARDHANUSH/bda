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
