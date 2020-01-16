![](media/rdwd-emheader.png) 

**DATABASE PERFORMANCE MANAGEMENT OF ON-PREMISES & ORACLE CLOUD INFRASTRUCTURE USER MANAGED SYSTEMS using Oracle Enterprise Manager** 
================================================================

In these hands-on lab activities, become familiar with on-premises and cloud database performance management capabilities using Oracle Enterprise Manager Cloud. (VM/BM/ExaCS). 

============================================================

### Contents
In this lab you will go through features in the following functional areas:


#### A. Database Performance Management On-Premises & OCI User Managed DB Systems

- **Lab Activity 1:** Performance Hub

- **Lab Activity 2:** Real-time database operation monitoring

- **Lab Activity 3:** Tuning a SQL in a PDB

#### B. Real Application Testing

- **Lab Activity 4:** SQL Performance Analyzer Optimizer Statistics

- **Lab Activity 5:** Database Workload Replay (optional, time permitting)

Appendix A - Exercise overview and business case


_____________________________________
### **Lab Environment Setup**

What You Need

-   Windows or Mac

-   PuTTY as an SSH client if using Windows

-   Your service instance’s public IP address.

On Windows, you can use PuTTY as an SSH client. PuTTY allows Windows users
to connect to remote systems over the internet using SSH and Telnet. SSH is
supported in PuTTY, provides for a secure shell, and encrypting information
before it's transferred.

1.  Download and install PuTTY.

Go to <http://www.putty.org/> and click the “You can download PuTTY here”
link.

2.  Run the PuTTY program.

On your computer, go to All Programs \> PuTTY \> PuTTY

3.  Select or enter the following information:

-   Category: Session

-   IP address: Your service instance’s public IP address

-   Port: 22

-   Connection type: SSH

![](media/7c9e4d803ae849daa227b6684705964c.jpg)

**Configuring Your Automatic Login**

4.  In the category section, **Click** Connection and then **Select** Data.

5.  As your auto-login username, enter **opc**.

![](media/36164be0029033be6d65f883bbf31713.jpg)

**Adding Your Private Key**

6.  In the category section, **Click** Auth.

7.  **Click** browse and find the private key file that matches your VM’s public
    key. This private key should have a .ppk extension for PuTTy to work.

![](media/df56bc989ad85f9bfad17ddb6ed6038e.jpg)

To save all your settings:

 8. In the category section, **Click** session.

 9.  In the saved sessions section, name your session EM13C-ABC and **Click** Save.

**Connecting to Your VM from a Unix-style System (Mac)**

##### Use the following command to set the file permissions so that only you can read the file:

-   \$ chmod 400 *\<private_key\>*

-   *\<private_key\>* is the full path and name of the file that contains the
    private key associated with the instance you want to access.

    Use the following SSH command to access the instance

-   ssh –i *\<private_key\> opc\@\<public-ip-address\>*

-   *\<public-ip-address\>* is your instance IP address that you retrieved from
    the console.

**Running your Workload**

##### Change to oracle user via sudo

Option 1:
-   \$ sudo su - oracle

-   Change directory to scripts

-   \$ cd scripts

-   Set the environment for the database by running

-   \$ source SALESENV

-   Execute the script 1-db_lab_start.sh as shown below

![](media/c77440e3c5d8049abaed13e85897ad53.jpg)

Option 2:

1. Log into Oracle Enterprise Manager
-   https://*<<your assigned i/p address>>*: 7803/em/login

-   Use the credentials  [sysman/welcome1] to log into Enterprise Manager 

![](media/em13loginscreen.png)

2. Navigate to Enterprise, then Job, then to Library

![](media/emnav.png)

3. Select job name 1-DB_LAB_START, then Click the Submit button

![](media/emjobsubmit.png)

4. Then Click the Submit button on the next screen

![](media/emjobtarget.png)

5. The workload is now started and will take a few minutes before it has fully ramped up.

![](media/emjobconfirmed.png)

# *A. Database Performance Management*


<br>**Lab Activity 1: Performance Hub**
======================================================================

Estimated Time to Complete Use Case: 15 minutes

Business Case

Oracle Enterprise Manager 13c includes the Jet based Performance Hub, a
completely new unified interface for performance monitoring. It is the
single pane of glass view of database performance with access to ASH
Analytics, Real-Time SQL Monitoring and SQL Tuning under the same hood. A
flexible time picker allows the administrator to seamlessly switch between
Real-Time and Historical views of database performance.

