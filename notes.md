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