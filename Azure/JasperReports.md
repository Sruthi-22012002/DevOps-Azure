<div align ="center"><h2>JasperReports® Server</h2></div>

 ## Introduction
* JasperReports® Server builds on the `JasperReports® Library` as part of a comprehensive family of Business Intelligence (BI) products`, providing robust static and interactive reporting, reportserver, and data analysis capabilities.
* These capabilities are available as either stand-alone(only one tool) products, or as part of an integrated end-to-end BI suite(all tools together).
* The products utilize common metadata(common data definitions) and provide shared services, such as security, a repository, and scheduling.
* This enables seamless integration with other applications and the capability to add custom functionality with ease.

### `The heart of the Jaspersoft® BI Suite is the JasperReports server`, which provides the ability to:
 * Easily create reports based on views designed in an intuitive, web-based, drag and drop tool(Ad Hoc Editor).
 * Efficiently and securely manage many reports.
 * Interact with reports, including sorting, changing formatting, entering parameters, and drilling on data.
 * Schedule reports for distribution through email and storage in the repository.
 * Combine reports and visual elements to create interactive dashboards that clearly show business trends.

## JasperReports Server Distributions
> JasperReports Server is a web application that runs in an app server and uses an external database to store its repository.

JasperReports Server is available in two distributions: a **binary installer** for evaluation and a **WAR file** for production.
### Binary Installer
* The `binary installer` is an executable file that includes the **Tomcat application server and PostgreSQL database** so that it is fully self-contained.
*  The installer software leads you through the options and installs Tomcat and PostgreSQL with default settings for JasperReports Server to use.
*  The binary installer runs on desktops and laptops under Linux, MacOS, and Windows (64-bit), so you can quickly install an instance of JasperReports Server and explore all of its features.
### WAR file
* The WAR (web archive) file is a zipped file containing only the JasperReports Server web app.
* To install the WAR file in production, you must first install and configure one of the supported app servers (for example Tomcat, JBoss, WebLogic, or Websphere) and one of the supported databases (most major relational databases)
* The WAR file distribution includes scripts that you edit to specify your app server and database.
* When you run these scripts, they create the necessary tables in your database and copy the files of the web app to your app server.
 > To install TIBCO(is the company that owns and develops JasperReports Server) for enterprise production environments, use the **stand-alone WAR file distribution**, which is the official TIBCO JasperReports Server installer.

#### Download 
[Jaspersoft](https://www.jaspersoft.com/support) -> Products -> community edition -> Download Now

![image](https://github.com/user-attachments/assets/3c96649e-f0fb-4d3b-8a93-439a5c732fd1)

## System Requirements
 The following table contains the minimum and recommended resources for a full installation that includes PostgreSQL and an application server.
 
 ![image](https://github.com/user-attachments/assets/70f26645-eb22-46d0-8c05-7390c6748b63)

##  Installation Types
 As of version 8.0, JasperReports Server supports the following installations:
 * **Compact installation:** The Repository, Audit, Access, and Monitoring tables are created in a single repository database. This is the same configuration as previous versions.
> The Access and Audit events are now processed asynchronously using a thread pool. The default installation is the Compact installation.

 * **Split installation:** Only the Repository tables are created in the repository database. The Audit, Access, and Monitoring tables are created in a separate audit database.
> The binaryinstaller does not support split installation. For split installation, use the stand-alone WAR file distribution, which is the official JasperReports Server installer

