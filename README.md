# Allure jenkins fork

A flexible, lightweight multi-language test report tool, with the possibility of adding to the report of additional information such as screenshots, logs and so on.

The fork is intended to solve the size of the report problem. Each report contains all javascript dependencies and static files. The take about 10Mb of disk space. If you have about 100 test runs a day - your disk drive will run out of disk space soon. The problem is that almost all of that 10Mb are Javascripts dependencies and static files, the report data itself takes significantly less than 1Mb. The solution is to move the static files to the Jenkins static contents folder - $Jenkins_Home/userContent


## Set up your Jenkins
Copy the contents of the src/main/webapp.full/ to the $Jenkins_Home/userContent

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
to your organization maven repo.
 

## Use it
In the "Allure Report generation" post build task set the custom report version to the "1.4.5-jencba"
