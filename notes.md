### Hospital Management System – Needs W.r.t Application Stability

* The architecture of management system is as follows

![alt text](shots/1.PNG)

* Your organization `qtinfosystems` is maintaing this system for 100 hospitals
* Now let's try to figure out some failures
    * Network failures
    * Hardware failures
    * Application failures
* You are assigned to figure out failures. To solve this issues we will figure out a _**pro-active approach**_
    * For every 1 minute
        * Check if every server is responding or not
        * Check if  application is responding or not
    * Alert if the servers / applications are not responding
* _**Log**_ is a record which specifies some activity done
    * Operating systems have logs, we might need to finetune it
        * Windows => event viewer
        * Linux => Syslog
    * Applications also log, try to understand about failure from there
* _**Tracing**_ is an approach to figure out the flow in your system
* Every system has resource utilization information
    * cpu
    * memory
    * disk
    * network
* _**Metrics**_ are values which represent some information about system / application with value as number with time dimension
* QT Info System needs a `Monitoring` Solution
* _**Observability**_ is what QT Info System needs i.e. they need to get
    * logs
    * metrics
    * traces
* _**MTTR ( Mean Time To Recover )**_ : This refers to average time taken by your organization to `recover from failures`
* _**MTTF ( Mean Time To Fail )**_ : This refers to `average time` during the `certain to get an failure` in your system
* _**SLA ( Service Level Agreement )**_ : This is an agreement between service provider and customer w.r.to availability and other important metrics

#### What has to be monitored?

