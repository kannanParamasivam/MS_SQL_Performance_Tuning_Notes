* Page Life Expectancy query to find page handing performance   
![page_life_expectancy]
* Perfmon is also can be used to get SQL server performance   
![perf_mon]
* Transaction logs and check point   
* Lazy writes per second   
![lazy_write]
* Performance counter query and Perf. mon. UI tool presents same information
* Physical reads/writes and logical reads/writes
* `SET STATISTICS IO ON` will write IO opertations for quries running in message page    
![stat_io_on]
* `SET STATISTICS TIME ON` will show the CPU time and Elapsed time taken for a query
* Smallest read in SQL server is a page (8 KB) even though we quried for single row ![read_size] 
* **NUMA** setup in SQL server
* Disk should be **formatted as 64 KB memory** allocation and **different disks** should be selected for Transaction Logs and Data File(s)
* SQL Server startup parameters
* Joins, sorting, temp tables and other kind of computations **use temp DB**
* It is better to have as many data files as the number of cores for TEMP DB
* It is recommended to have only one transactional log file as the read write would be faster as it is happening in serial
* Locking table before making bulk inserts/updates/deletes will lock other users from accessing table and SQL stops doing page locks. This makes query execute faster
* `sp_configure` to list and set SQL configurations. Following are the two very important to be taken care   
![sp_config]
* Configuration **optimize_for_ad_hoc_workloads** will increase the performance of Entity Framework. This will cache the execution plans for quries to improve performance
* It is importent to configure max memory can be used by SQL server. Do not let SQL take all the memory because when OS runs out of memory, the server may crash
* It is good to have more **SCSI controllers**
* **XEvents** Profiles better than profiles. Which does not block query execution
* Power option should be **High Performance** in SQL server machine
* **CPU-Z** is the tool to find CPU performance and CPU load details
* Table variable is good for 10 to 100 rows, if rows are more than that go for temp table
* Do not use sub quries instead, create temp table with necessary data and do join
* Do not use DataBase name in when mentioning table in query with its fully qualified name. Because when database name is mentioned, SQL server will go to master database and check if database exists which increase the cost
* Do use schema name because when schema name is not mentioned in fully qualified name, it will go and check if table exists in dbo schema
* Do not use hard code IN list, create table or temp table for it
* If local variable whos value does not change, hard code it in query. This way it can take advantage of DENSITY optimization
* Avoid user defined functions in quries
* Do add DDL statements between DML statements which will cause rebuild for every new DDL statement
* Table variable does not support statistics but temp table does, so do not use table variable for rows more than hundred
* **PoorSQL.com** is to format quries
* Enable `Query Optimizer Fixes` when upgraded to newer version of SQL server which will apply new query optimization improvements (fixes) in the database
* Enable `Query Optimizer Fixes` in database to enable the improvements added to the version of SQL server on Query Optimization    
![enabling_query_optimizer_fixes]   
* We can Connect to SQL Server instance from SSMS with custom parameters
![connect_to_sql_server_with_custom_parameters]


## Tools to get diagnostic info from SQL server
> * Pssdiag and sqldiag to collect diagnostic info from SQL server. Available for free for download from github. SQL customer support team uses it
> * Import this data into DB and generate reports   
![diag]
![pssdiag1]
![pssdiag2]
![pssdiag3]
![collection_started]
> * SQL Nexus is used to view the report collected. This tool provide suggestions on indexes, information about locks and performance tuning suggestions. This also would be available in github
![import_nexus]

## Indexes
* Types of Inexes   
![types_of_indexes]
* Clustered Index   
![clustered_index]
* Non-Clustered Index has include functionality which include data of other columns which does not need to do key lookup. In Non-Clustered index we should be eliminating key lookup by including clolumns to improve performance.
* SARGability

## Statistics
* Statistics is sampling of data which is used by optimizer to select between different types of access methods
* Statistics will be created in following situations
    * When creating Index
    * Auto create statistics is on by default
    * Can create statistics manually
* By default statistics set for auto update. Auto update statistics can be configured as async

## Heap
* Does non-clustered index creates heap?

## Compressions
* Compressing table fits more data in every page and it will decrease the number of logical reads and which increase the performance of the query
* Compressing will take more CPU than non compressed table because decomressing (typecasting) needs more CPU
* TODO: How to add compressing to a table.
* Two types of compression
    * Row compression - which reduses unused space in rows data types
    * Page compression - which does Row Compression and on top of that it will do compress page data. (i.e when a column has same data repeated, it will compress it)
* Index can also be compressed

## Parameter Sniffing problem

## SQL server 2017 Features
* Adaptive query processing

## Question
* what are processor sockets in vms?
* What is Hyper-V?
* What is seek and scan in SQL server?
    * Scan is reading all data in a table
    * Seek is reading row with condition i.e., where clause
* What should be done when table is too older and has lot of data which does not fit in memory without going to temp db?
* What is Histogram?
* What is Cardinality? (Cardinality estimator)
* What is Density?
    - Find the frequency of data in rows of the table.
* What are Filtered Index and Filtered Statistics?
* APPLY instead of Joins. Cross Apply and Outer Apply
* What are Query Hints in SQL sever?
* What are "Availability Groups"?
* Difference between High Availability and Disaster Recovery?

## Notes
* David Klee have atricles about SQL in Virtual machine (https://www.davidklee.net/articles/)
* Commands for DataBase Administration is available at https://dbatools.io/ 

[page_life_expectancy]: ./images/page_life_expectancy.PNG
[perf_mon]: ./images/per_mon.PNG
[lazy_write]: ./images/lazy_write.PNG
[stat_io_on]: ./images/stat_io_on.PNG
[read_size]: ./images/read_size.PNG
[sp_config]: ./images/sp_config.PNG
[diag]: ./images/diagnostics.PNG
[pssdiag1]: ./images/pssdiag1.PNG
[pssdiag2]: ./images/pssdiag2.PNG
[pssdiag3]: ./images/pssdiag3.PNG
[collection_started]: ./images/collection_started.PNG
[import_nexus]: ./images/import_nexus.PNG
[types_of_indexes]: ./images/types_of_indexes.PNG 
[clustered_index]: ./images/clustered_index.PNG
[enabling_query_optimizer_fixes]: ./images/enabling_query_optimizer_fixes.PNG
[connect_to_sql_server_with_custom_parameters]: ./images/connect_to_sql_server_with_custom_parameters.PNG