In this lab we will use an Oracle Database 18c Container database with few
pluggable databases. You will be logging in as a CDBA.

![](media/61a454d94f190ddedd4541203290c242.jpg)

Figure A: Container database with PDBs



1.  Log into Enterprise Manager:

    *Use the credentials [sysman/welcome1] to log in*

![](media/1876be1823ca17d9ab7e663e128859c4.jpg)

2.  **Click** on the Targets, then Databases. You will be directed to the list of
    Databases in EM.

![](media/9b88b0ba0cefae75a2374d91dcbd4e2e.jpg)


3. Here you will notice different databases listed, such as SALES, HR etc., we will work the sales container database. **Select** the Sales database from the list, this will take you to the DB home page
    for this database

![](media/95063e3082e730e54d957b9ff7575f49.jpg)



![](media/89801010273a62f99a3da10de8bf5c71.jpg)

4.  **Click** on the Containers tab. It is located at the upper right-hand corner of
    the page, underneath the Performance tile. This will show the list of
    pluggable databases in the CDB and their activity



![](media/c6bc11e91d6db9627a146b3e79d0ce19.jpg)



5.  Notice that the PSALES database is the busiest. We focus our attention to this
PDB. Let us now navigate to Performance Hub. **Select** Performance Hub from the Performance Menu and **Click** on ASH Analytics
    and use the sales_system credential name from the database login screen

![](media/e131e1ce965ab5bb248d5439529fc921.jpg)

![](media/d4ec276ea05aceb2ff86f5b7ea71c36e.jpg)


![](media/58e81976fa9957ee57f89139a06c4841.jpg)

6. Make sure to slide the time picker on an area of high usage (e.g., CPU, IO or
Waits). Notice how the corresponding selected time window also changes in the
summary section. You can also resize the slider to entirely cover the time period of your interest. 

    Notice the graph at bottom, it is providing more detailed view of the time window you selected. By Default the wait class dimension is selected. On the right hand side of the graph you have a list of wait classes for the time window you selected (blue for user I/O, green for CPU etc.). Notice how the color changes if you hover over either the menu or the graph to highlight the particular wait class. 
    
    Wait class isn’t the only dimension you can drill into the performance issue by. Let’s say you wanted to identify the SQL that was causing the biggest
performance impact. You can do that by **Clicking** the drop down list and changing
the top dimension from wait class to SQL ID.



7.  **Select** the SQL ID dimension from the list of available dimensions (Under Top
    Dimensions) using the dropdown box that is currently displaying Wait Class.
    Top Dimensions SQL ID

![](media/32b079f89c002058721d0c8a3e41f993.jpg)

8. **Hover** your mouse on top of the SQL (one at the bottom) and you will be able
to see how much activity is consumed by this SQL. Now using the same list of filters select the PDB dimension. Session
Identifiers PDB



![](media/95cce3b331aa85fc893b8eecc9a6c0a6.jpg)

9. What do you see? The chart changes to activity by the different pluggable databases created
in this Container database. **Click** on the ‘PSALES” pluggable database on the
list to add it to the filter by list and drilldown to activity by this PDB
on the same page.



![](media/384fdb12e234cbc0d60df1639079dc3e.jpg)

![](media/07dcb138dcb6773ee6b560681a62ec5f.jpg)

10.  **Click** on the SQL Monitoring Tab

![](media/6e47bf2703c3c1e4adffd39d2202045f.jpg)



11. You can see all the executed SQL during that time along with different
attributes like ‘user’,’Start’,’Ended’ etc. The test next to the \@ sign
indicates the name of the PDB. **Click** on any SQL of your choice (e.g.
6kd5jj7kr8swv)

![](media/533523dca8453a0ce246ac933fdb639c.jpg)

12. It will navigate you to show the details of this particular query. You can see
the plan, parallelism and activity of the query. “Plan Statistics” tab is
selected by default. You can see the plan of this query in graphical mode. In some cases, the Monitored SQL may have aged out and no rows are displayed, in
this case try using the time-picker and pick last 24 hrs. time period to
identify the historical SQL that was monitored. 

13. **Select** “Parallel” tab. This will give details about parallel coordinator and parallel slaves.

14. **Click** on the SQL Text tab. You can see the query text which got executed.

15. **Click** on the activity tab to understand about the activity breakdown for this SQL
    