* Organizations and individuals who have published the best practices on implementing a `monitoring solution`

 1. Google Four Golden signals 
    
    [ Refer Here : https://sre.google/sre-book/monitoring-distributed-systems/ ]

 2. USE method 
    
    [ Refer Here : https://www.brendangregg.com/usemethod.html ]

 3. RED method 

![alt text](shots/2.PNG)

#### Terms in Monitoring

* Latency
* Traffic
* Errors
* Saturation

#### Some basic stuff


* Impact of  CPU, Memory and DISK on your applicaions

![alt text](shots/3.PNG)

* _**Webserver**_ : When requests are sent, threads are created which will have its own  cpu and memory share. So as number of requests increase the load on cpu and memory increases

![alt text](shots/4.PNG)

* Generally, to figure out the saturation points, organizations stress / load the systems with the help of performance test engineers

### Metrics

* For detailed info on `logs v/s metrics v/s traces`

    [ Refer Here : https://microsoft.github.io/code-with-engineering-playbook/observability/log-vs-metric-vs-trace/ ]

* Metrics are numeric time-series data

### Logs

* Logs are text informations with no standard way / format
* Logs from different applications / servers
    
1.  Apache `192.168.2.20 - - [28/Jul/2006:10:27:10 -0300] "GET /cgi-bin/try/ HTTP/1.0" 200 3395`
 2. For some other  applications

    [ Refer Here : https://www.ossec.net/docs/log_samples/ ]
    
* For logs we deal with text (unstructured data)
* Using logs requires a solution to :
    * convert unstructured text in semi-structured
    * understand logs with various format
    * Log analysis solution

### Traces

* _**APM ( Application Performance Monitoring)**_ agents can help
* We are trying to make our applications observable
* ` Monitoring` tells you when something is wrong, while `observability` enables you to understand why
* Tools

![alt text](shots/5.PNG)

### Pull v/s Push Monitoring

* _**Pull Monitoring**_ : Monitoring system pulls the information from various servers / applications / network devices the metrics

![alt text](shots/6.PNG)

* _**Push Monitoring**_ : Monitoring system get the information from various servers / applications

![alt text](shots/7.PNG)

* Examples
 1. Pull :
    * Prometheus
    * Nagios
 2. Push :
    * Log stash
    * Splunk

### Elastic Stack

* This was called as _**ELK Stack**_
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

#### Google for the following

* What are the common metrics for
    * web server ( apache )
    * database ( mysql )
* Web Servers
    * Requests per second
    * Errors
    * Thread count
    * Response Time ( Average )
* Server
    * CPU Uilization
    * Free Memory / Used Memory
    * Disk Space
    * Disk I/O
    * Network
        * Incoming
        * Outgoing
* Databases
    * Number of Connetions
    * Size of Data Processed per second
    * Database Size

### Applications we will be observing


 1. _**Traditional Applications**_ : These are the applications which run on physical or virtual machines hosted on-premises or cloud
 2. _**Containerized Applications**_ : These will be the applications running on kubernetes cluster
* Technology :
    * Python
    * .net
    * C#
    * nodejs
* Approach :
    * We will be getting info in the following order
        * metrics
        * logs
        * traces
    * What is Site Reliability Engineering ?

### Traditional Applications

* Let's choose the same applications for both traditional and k8s

#### Lab Setup

* Cloud Account (AWS/Azure)
* Elastic Cloud (14 day free trail)
* How to create VMs?

#### Options

* Ecommerce
    * shopizer ( java )
    * nopCommerce ( .net )
    * Saleor ( python )
    * Sprut Commerce ( nodejs )
* Medical record system / Hospital managment system
    * Open Mrs ( java )
    * Bahmni ( java )
    * Hospital run ( node js )

### Application - NOP Commerce

* To install this application we need atleast two servers
 1. Database server : ( Linux / Windows )
    * mysql
    * microsoft sql server
    * postgres
 2. Application / web server : ( Linux / Windows )
    * dotnet core
    * nginx
* Our setup :
    * Two ubuntu Linux servers
* Metrics :
    * Server metrics
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

#### nopCommerce Architecture

* This  application has two  servers involved

 1. Application 
    * This application runs on .net core 7
    * Install the application
    * If the application is horizontally scaled, then we will be using a loadbalancer / reverse  proxy
 2. Database
    * We will be using mysql database
    * This can be a managed database

    ![alt text](shots/9.PNG)

### Realizing the application in AWS

* Let me create a free tier rds based mysql
* Install dotnet 7 on ubuntu VM 

    [ Refer Here : https://learn.microsoft.com/en-us/dotnet/core/install/linux-scripted-manual#scripted-install ]

* For installing nopcommerce on linux

    [ Refer Here : https://docs.nopcommerce.com/en/installation-and-upgrading/installing-nopcommerce/installing-on-linux.html ]

#### Next Steps

* Let's create a basic check to verify if
    * the server is alive
    * the application is alive
* _**Email Alerts**_ : Create an inbox in mail trap

    [ Refer Here : https://mailtrap.io/ ]

### Monitoring and Observability setup

#### Lab Setup

* We will be using two elastic cloud accounts
    * one account for dev / experimentation
    * other account for making nopCommerce observable
* We need a mail trap setup for alerts where we will have two inboxes

### Working with Elastic Stack

* Understanding of YAML

    [ Refer here : https://www.youtube.com/watch?v=ggOmHlnhPaM&list=PLuVH8Jaq3mLud3sVDvJ-gJ__0zd15wGDd&index=16 ]

### Elastic Cloud Account Setup

* Create a free trail account 

    [ Refer Here : https://www.elastic.co/cloud/ ]

![alt text](shots/10.PNG)
![alt text](shots/11.PNG)
![alt text](shots/12.PNG)
![alt text](shots/13.PNG)
![alt text](shots/14.PNG)
![alt text](shots/15.PNG)
![alt text](shots/16.PNG)

* Let's setup connectors for communications ( email / teams / slack )

![alt text](shots/17.PNG)
![alt text](shots/18.PNG)
![alt text](shots/19.PNG)
![alt text](shots/20.PNG)

* For email, create account in mailtrap and use the credentials of mail trap over here
* Enter the details of mail trap in email and run the test 

![alt text](shots/21.PNG)
![alt text](shots/22.PNG)

#### Workflow

* Overview

![alt text](shots/23.PNG)

* We will have a system with heartbeat installed which checks if the application / server is up or not and reports the status to elastic cloud ( elastic search )
* The uptime in observability section of elastic cloud will show the status of each service / server from which you can configure alerts based on connectors

### Uptime monitoring

* Overview of the setup

![alt text](shots/24.PNG)

* Let's create a linux machine and
    * install heart beat
    * configure heart beat to send metrics to elastic  cloud
* We will be configuring heart beat to check if the
    * apache  server is alive
    ```
    bash
    sudo apt update
    sudo apt install apache2 -y
    ```
#### _**Heart beat installation**_ :
    
* Overview [  Refer Here : https://www.elastic.co/guide/en/beats/heartbeat/current/heartbeat-installation-configuration.html ]

* Official doc's for installing heart beat

    [ Refer here : https://www.elastic.co/guide/en/beats/heartbeat/current/heartbeat-installation-configuration.html#installation ] 
    
* For `apt` package based installation

    [ Refer Here : https://www.elastic.co/guide/en/beats/heartbeat/current/setup-repositories.html#_apt ]

#### _**Configuration**_ :

* All the elastic stack is generally installed and configuration files are stored in similar directories

* _**config location**_ : /etc/<prod-name>

* _**install location**_ : /usr/share/<prod-name>

* Edit `/etc/heartbeat/heartbeat.yml` to add cloud id and authentication
* What has to be monitored ?
    * apache server
    * Monitor types
    
    [ Refer Here : https://www.elastic.co/guide/en/beats/heartbeat/current/configuration-heartbeat-options.html#monitor-types ]

* Configuration 

![alt text](shots/25.PNG)

* Start heart beat 

    [ Refer Here : https://www.elastic.co/guide/en/beats/heartbeat/current/heartbeat-installation-configuration.html#start ]

![alt text](shots/26.PNG)

* Now open kibana & navigate to uptime

![alt text](shots/27.PNG)
![alt text](shots/28.PNG)

* To view the down status, stop the service and wait for the page to reload

![alt text](shots/29.PNG)

* Let's create an alert to send email about status of server

![alt text](shots/30.PNG)
![alt text](shots/31.PNG)

#### Exercise

* Create an alert to check if the nop-app and nop-db is up or not
* Create a linux VM install apache / nginx
* Also create uptime dashboard in elastic stack
    * based on icmp ( ping )
    * based on http

### Basic Checklist

* Create a linux VM in any  cloud and ssh into it
* Create a ssh key from cloud and importing ssh into cloud from your system
* Concept of Service / Daemon
* Package management – `apt`
* JSON and YAML files
* concept of sudo
* using `vi` or `nano` editor
* Fixing :
    * Post on Slack

### Novice Checklist

* Knowing the problem, log files and read the logs to figure out errors
* Installation steps and configuration steps for any application
* Concept of environmental variables and setting
    * User
    * System

### Expert Checklist

* Understanding system architectures
* System Design fundamentals

### Troubleshooting Beats

* All the elastic componets logs can be viewed using _**journalctl**_ `journalctl -u heartbeat-elastic.service`
* Look into YAML for syntax issues and cloud id and auth for configuration
* Ensure metrics are enabled

![alt text](shots/32.PNG)
![alt text](shots/33.PNG)

### Metric Beat

* This beat collects metrics about system and some predefined applications
* Install metric beat 

    [ Refer Here : https://www.elastic.co/guide/en/beats/metricbeat/8.7/setup-repositories.html#_apt ]

#### Metric Beats to capture metrics

* Enable nginx metrics
    * Navigate to `/etc/metricbeat/modules.d` and rename nginx.yml.disabled to `nginx.yml`
    * Copy the dashboards into bin `sudo cp -r /usr/share/metricbeat/kibana/ /usr/share/metricbeat/bin`
* Now start the metric beat after setting in `metricbeat.yml`
    * cloud.id
    * cloud.auth
    * kibana url
* We have configured all dashboards
    * System Overview :

    ![alt text](shots/34.PNG)

    * Apache Dashboard

    ![alt text](shots/35.PNG)

### Log Analysis

* Every logging mechanism will have levels, most widely adopted levels are
    * _**INFO**_ : This is informational log
    * _**DEBUG**_ : This is informative log
    * _**ERROR**_ : This represents errors
    * _**CRITICAL/FATAL**_ : This represents serious system failures

* Logs are time based information
* In Elastic Stack we have logstash which can extract the logs, transform and load into elastic search for querying / visualizations
* Logstash does the transformations with the help of plugins
    * _**Input plugins**_ : to read from different sources, for input plugins supported by logstash

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/input-plugins.html ]

    * _**Filter plugins**_ : to transform the log, for filter plugins

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/filter-plugins.html ]

    * _**Output plugins**_ : to store the output to different sources, for output plugins

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/output-plugins.html ]

* Installing logstash :

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/installing-logstash.html#_apt ]

* Ideal use case for us

![alt text](shots/36.PNG)

### Logstash

* Let's create a linux VM and explore logstash

#### Logstash pipeline

* Syntax
```
input {}
filter {}
output {}
```
* In input section we can define the datasources from where we process inputs `Extract`
* In filter section we define the transformations `Transform`
* In output section we define the destination `Load`
* The list of inputs is all the installed logstash input plugins and same with other sections

### Activity 1 : Let's create a very basic pipeline which reads input from stdin and displays out to stdout

* Stdin input plugin 

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/plugins-inputs-stdin.html ]

* Stdout output plugin 

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/plugins-outputs-stdout.html ]

* Pipeline
```
input {
    stdin {
    }
}
output {
    stdout {
    }
}
```
* Create a file with above content in `/tmp/first.conf`
cd in `/usr/share/logstash` and execute the following command `sudo ./bin/logstash -f /tmp/first.conf`

![alt text](shots/37.PNG)

* Now let's the codec from rubydebug to json
Edit first.conf with following content and start logstash `sudo ./bin/logstash -f /tmp/first.conf`
```
input {
    stdin {
    }
}
output {
    stdout {
        codec => json
    }
}
```
![alt text](shots/38.PNG)

* Let's add one more output to some file `stdout => codec => rubydebug`
* File output plugin

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/plugins-outputs-file.html ]

```
input {
    stdin {
    }
}
output {
    stdout {
    }
    file {
        path => "/tmp/output%{+YYYY-MM-dd}.txt"
    }
}
```
![alt text](shots/39.PNG)

* Open the file for contents

![alt text](shots/40.PNG)

### Activity 2 : Let's create a pipeline to read the file /tmp/test and display the contents in stdout

* input = file
* output = stdout
```
input {
    file {
        path => ["/tmp/test"]
    }
}
output {
    stdout {

    }
}
```
* Install apache and redirect `/var/log/apache2/access.log` to stdout
```
input {
    file {
        path => ["/var/log/apache2/access.log"]
    }
}
output {
    stdout {

    }
}
```
* Let's try to understand filters
* Grok filter can parse unstructured data into fields 

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html ]

### Grok Patterns

* Open the DevTools in Kibana and then Grok Debugger

![alt text](shots/41.PNG)
![alt text](shots/42.PNG)

* For the grok filter in logstash

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html ]

* For writing your own patterns use Regex 
    [ Refer Here : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Cheatsheet ]

* Let's try to build a simple pattern as shown below

![alt text](shots/43.PNG)
![alt text](shots/44.PNG)
![alt text](shots/45.PNG)
![alt text](shots/46.PNG)
![alt text](shots/47.PNG)

* For Grok debugger

    [ Refer Here : https://grokdebugger.com/ ]

#### Sending logs to elastic cloud

* Overview

![alt text](shots/48.PNG)

* Install apache and filebeat on linux instances 

    [ Refer Here : https://www.elastic.co/guide/en/beats/filebeat/current/setup-repositories.html ]

```
sudo apt update
sudo apt install apache2 -y
```
* Install  logstash on other linux instance 

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/installing-logstash.html ]

#### Configuring filebeats to send apache access logs to logstash

* For basic configuration information

    [  Refer Here : https://www.elastic.co/guide/en/beats/filebeat/current/logstash-output.html ]

* Sending data from logstash to elastic  cloud 

    [ Refer Here : https://www.elastic.co/guide/en/logstash/current/connecting-to-cloud.html ]

* Logstash pipeline
```
input {
  beats {
    port => 5044
  }
}
filter {
    grok {
        match => { "message" => "%{COMBINEDAPACHELOG}" }
    }

}
output {
    elasticsearch {
        cloud_id => "learningenv:dXMtY2VudHJhbDEuZ2NwLmNsb3VkLmVzLmlvOjQ0MyQxMDg1YTVjOWQyOWY0N2FjODkyNTBmNjY3NjJkYWU3MyRlNDM5MGRmYmJmMzM0MGViODZiMGNhNTg3ODA1MmZkOQ=="
        cloud_auth => "elastic:h22oWprNjqqbEGTKPSvHHpqS"
    }
    file {
        path => /tmp/test.log
    }
}
```
* Create a file called as `apache.conf` in `/etc/logstash/conf.d`
* Enable and start logstash service

![alt text](shots/49.PNG)

* Now configure filebeat to send logs from `/var/log/apache2/access.log` to `logstash`
* To generate artifical traffic we have executed the following script
```
#!/bin/bash
while true; do
        curl 'http://34.219.90.251'
        sleep 2
done
```
* As of now we are getting issue with indexing (storing ) in elastic search
```
[WARN ] 2023-05-19 03:52:25.065 [[main]>worker0] elasticsearch - Could not index event to Elasticsearch. status: 400, action: ["index", {:_id=>nil, :_index=>"apachelog-2023.05.19", :routing=>nil, :pipeline=>"apachelogs"}, {"log"=>{"offset"=>29714, "file"=>{"path"=>"/var/log/apache2/access.log"}}, "message"=>"157.48.143.223 - - [19/May/2023:03:52:15 +0000] \"-\" 408 0 \"-\" \"-\"", "@version"=>"1", "cloud"=>{"machine"=>{"type"=>"t2.medium"}, "account"=>{"id"=>"678879106782"}, "provider"=>"aws", "availability_zone"=>"us-west-2c", "image"=>{"id"=>"ami-0fcf52bcf5db7b003"}, "region"=>"us-west-2", "service"=>{"name"=>"EC2"}, "instance"=>{"id"=>"i-0b27f5e82d459e378"}}, "source"=>{"address"=>"157.48.143.223"}, "input"=>{"type"=>"filestream"}, "timestamp"=>"19/May/2023:03:52:15 +0000", "ecs"=>{"version"=>"8.0.0"}, "http"=>{"response"=>{"status_code"=>408, "body"=>{"bytes"=>0}}}, "@timestamp"=>2023-05-19T03:52:23.879Z, "event"=>{"original"=>"157.48.143.223 - - [19/May/2023:03:52:15 +0000] \"-\" 408 0 \"-\" \"-\""}, "host"=>{"id"=>"b9e46fc917bf4bc080ee389c0cef33ad", "name"=>"ip-172-31-10-238", "containerized"=>false, "hostname"=>"ip-172-31-10-238", "os"=>{"name"=>"Ubuntu", "codename"=>"jammy", "version"=>"22.04.2 LTS (Jammy Jellyfish)", "platform"=>"ubuntu", "kernel"=>"5.15.0-1031-aws", "type"=>"linux", "family"=>"debian"}, "architecture"=>"x86_64", "ip"=>["172.31.10.238", "fe80::8ef:a7ff:fe5a:5c85"], "mac"=>["0A-EF-A7-5A-5C-85"]}, "tags"=>["beats_input_codec_plain_applied"], "agent"=>{"id"=>"130803ea-47c3-46d3-aad8-8ba6449baff2", "name"=>"ip-172-31-10-238", "version"=>"8.7.1", "ephemeral_id"=>"1b68db3e-0975-4e11-a939-83d1318ed448", "type"=>"filebeat"}}], response: {"index"=>{"_index"=>"apachelog-2023.05.19", "_id"=>nil, "status"=>400, "error"=>{"type"=>"illegal_argument_exception", "reason"=>"pipeline with id [apachelogs] does not exist"}}}
[INFO ] 2023-05-19 03:52:25.066 [[main]>worker0] file - Opening file {:path=>"/tmp/test.log"}
```

### Fixing logstash issue with elastic cloud

* We had issue with pipeline id, removed the pipeline field
* Restarted all the services and executing requests from a script
* So filebeat reads the logs and sends to logstash, logstash breaks the message into multiple fields and stores in elastic search with index name `apachelog-*`
* Now create a data view from kibana

![alt text](shots/50.PNG)
![alt text](shots/51.PNG)

* We were able to search logs by writing simple queries and create pie charts, line charts, metric etc

### Tracing a java application

* Installing sample application
    * openjdk 11
    ```
    sudo apt update
    sudo apt install openjdk-11-jdk -y
    ```
    * Download the jar file 
    
    [ Refer Here : https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/spring-petclinic-2.4.2.jar ]

* Open APM

![alt text](shots/52.PNG)
![alt text](shots/53.PNG)
![alt text](shots/54.PNG)

* Java app tracing

![alt text](shots/55.PNG)

* Download apm-agent jar `wget https://oss.sonatype.org/service/local/repositories/releases/content/co/elastic/apm/elastic-apm-agent/1.38.0/elastic-apm-agent-1.38.0.jar`
* We have run the app with following args
```
java -javaagent:elastic-apm-agent-1.38.0.jar \
-Delastic.apm.service_name=pet-clinic \
-Delastic.apm.secret_token=uu0Dl9Q09RFfMdq86p \
-Delastic.apm.server_url=https://eff6e04ad9d6425fa3492b1a56f794a3.apm.us-central1.gcp.cloud.es.io:443 \
-Delastic.apm.environment=dev \
-Delastic.apm.application_packages=org.spring \
-jar spring-petclinic-2.4.2.jar
```
* Use the application and launch apm

![alt text](shots/56.PNG)
![alt text](shots/57.PNG)
![alt text](shots/58.PNG)
![alt text](shots/59.PNG)
![alt text](shots/60.PNG)

### Site Reliability Engineering (SRE)

* These are processes followed by Google to run its production systems 

    [ Refer Here : https://sre.google/books/ ]

![alt text](shots/61.PNG)

* For the article on SRE

    [ Refer Here : https://directdevops.blog/2019/10/22/site-reliability-engineering-overview/ ]

#### Exercises

 1. Make nop commerce observable
 2. Post k8s metrics to elastic cloud



















































