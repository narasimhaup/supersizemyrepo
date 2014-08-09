supersizemyrepo
===============

A new way to create lots of content in your alfresco repository.

This tool enable you to create (bulk-import-ready) content and metadata for your alfresco repository.


Types of documents created 
-------
<ul>
<li>
MS Word Documents (.doc) </li>
<ul>
<li>Average size of 1024k </li>
<li>Correspondent Meta-Data xml properties files</li>
</ul>

<li>MS Excel Documents(.xls)</li>
<ul>
<li>Average size of 800k </li>
<li>Correspondent Meta-Data xml properties files</li>
</ul>

<li>Pdf documents(.pdf)</li>
<ul>
<li>Average size of 10MB </li>
<li>Correspondent Meta-Data xml properties files</li>
</ul>

<li>MS PowerPoint Presentation Documents(.ppt)</li>
<ul>
<li>Average size of 5MB </li>
<li>Correspondent Meta-Data xml properties files</li>
</ul>

<li>Jpeg images(.jpg)</li>
<ul>
<li>Average size of 2MB </li>
<li>Correspondent Meta-Data xml properties files</li>
</ul>

</ul>

Pre-Requirements
-------
 

<b>1 - Software requirements</b><br/>
<ul>
<li>JDK 1.7 </li>
<li>Apache Maven 3.0.4+</li>
</ul>

<b>2 - Configuration requirements</b><br/><br/>
During the installation of maven, a new file name settings.xml was created. This file is our entry point to the your local maven settings configuration, including the remote maven repositories.
Edit your settings.xml file and update the server’s section including the alfresco server id and your credentials.

Note that the root pom.xml references 2 different repositories : <b>alfresco-private</b>, <b>alfresco-private-snapshots</b> . The id of each repository must match with a server id on your settings.xml (where you specify your credentials for that server).

Section from configuration settings.xml

```xml
...
        <server>
            <id>alfresco-private</id>
            <username>YOUR_USERNAME</username>
            <password>YOUR_PASSWORD</password>
        </server>
        <server>
            <id>alfresco-private-snapshots</id>
            <username>YOUR_USERNAME</username>
            <password>YOUR_PASSWORD</password>
        </server>
        
        <server>
            <id>workdesk-internal</id>
            <username>YOUR_USERNAME</username>
            <password>YOUR_PASSWORD</password>
        </server> 
 ...
```

Section from the root pom.xml maven build file

```xml
...
        <repository>
            <id>alfresco-private</id>
            <url>https://artifacts.alfresco.com/nexus/content/groups/private</url>
        </repository>
        <repository>
            <id>alfresco-private-snapshots</id>
            <url>https://artifacts.alfresco.com/nexus/content/groups/private-snapshots</url>
        </repository>
        
         <repository>
            <id>workdesk-internal</id>
            <url>https://artifacts.alfresco.com/nexus/content/groups/workdesk/</url>
        </repository> 
 ...
```

<b>3 - Location/Path Where to create the files </b><br/><br/>

Edit the src/main/java/super-size-my-repo.properties and configure your deployment location in a place inside 
your contentStore. This will be the root for the in-place bulkImport.


Tool Configuration files and options
-------

You find the tool configuration file under src/main/java/super-size-my-repo.properties
This configuration file contains the following pre-explanatory properties.

```xml
...
       files_deployment_location=<PATH_WHERE_THE_FILES_WILL_BE_CREATED>
       images_location=<DEFAULT_LOCATION_FOR_BASE_IMAGES>
       num_Threads=<NUMBER_OF_THREADS_TO_EXECUTE>
       threadPoolSize=<SIZE_OF_THE_THREAD_POOL>
 ...
```

The only property that is mandatory to adjust is the files_deployment_location,
All of the other properties have running default values.


How to run with maven ?
-------
Issue the following maven command to run the project from the root

<b>mvn clean install -Prun</b> <br/>

This will build and run all the modules and it's the easiest way to build the project


Next Steps ?
-------
The goal is to execute the in-place-bulk import action to add all the documents and correspondant 
meta-data to a target Alfresco repository

