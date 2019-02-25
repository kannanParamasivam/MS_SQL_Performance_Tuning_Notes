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
* Smallest read in SQL server is a page (8 KB) even though we quried for single row ![read_size] 

[page_life_expectancy]: ./images/page_life_expectancy.PNG
[perf_mon]: ./images/per_mon.PNG
[lazy_write]: ./images/lazy_write.PNG
[stat_io_on]: ./images/stat_io_on.PNG
[read_size]: ./images/read_size.PNG