16. **Click** on “Save” button on top right corner of the page. This will help you
    to save this monitored execution in “.html” format, which you can use it to
    share or to diagnose offline.


<br>**Lab Activity 2: Real-Time Database Operations Monitorings**
======================================================================



#### Environment Details:

The target database is running a load on the sample schema provided via the
Examples (or companion) software accompanying the Oracle database software.
There are other schemas created to simulate specific performance scenarios.

#### Estimated Time to Complete Use Case: 10 minutes


Real-Time Database Operations Monitoring, introduced in Oracle database 12c,
enables an administrator to monitor long running database tasks such as
batch jobs, ETLs etc. as a composite business operation. It tracks the
progress of SQL and PL/SQL queries associated with the business operation
being monitored. Developers and DBAs can define business operations for
monitoring by explicitly specifying the start and end of operation or
implicitly through the use of tags that identify the operation.

Start the Database Operation.

    ssh using a terminal window or putty and log in as oracle. (see Lab Environment section)
    

    Once Logged in perform the following

    [oracle\@em12 \~]\$ cd scripts

    [oracle\@em12 scripts]\$ . ./ SALESENV

    [oracle\@em12 scripts]\$ cd load/frame/queries/awrv [oracle\@em12 awrv]\$
    pwd

    /home/oracle/scripts/load/frame/queries/awrv

1.  Using SQLPlus connect to the sh2 account. [oracle\@em12 awrv]\$ sqlplus
sh2/sh2\@psales. Open the file (!vi DBOP.sql) from the SQL prompt and then review the content of the file.

    At the beginning of the file you will notice how we have tagged the
operation with dbms_sql_monitor.begin_operation and ended it with
dbms_sql_monitor.end_operation

    Now execute the file \@DBOP.sql

2.  You should already be logged on to Enterprise Manager. If you are not,
    please follow the instructions detailed  earlier. Select the Monitored SQL tab.

3.  Review the list of currently executing SQLs are visible click on the
DBOP_DEMO name. This will open the DBOP named DBOP_DEMO.

Note: You may need to scroll down or select “Database operations” from the type
dropdown.

![](media/b10c056370e56dd1286ca1f556118c8f.jpg)

4.  Review the details of the Database Operations.

![](media/a59f28bdd1166978c41e9c9c6a5d9b93.jpg)

5.  Click on the Activity tab. You will see all the activity for this operation.



![](media/1a32fbdd89e519c2b8401e7dd0626890.jpg)


<br>**Lab Activity 3: Tuning a SQL in a PDB**
======================================================================

#### **Environment Details:**

The target database is running a load on the sample schema provided via the
Examples (or companion) software accompanying the Oracle Database software.
There are other schemas created to simulate specific performance scenarios.



#### Lab Assumption: Your environment should have EM13c and a workload running. 

#### Estimated Time to Complete Use Case: 10 minutes



This use case is o show how a pluggable database
administrator can tune queries in a PDB. With a running workload, this
activity will help you  identify a Top SQL and then tune it using SQL Tuning
Advisor. The PDBA will have no access to the Container and their view is
only restricted to the queries running in the PDB assigned to this user.

    Log into Enterprise Manager Cloud Control.

    Please note that you will be using a new URL:
    *https://Your_Assign_IP:7803/em*

    Login: sysman/welcome1

![](media/8e45436e4fa48b9a5bda495da7b0a674.jpg)

1.  Once logged into Enterprise Manager, **Select** Targets, then Databases . **Click** on
    the expand icon on the left and click on the database
    **sales.subnet.vcn.oraclevcn.com**

![](media/63f4072fb3b311db561d2c284bc93ffe.png)

2.  You should now see the Database Home page.

![](media/611d814ca29dfc9f327a7c8159608093.jpg)

3.  From the Performance Menu **Click** on Performance Hub, then ASH Analytics



![](media/ea10a67618855f3e0ce1a5f5c7157d71.jpg)

4.  **Click** on the activity bar for the SQL showing highest activity in the bottom
    left region.

![](media/1530ad41444abf8120ba3a6bce8d9ba1.jpg)

5.  Now schedule the SQL Tuning Advisor by **Clicking** on the **Tune SQL** button.

![](media/4532cfdb72eeef8ade51f86d9974061e.jpg)

6.  Accept the default and **Submit** the SQL tuning Job.

![](media/528d1e6ee4c55f477811c554c2eeff99.jpg)

![](media/8aaa9d1d202302cd87c3870ffe51b956.png)

