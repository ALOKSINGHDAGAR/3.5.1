# Load Test Solution For PayrollService  

### Description 
This dockerized solution is built using open source load testing tool k6. Project has been modularized in into different module and has been implemented in javascript.
File `PayrollServiceTest.js` is the main script and rest of the folder are modules.

### Steps to execute load test
* Update the field IP in file named `EnvConfig.json` under folder 'Config' with the IP address of your local machine assuming the dockerized application under test `APP_PERFORMANCE_CC` is running on your local as well.
* Update the field 'Vusers' in file named `WorkloadConfig.json` under folder 'Config' to send the desired number of concurrent mesaages for example if set to 100, same number of messages would be sent concurrently to sns service.
* To execute the test run `docker-compose up` command from the parent directory of solution.


### Steps to validate load test
* Once the test stops it print the summary at the end in the terminal, look for field checks in the summary, ideally it should 100% in case of no failure.
* Debug mode of test is set to full, it would prints the response of all request made.
* Result of load would be logged in folder named Results for further reference.
* Validation from DB - Execute following command to get the count of events processed and avg response time it took post test : `select  count(*) ,avg(  ((DATE_PART('day', processed_at::timestamp - occurred_at::timestamp) * 24 + 
                DATE_PART('hour', processed_at::timestamp - occurred_at::timestamp)) * 60 +
                DATE_PART('minute', processed_at::timestamp - occurred_at::timestamp)) * 60 +
                DATE_PART('second', processed_at::timestamp - occurred_at::timestamp)) as AvgResponseTime from performance p;`  

### Errors that can be encountered while executing the test
If error looks like this `Dial tcp connection refused` then there are chance wrong IP has been used, if you are connected to VPN try with differnt ips' enlisted upon running `ipconfig` in case of winodws and `ifconfig` in case of linux.




