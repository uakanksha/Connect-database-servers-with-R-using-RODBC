# Connect database server with R using RODBC

Install Package and Load RODBC
```bash
$ library(RODBC); 
```
Connection information
```bash
$ dsn_driver <- "{IBM DB2 ODBC Driver}"
$ dsn_database <- "******"            # e.g. "bludb"
$ dsn_hostname <- "*****************" # e.g "54a2f15b-5c0f-46df-8954-.databases.appdomain.cloud"
$ dsn_port <- "****"                  # e.g. "32733" 
$ dsn_protocol <- "TCPIP"            # i.e. "TCPIP"
$ dsn_uid <- "********"              # e.g. "zjh17769"
$ dsn_pwd <- "********"             # e.g. "zcwd4+8gbq9bm5k4"  
$ dsn_security <- "ssl"
```
Create a database connection
```bash
$ conn_path <- paste("DRIVER=",dsn_driver,
                  ";DATABASE=",dsn_database,
                  ";HOSTNAME=",dsn_hostname,
                  ";PORT=",dsn_port,
                  ";PROTOCOL=",dsn_protocol,
                  ";UID=",dsn_uid,
                  ";PWD=",dsn_pwd,
                  ";SECURITY=",dsn_security,        
                    sep="")
$ conn <- odbcDriverConnect(conn_path)
$ conn
```
Connection Attributes
```bash
$ attributes(conn)
```
Connection Metadata
```bash
$ conn.info <- odbcGetInfo(conn) 
```
Connection Information
```bash
$ conn.info["DBMS_Name"]
conn.info["DBMS_Ver"] 
conn.info["Driver_ODBC_Ver"]
```
Supported Datatypes
```bash
$ sql.info <- sqlTypeInfo(conn)
print(sql.info[c(1,3)], row.names=FALSE) 
```
 List of Tables
```bash
$  tab.frame <- sqlTables(conn, schema="SYSIBM") # e.g. "SYSIBM"
nrow(tab.frame)
tab.frame$TABLE_NAME
```

 Columns in a Table
```bash
$ tab.name <- "SYSSCHEMATA" # e.g. "SYSSCHEMATA"
col.detail <- sqlColumns(conn, tab.name)
print(col.detail[c(2,3,4,6,7,9,18)], row.names=FALSE)
```
Dis-connect
```bash
odbcCloseAll()
```