7.  Once the job completes. You should see the recommendations for either
    creating a profile or an index.



![](media/64e4e02ca8258d7c1fc54bec446b691a.png)

8.  Implement the SQL Profile recommendation. SQL Profiles are a great way of
    tuning a SQL without creating any new objects or making any code changes. 

9. At this point let’s now turn off the load: Change directory to scripts and execute the script *1-db_lab_stop.sh* as shown below

![](media/e032d591c5b1132ac156974c6abbe2f4.jpg)

Alternatively you can use the Enterprise Manager Job Scheduler capability to stop the job.	
1. Navigate to Enterprise, then Job, then to Library

![](media/emjoblibnav.png)

2. Select the job *1-DB_LAB_STOP*

![](media/emjoblabstop.png)

3. And then Submit the job

![](media/emlabstopsubmit.png)

4. When the job is completed, the workload stops

![](media/emlabstopped.png)

This concludes the Database Performance Management lab activity. You can now move on to Real Application Testing lab activity.

# *B. Real Application Testing* 

The objective of this lab section is to provide exercises designed to showcase Real Application Testing capabilities in Oracle Enterprise Manager Cloud
Control 13c and Database 18c.



In this lab you will go through these functional areas:

    SQL Performance Analyzer Optimizer Statistics

    SQL Performance Analyzer Gather Optimizer Statistics Validation

    Consolidated Database Replay

    Replay multiple workloads concurrently against Pluggable Databases in the
    Container Database


<br>**Lab Activity 4: SQL Performance Analyzer Optimizer Statistics**
======================================================================






#### Estimated Time to Complete Use Case: 10 minutes 

In this exercise we need to configure the database to set up optimizer
statistics to be stale. So the first step is to create and submit a job that
will configure the statistics to be stale.

1.  Execute SPA task using optimizer statistics - Login using username and password **sysman/ welcome1**



![](media/6dc92e956b3d9cd7b140a588219ee285.jpg)

2.  Navigate to the Job library, from **Enterprise**, to **Job**, to **Library**

![](media/4037bd7209e67b936206da6f43991120.jpg)

3.  Select SPA_STAT_SETUP and **Click** the **Submit** button

![](media/emspasetup.png)

4. Select OS Command in the Create library Job drop down list **Click** Go

![](media/a04978f5e6e7d3e03d34685c7212f413.jpg)

5. **Click** the **Submit** button 

![](media/spasubmit.png)

6. The job then runs and completes

![](media/emspajobconfirm.png)

7.  Next configure SPA Quick Check. Provide Name: STAT_SETUP **Click** Add in Target section Select
    emcc.marketplace.com Select Tab **Parameters**

![](media/e3bafcbbfdeb0df5f1921db3f6440dea.jpg)

![](media/b67d43eba55ba84b4758e4e02f809851.jpg)

8.  Select Tab **Credentials**, Select **Named**, Select **ORACLE_HOST**, and **Click** Save to Library

![](media/954828645f8ad404b3350faa88ea93b4.jpg)

![](media/339c058ab81443636e69e38f1f46627e.jpg)

9.  Select ‘”STAT_SETUP” Click “Submit”

![](media/f8b8fa1c13413a037468b536860cab66.jpg)



10. The job is now running. Continue with configuring SPA Quick Check. Navigate to Databases: from the menu, **Targets**, then **Databases**

![](media/baa21e15a952e1b090944051c919d47e.jpg)

11. Expand the sales.subnet.vcn.oraclevcn.com database. **Click** on “sales.subnet.vcn.oraclevcn.com_HR” pluggable database

![](media/6273897d2614da4d3babab73299d5bc5.jpg)

12. In sales.subnet.vcn.oraclevcn.com_HR database Navigate to **Performance**, to **SQL**, to **SQL Performance Analyzer Quick Check Setup**

![](media/52d28e53edc6e12a26eefd6df1487d20.jpg)

13.  This is the page where you configure SPA Quick Check. Make sure that the
    selected SQL Tuning Set includes as many SQL statements as possible. If the
    application has specific workloads that are executed during End of Month,
    End of Year or even certain period during the day, then make sure to collect
    the workload in separate SQL Tuning Sets and merge them into a “Total
    Workload Tuning set”

14. In this example we are working with a SQL Tuning Set called PENDING_STATS_WKLD. Select: SQL Tuning Set: PENDING_STATS_WKLD. Select “Comparision Metric”: Buffer Gets **Click** Save.

