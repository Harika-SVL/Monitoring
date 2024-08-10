### Hospital Management System – Needs W.r.t Application Stability

* The architecture of management System is as follows

![alt text](shots/1.PNG)

* Your organization `qtinfosystems` is maintaing this system for 100 hospitals
* Now let's try to figure out some failures
    * Network failures
    * Hardware failures
    * Application failures
* You are assigned to figure out failures. To solve this issues we will figure out a pro-active approach
    * For every 1 minute
        * check if every server is responding or not
        * Check if  application is responding or not
    * Alert if the servers/applications are not responding
* Log is a record which specifies some activity done
    * Operating systems have logs, we might need to finetune it
        * Windows => event viewer
        * Linux => Syslog
    * Applications also log, try to understand about failure from there
* Tracing is an approach to figure out the flow in your system
* Every system has resource utilization information
    * cpu
    * memory
    * disk
    * network
* Metrics are values which represent some information about system/application with value as number with time dimension
* QT Info System needs a Monitoring Solution.
* Observability is what QT Info System needs i.e. they need to get
    * logs
    * metrics
    * traces
* MTTR (Mean Time To Recover) this refers to average time taken by your organization to recover from failures
* MTTF (Mean Time To Fail): This refers to average time during the certain to get an failure in your system
* SLA (Service Level Agreement): This is an agreement between service provider and customer w.r.t to availability and other important metrics

### What has to be monitored?

* There are organizations and individuals who have published the best practices on implementing a monitoring solution
    * Google Four Golden signals 
    
    [ Refer Here : https://sre.google/sre-book/monitoring-distributed-systems/ ]

    * USE method 
    
    [ Refer Here : https://www.brendangregg.com/usemethod.html ]

    * RED method 
    
    [ Refer Here :  ]

![alt text](shots/2.PNG)

### Terms in Monitoring


* Latency
* Traffic
* Errors
* Saturation

### Some basic Stuff


* Impact of  CPU, Memory and DISK on your applicaions

![alt text](shots/3.PNG)

* _**Webserver**_ : When requests are sent, threads are created which will have its own  cpu and memory share. So as number of requests increase the load on cpu and memory increases.

![alt text](shots/4.PNG)

* Generally, to figure out the saturation points, organizations stress/load the systems with the help of performance test engineers

### Metrics

* for detailed info on logs vs metrics vs traces

    [ Refer Here : https://microsoft.github.io/code-with-engineering-playbook/observability/log-vs-metric-vs-trace/ ]

* _**Metrics**_ : Metrics are numeric time-series data.

### Logs

* Logs are text informations with no standard way/format.
* Logs from different applications/servers
    * Apache `192.168.2.20 - - [28/Jul/2006:10:27:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395`
    * For some other  applications

    [ Refer Here : https://www.ossec.net/docs/log_samples/ ]
    
* For logs we deal with text (unstructured data)
* Using logs requires a solution to
    * convert unstructured text in semi structured
    * understand logs with various format
    * Log analysis solution

### Traces

* APM ( Application Performance Monitoring) Agents can help
* We are trying to make our applications observable
* Monitoring tells you when something is wrong, while observability enables you to understand why.
* Tools

![alt text](shots/5.PNG)

### Pull vs Push Monitoring

* _**Pull Monitoring**_ : Monitoring System pulls the information from various servers/applications/network devices the metrics.

![alt text](shots/6.PNG)

* _**Push Monitoring**_ : Monitoring system get the information from various servers/applications

![alt text](shots/7.PNG)

* Examples
 1. Pull:
        * Prometheus
        * Nagios
 2. Push:
        * Log stash
        * splunk

### Elastic Stack

* This was called as ELK Stack
* ELK
    * E = Elastic Search
    * L = Log Stash
    * K = Kibana
* Architecture

![alt text](shots/8.PNG)

* _**Elastic Search**_ : This is memory or storage system in the Elastic Stack
* _**Logstash**_ : Responsible for making logs queryable
* _**Beats**_ : Export metrics, logs, traces to Elastic Search
* _**Kibana**_ : Creates dashboards and visualizations

### Google for the following

* What are popular metrics for
    * web server (apache)
    * database (mysql)
* Web Servers
    * Requests per second
    * Errors
    * Thread count
    * Response Time (Average)
* Server:
    * CPU Uilization
    * Free Memory/Used Memory
    * Disk Space
    * Disk I/O
    * Network
        * Incoming
        * Outgoing
* Databases:
    * Number of Connetions
    * Size of Data Processed per second
    * Database Size

### Applications we will be observing


* _**Traditional Applications**_ : These are the applications which run on physical or virtual machines hosted on-premises or cloud
* _**Containerized Applications**_ : These will be the applications running on kubernetes cluster.
* Technology:
    * Python
    * .net
    * C#
    * nodejs
* Approach:
    * We will be getting info in the following order
        * metrics
        * logs
        * traces
    * What is Site Reliability Engineering?

### Traditional Applications

* I will be sharing some scripts when necessary
* Let's choose the same applications for both traditional and k8s

### Lab Setup

* Cloud Account (AWS/Azure)
* Elastic Cloud (14 day free trail)
* How to create VMs?

### Options

* Ecommerce
    * shopizer (java)
    * nopCommerce (.net)
    * Saleor (python)
    * Sprut Commerce (nodejs)
* Medical Record System/Hospital managment system
    * Open Mrs (java)
    * Bahmni (java)
    * hospital run (node js)

### NOP Commerce

* To install this application we need atleast two servers
    * database server: (Linux/Windows)
        * mysql
        * microsoft sql server
        * postgres
    * application/web server: (Linux/Windows)
    * dotnet core
    * nginx
* Our setup:
    * 2 ubuntu Linux servers
* Metrics:
    * Server Metrics
        * cpu
        * memory
        * disk
        * network
    * Application metrics
        * Requests
        * Errors
        * Response time
* Installation
    * Manual
    * Automated 

### nopCommerce Architecture

* This  application has two  servers involved

* Application:
    * This application runs on .net core 7
    * install the application
    * If the application is horizontally scaled, then we will be using a loadbalancer/reverse  proxy
* Database
    * we will be using mysql database
    * This can be a managed database

    ![alt text](shots/9.PNG)

### Realizing this application in AWS

* Let me create a free tier rds based mysql
* Install dotnet 7 on ubuntu vm 

    [ Refer Here : https://learn.microsoft.com/en-us/dotnet/core/install/linux-scripted-manual#scripted-install ]

* For installing nopcommerce on linux

    [ Refer Here : https://docs.nopcommerce.com/en/installation-and-upgrading/installing-nopcommerce/installing-on-linux.html ]

* Refer To classroom video for installation

### Next Steps

* Let's create a basic check to verify if
    * the server is alive
    * the application is alive
* _**Email Alerts**_ : Create an inbox in mail trap

    [ Refer Here : https://mailtrap.io/ ]

### Monitoring and Observability Setup

#### Labsetup

* We will be using two elastic cloud accounts
    * one account for dev/experimentation
    * other account for making nopCommerce observable
* We need a mail trap setup for alerts where we will have two inboxes

### Working with Elastic Stack

* Understanding of YAML

    [ Refer here : https://www.youtube.com/watch?v=ggOmHlnhPaM&list=PLuVH8Jaq3mLud3sVDvJ-gJ__0zd15wGDd&index=16 ]





























