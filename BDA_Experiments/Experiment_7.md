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