![](media/dd8e59451bf9d2de14f07592d390da6a.jpg)

15.  Navigate To **Performance** , to **SQL** , to **Optimizer Statistics**

![](media/4e82b571a46f839223bca1f879643bb0.jpg)

16.  **Click** “Gather”

![](media/1e54f21d483e95189477069278b54053.jpg)

17.  Select “Schema”. Check “Validate the impact of statistics on…..” **Click**  “Next”

![](media/1d4b3ee3678078564de13336896fbe34.jpg)

18.  **Click**  “Add”

![](media/07c9dde006c7bc0a1fc804ef62f5cd5a.jpg)

19.  **Click**  “Search”. **Select:** STAT1, STAT2 **Click**  “OK”

![](media/5f8e1b0229f48747aa96998dbbe0aa87.jpg)

20.  **Click**  “Next”

![](media/47d4db96f2a225723e405f06171d2c7d.jpg)

21.  **Click**  “Next”

![](media/a4faddf1878e9f72df40f1bde4e54bdf.jpg)

22.  **Click**  “Submit”

![](media/d2c4f87d66682e3ecbb6b9c62e639281.jpg)

23. In the confirmation section on top, click on the SQL Performance Analyzer
    Task that was started. If you accidentally closed or lost this page, navigate to **DB Target** , then **Performance Menu** ,  then **SQL Performance Analyzer Home** , then **Select** the latest SPA task you just
created at the bottom of the page.

![](media/24fee673a5a32b19e55b92dae376c233.jpg)

24. You now have now a running SQL Performance Analyzer task. Wait until its Last
    Run Status is Completed. **Click**  on “Name”

![](media/d7b97d687f8d9a904ed2e7ee68f5da89.jpg)

25.  As you can see there have been four SQL trials executed. The first two have
    identified SQL statements with plan changes. In the last two trials it is
    only statements with plan changes that have been executed. This will reduce
    the amount of time and resources used in a production system. **Click** on the eyeglasses icon for the second report.

![](media/e74bda3508f98dbfb69f1e9e196d9c01.jpg)

26.  As we can see the majority of our statements had unchanged performance. We
    have a significant improvement but most important to notice is that we have
    no regression. If there had been regression then we have the ability to tune the regressed
statement or use SQL Plan Baselines to remediate the identified regressions.
Note you can also use SQL Tuning Advisor to remediate regressions by
implementing SQL Profile recommendations

![](media/2d5e94962e6a26f9d9442e09870cde04.jpg)



27.  Since this application has used stale statistics for a long period, then it would be good to have new statistics implemented. **Click** on “Publish Object Statistics”

![](media/bfd46716f39ec820e1c9c0c9982d5218.jpg)

28. We can now change statistics for all tables where we have pending
    statistics. For the scope of this exercise we will only change statistics
    for schema STAT1. **Click** the Checkbox for schema STAT1 **Click** Publish

![](media/1d3a02d5d46d720eefbe226143471f2c.jpg)

**Click** “Yes”

![](media/a8dc3af7bcf1c5b473e4f0037dd722a4.jpg)

![](media/e75f7e6b78aafd328d6b57f505245622.jpg)

For publishing statistics for user STAT2 please repeat the task in 3.25

You have now learned how to work with SPA. As you can see there are Guided
Workflows that will help you during your analysis and verify that you can
implement new changes in production with confidence.

Details about newly published statistics can be found if you navigate ‘Schema** , to **Database Object** , to **Tables** , and Select tables for schema ‘STAT1’

<br>**Lab Activity 5: Database Workload Replay** (optional)
======================================================================


#### Replay workloads against Pluggable Databases in the Container Database

Estimated Time to Complete Use Case: 10 minutes. Note this section is optional,
if you have completed the other recommended labs, go through these activities next. Database Replay activities are command line driven as we have seen there are many customers that prefer to use API's and
    not Enterprise Manager natively.



### Scenario ###
You've been asked to add three new indexes for an  application, but before those indexes can be added we want  proof later that the performance in the database improved. Since there are an additional cost to maintain indexes it is
not enough to validate the performance with SQL Performance analyzer only.
Replay will be done against the Container database Sales. The changes need
to be done in the OLTP container against the DWH_TEST schema. The database
version is 18c so the capture is done against a CDB and the replay will also
be done against the CDB.

