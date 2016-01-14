# Allure standalone static files fork


The fork is intended to solve the size of the report problem. Each report contains all javascript dependencies and static files. The take about 10Mb of disk space. If you have about 100 test runs a day - your disk drive will run out of disk space soon. The problem is that almost all of that 10Mb are Javascripts dependencies and static files, the report data itself takes significantly less than 1Mb. The solution is to move the static files to the webroot folder of your webserver. You can then place a report to any folder of your server. 


## Set up your Server
Copy the contents of the src/main/webapp.full/ to the webroot folder of your web server

## Build and deploy the artifacts
The allure-report-face depends on 
 * allure-report-data
 * allure-model
 * allure-commons
 
You will need to deploy all these artifact on your organization's maven repository to make the custom version report generation work.

Just build the the allure-core by __mvn install -DskipTests=true__ command. It will build and deploy the artifacts to you local maven repository. And then you need manually deploy 
 * allure-report-data
 * allure-model
 * allure-commons
 * allure-report-face
 
to your organization's maven repo.
 

## Use it
#### Step 1
add reporting section to your pom.xml file: 
````xml
    <reporting>
        <excludeDefaults>true</excludeDefaults>
        <plugins>
            <plugin>
                <groupId>ru.yandex.qatools.allure</groupId>
                <artifactId>allure-maven-plugin</artifactId>
                <version>2.2</version>
                <configuration>
                    <resultsPattern>target/allure-results</resultsPattern>
                    <reportVersion>1.4.5-sbt-lp</reportVersion>
                </configuration>
            </plugin>
        </plugins>
    </reporting>
````
#### Step 2
Generate report
__mvn site__
The report is generated in the target\site folder

#### Step 3
You can also automatically deploy the report to your webserver server using __mvn site:deploy__ command. You need to configure     distributionManagement block in your pom.xml to make site:deploy target work



