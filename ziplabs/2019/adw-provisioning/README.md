---
layout: ziplab
description: Learn how to provision and get started with Oracle Autonomous Data Warehouse.
tags: Oracle Cloud, Autonomous Data Warehouse, ADW, Oracle Cloud Infrastructure, OCI
permalink: /ziplabs/2019/adw-provisioning/index.html
---
# Provisioning Autonomous Data Warehouse #

## Before You Begin ##
This 10-minute lab walks you through the steps to get started using the Oracle Autonomous Data Warehouse (ADW) on Oracle Cloud Infrastructure (OCI). You will provision a new ADW database. Later labs show you how to connect and query the database with SQL Developer Web, and use other services.

### Background ###
Autonomous Data Warehouse is built around the market leading Oracle database and comes with fully automated data warehouse specific features that deliver outstanding query performance.  This environment is delivered as a fully managed cloud service running on optimized high-end Oracle hardware systems.  You don’t need to spend time thinking about how you should store your data, when or how to back it up or how to tune your queries.  We take care of everything for you.  You can select the exact combination of storage and CPUs to fit your project and your budget. We keep all of your data safe and secure.  It’s always backed up and always encrypted in Oracle’s cloud.  Using our client tools you load all kinds of different types of data from worksheets on your computer, webstore log files to data files stored in Oracle’s cloud-based object store and load that data into your Autonomous Data Warehouse.

Oracle’s Autonomous Data Warehouse is the perfect quick-start service for fast data loading and sophisticated data reporting and analysis.  Oracle manages everything for you so you can focus on your data.

### What Do You Need? ###
* Access to an instance of Oracle Autonomous Data Warehouse Cloud


## Create an ADW Instance ##
1. Sign in to the Oracle Cloud Platform. 
2. Click the menu icon to expand the menu on the left edge of the screen.
3. Click **Autonomous Date Warehouse**.

    ![](img/OCIMenu.png)

    [Description of the illustration OCIMenu.png](files/OCIMenu.txt)

4. Click the **Create Autonomous Database** button to start the instance creation process.
5. On the Create Autonomous Database page, enter the following information:
     * **Compartment**: For this lab, we'll use the `root` compartment.
     * **Display Name**: `ADW Finance Mart`
     * **Database Name**: `ADWFINANCE`
     * **Workload Type**: `Data Warehouse`
     * **CPU Core Count**: `1`
     * **Storage (TB)**:  `1`
     * **Auto Scaling**: Unchecked
     * **Administrator Credentials**: Create a password for the ADMIN user of the service instance. Remeber this password! You'll need it later to sign in to various services.
     * **License Type**: `Bring Your Own License`
6. Click the **Create Autonomous Database** button to start provisioning the instance. 
7. You're taken to the instance's details page. Details include a State field, which indicates the instance is **Provisioning**. When it's complete, the State field changes from **Provisioning** to **Available**. If the status doesn't change after few minutes, try refreshing the page.

    ![](img/adw_provisioning_state.png)

    [Description of the illustration adw_provisioning_state.png](files/adw_provisioning_state.txt)


## Want to Learn More? ##
* [Autonomous Cloud Platform Courses](https://learn.oracle.com/pls/web_prod-plq-dad/dl4_pages.getpage?page=dl4homepage&get_params=offering:35573#filtersGroup1=&filtersGroup2=.f667&filtersGroup3=&filtersGroup4=&filtersGroup5=&filtersSearch=) from Oracle University 
* [Autonomous Data Warehouse Cloud Certification](https://education.oracle.com/en/data-management/autonomous-database/product_817?certPage=true) from Oracle University
* [ADW Test Drive Workshop](https://oracle.github.io/learning-library/workshops/journey4-adwc/?page=README.md)