1.  Create a Replay Task

    You need to connect two sessions to you dedicated host as user OPC using
    the provided SSH key. Use putty or similar to connect to your local
    host. (see section above: Lab Environment Setup)

    **ssh -i [privatekey] opc\@[Your IP]**

    Session 1 and session 2

2.  Connect to user oracle from the OPC: 

    **user sudo su – oracle**

    \*\*\*\*\*\*\*\*  Session 1  \*\*\*\*\*\*\*\*\*

3.  Set Environment variables for sales database

    **. ./sales.env**

4.  Connect to sales database and create indexes. (indexes are already created,
    just need to make them visible)

    **sqlplus system/welcome\@oltp**

    **alter index dwh_test.DESIGN_DEPT_TAB2_IDX1 visible;**

    **alter index dwh_test.DISTRIBUTION_DEPT_TAB2_IDX visible;** 
    
    **alter index dwh_test.OUTLETS_TAB3_IT_IDX visible;**

    **exit**

5.  We have already performed the capture and stored it in
    **/home/oracle/scripts/dbpack/RAT_CAPTURE/DBReplayWorkload_OLTP_CAP_1
    RAT_REPLAY** 
    
    The capture directory should be copied to a Replay directory. In
    a normal situation replay is performed against a test server. This test
    environment is limited so we will only copy the directory to a replay path
    instead

    **cd scripts/dbpack**
    
    **cp -r RAT_CAPTURE/DBReplayWorkload_OLTP_CAP_1 RAT_REPLAY** 
    
    **cd RAT_REPLAY/DBReplayWorkload_OLTP_CAP_1**

6. Connect to as sysdba and grant become user to system on all containers

    **sqlplus sys/welcome1 as sysdba**

    **grant become user to system container=all;**

7. Connect to system create a directory object to locate the capture and
    preprocess the capture

    **connect system/welcome1**

    **CREATE DIRECTORY DBR_REPLAY AS**

    **'/home/oracle/scripts/dbpack/RAT_REPLAY/DBReplayWorkload_OLTP_CAP_1';**

    **exec DBMS_WORKLOAD_REPLAY.PROCESS_CAPTURE (capture_dir =\> 'DBR_REPLAY');**

8. We can now start to replay the workload. Initialize replay will load replay
    metadata created during preprocessing

    **exec DBMS_WORKLOAD_REPLAY.INITIALIZE_REPLAY (replay_name =\> 'REPLAY_1',
    replay_dir =\> 'DBR_REPLAY');**

9. If the replay environment uses different connect strings compared to the
    capture environment then we need to remap connections. Check connect
    strings.

    **select \* from DBA_WORKLOAD_CONNECTION_MAP;**

10. Next, remap connections

    **exec DBMS_WORKLOAD_REPLAY.REMAP_CONNECTION (connection_id =\> 1,
replay_connection =\> 'HR');** 
    
    **exec DBMS_WORKLOAD_REPLAY.REMAP_CONNECTION
(connection_id =\> 2, replay_connection =\> 'OLTP');**
    
    **exec DBMS_WORKLOAD_REPLAY.REMAP_CONNECTION (connection_id =\> 3, replay_connection =\> 'SALES');** 

    **exec DBMS_WORKLOAD_REPLAY.REMAP_CONNECTION (connection_id =\> 4,
replay_connection =\> 'SALES');** 

    **exec DBMS_WORKLOAD_REPLAY.REMAP_CONNECTION (connection_id =\> 5, replay_connection =\> 'PSALES');** 

    **exec DBMS_WORKLOAD_REPLAY.REMAP_CONNECTION (connection_id =\> 6, replay_connection=\> 'SALES');**

14. Now check new settings for connect strings

    **select \* from DBA_WORKLOAD_CONNECTION_MAP;**

15. Prepare the replay by setting replay options. This replay will use default
    synchronization which is time-based synchronization. With this setting we
    honor timing for each individual call the best as possible. If a session
    has slow SQL statements then other sessions will still honor timing but
    they will not wait for the slow session. This can cause higher divergence.
    If divergence is less than 10 % then it should be considered as a good
    replay.

    **exec DBMS_WORKLOAD_REPLAY.PREPARE_REPLAY (synchronization =\> 'TIME');**

### Now switch to session 2. You should already be connected as user oracle ###

13. Set Environment variables for sales database and change to the replay
    directory

    **. ./sales.env**

    **cd scripts/dbpack/RAT_REPLAY/DBReplayWorkload_OLTP_CAP_1**

16. Calibrate the replay and validate how many replay clients that are needed to replay the workload. 

    **wrc mode=calibrate replaydir=/home/oracle/scripts/dbpack/RAT_REPLAY/DBReplayWorkload_OLTP_CAP_1**

    **Note:** Replay clients are the application tier and should not be co-allocated
    with the database due to resource usage. Our recommendation is to place
    replay clients close to the database to avoid delays between
    database and replay clients. This is regardless if the application tier is
    located far away. The reason is that the replay clients communicate with the
    database to know when a certain database call should be replayed and if
    replay clients are located far away it will delay the call and create
    artificial delays during the replay.



\*\*\*\*\*\*\*\*\*\*\*\*\* Calibrate output \*\*\*\*\*\*\*\*\*\*\*\*\*

Workload Replay Client: Release 18.0.0.0.0 - Production on Tue Nov 5
09:43:45 2019 Copyright (c) 1982, 2018, Oracle and/or its affiliates. All
rights reserved.

Report for Workload in:

/home/oracle/scripts/dbpack/RAT_REPLAY/DBReplayWorkload_OLTP_CAP_1

\-----------------------

Recommendation: consider using at least 1 client divided among 1 CPU(s). You will need at least 112 MB of memory per client process. If your machine(s) cannot match that number, consider using more clients.

    Workload Characteristics:

    - max concurrency: 30 sessions

    - total number of sessions: 534

    Assumptions:

    - 1 client process per 100 concurrent sessions

    - 4 client processes per CPU

    - 256 KB of memory cache per concurrent session

    - think time scale = 100

    - connect time scale = 100

    - synchronization = TRUE 
   
17. The workload is relatively small and it needs
   only one replay client so we will start it from this session

    **wrc system/welcome1\@sales mode=replay
    replaydir=/home/oracle/scripts/dbpack/RAT_REPLAY/DBReplayWorkload_OLTP_CAP_1**

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* Session 1  \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

18. You should still be connected in the SQL\*Plus session as used before. From
    this window start the replay

    **Exec DBMS_WORKLOAD_REPLAY.START_REPLAY ();**

19. Monitor the replay in session 2 and when the replay has finished the
    generate replay reports from session 1.

20. When replay has finished import capture AWR data. First create a common user
    as staging schema

    **Create user C\#\#CAP_AWR;** 
    
    **Grant DBA to C\#\#CAP_AWR;**

    **SELECT DBMS_WORKLOAD_CAPTURE.IMPORT_AWR (capture_id =\> 11,staging_schema =\>
'C\#\#CAP_AWR') from dual;**

21. Generate replay report as a text report. This report can also be generated
    in HTML or XML format.

    **Set long 500000** 
    
    **Set linesize 200** 
    
    **Set pagesize 0**

    **Spool replay_report.txt**

    **select dbms_workload_replay.report (replay_id =\> 1, format=\> 'TEXT') from dual;** 
    
    **spool off**

22. Please open the text report with a Linux editor of your choice such as vi
    and look at replay details.

    **!vi replay_report.txt**

23. Can you see if the replay uses more or less database time than the capture?
    Exit the report in vi use “ZZ” and you will return back to SQL\*plus

24. Generate compare period report as HTML report.

    **spool compare_period_report.html** 

    **VAR v_clob CLOB**

    **BEGIN dbms_workload_replay.compare_period_report(replay_id1 =\> 1, replay_id2
=\> null, format =\> DBMS_WORKLOAD_REPLAY.TYPE_HTML, result =\> :v_clob);**

    **END;**

    **/**

    **print v_clob;** 

    **spool off**

    **exit**

25. To be able to read the report it needs to be downloaded change file
    permissions and copy the file to **/tmp chmod 777 compare_period_report.html**

    **cp compare_period_report.html /tmp**

26. Use a scp client to copy the file to your local machine. Open the file in a
    text editor and remove initial lines before first row starting with

    **“\<html lang="en"\>”**

    and trailing lines after last row ending with

    **“\< b\> End of Report. \</b\>**

    **\</body\>**

    **\</html\> “**

27. You can now open the report in a browser and look at SQL statement with
performance improvements and regression.


We have seen how you can use Real Application Testing Database Replay to
validate changes that may impact performance on both SQL statements and DML
statements. We have also seen the extensive reporting that will help you find
and analyze bottlenecks or peaks during certain workloads. 

# Appendix A. - Database Performance Overview and Business Cases #

## Oracle Enterprise Manager Express

Oracle Enterprise Manager Express (or simply
EM Express) was introduced in Oracle Database 12c. It is web based GUI tool optimized for performance Management. EM
Express is extremely light weight and is built inside the database so it
doesn’t require any additional install. With only a 20 MB disk footprint,
there is no resource usage when it is not invoked or used. You can use
Oracle Enterprise Manager Express to manage a single database while Cloud
Control can be used to manage many databases and targets.

Oracle Enterprise Manager Database Express includes Performance Hub, a unified interface for performance monitoring. It is the
single pane of glass view of database performance with access to ADDM, SQL
Tuning, Real-Time SQL Monitoring and ASH Analytics under the same hood. A
flexible time picker allows the administrator to seamlessly switch between
Real-Time and Historical views of database performance. For Oracle RAC
databases, there is an additional RAC tab that enables the database
administrator to monitor cluster related performance problems.

Diagnosing a slowly performing system or a sudden degradation in performance
is a time consuming task and often the activity where the DBAs spend most of
their time. A major component of the challenge is to simply identify what is
causing the problem in our increasingly complex business environments. There
is a need to sample the current state of all the sessions that are active in
our systems, but analyzing this data for transient problems that occur for
very short durations is not simple. EM Express allows the administrator to
rollup, drilldown, and slice or dice performance data across various
performance dimensions that are captured along with the session state. With
the ability to create filters on various dimensions, identifying performance
issues has never been easier.



When gathering new statistics, it is not uncommon that the new statistics
cause the optimizer to choose a new query plan. In most cases the new plan
will be more efficient but sometimes it causes query regression. As a DBA it is important to proactively predict how new statistics will
change the overall performance in the database. With SQL Performance
Analyzer (SPA) you have the ability to execute most of your SQL statements
that occur in your database.

We have the ability to gather production SQL statements into SQL Tuning Sets
either incrementally from Cursor Cache or AWR history for the period of time
that we want to test. For the purpose of the lab, we have one pre- created
SQL Tuning Set which is representative of the peak workload of this
application. We have also gathered statistics in pending mode for
validation. So, let’s see if the new statistics will change the performance
for this application.

#### SQL Performance Analyzer Optimizer Statistics Workflow 

In this activity you will use the SPA guided workflow for Optimizer
Statistics validation, tune regressed statements and implement
pending statistics on tables.

This activity will be done against a pluggable database, DW, in a container
database ‘test’.

The condition is that we have a warehouse based on 2 schemas ‘STAT1’ and
‘STAT2’. The warehouse has been populated and used for a couple of month and
we have currently not updated the statistics. We want to make sure that when
we publish new statistics then we would not be surprised with a performance
regression.

Some of the activities that are associated with this exercise are time
consuming so we have performed those tasks in advance for lab purposes to
save some time. The following task has already been executed in the setup of
the environment:

-   Gather Pending Optimizer Statistics on schema STAT1 and STAT2

Steps that we are going to perform in this exercise:

-   Run SPA Optimizer Statistics workflow

-   Compare performance of current statistics and pending statistics

-   Use SQL Plan base lines to fix plan regressions

-   Run SPA Optimizer Statistics workflow validate implemented SQL Plan Base
    lines

-   Compare performance of current statistics and pending statistics + SQL Plan
    Baselines implemented

-   Implement (Publish) new statistics

## Database Replay ##


During changes that can have impact on performance it is important to know that
the server will handle all workloads. On this front we have the Database Replay
feature that will help us to predict the workload behavior. We can test
different scenarios to make sure that we are as much prepared as possible.
Examples of scenarios to test could be:

-   Worst case scenario during peaks.

-   Growing user activity

In this use case we are going to replay a workload that has been pre-captured.
For the purpose of the lab, we’ve already setup the test system and the
Container database appropriately to the point-in-time of captures so that replay
can be started.

Lab Overview



To perform real-world testing of Oracle databases, by capturing production
workloads and replaying them on test systems enables you to perform real-world
testing quickly and accurately. This allows enterprises to assess the impact of
any planned system change before deploying it on production reliably.
Additionally, with Oracle Database 12c and beyond we have the Multitenant
capability that will make it possible to consolidate application into different
pluggable databases within one container database. This allows us to reduce the
footprint of each database and reduce resource usage on the server.

That concludes this lab.

>   [Return back to top menu listing all available labs](../readme.md)