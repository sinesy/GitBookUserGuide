# Source code static analysis using SonarQube

SonarQube is an open-source platform developed by SonarSource for continuous inspection of code quality to perform automatic reviews with static analysis of code to **detect bugs** and **code smells**. SonarQube offers reports on duplicated code, coding standards, unit tests, code coverage, code complexity, comments, bugs, and security recommendations.

SonarQube can record metrics history and provides evolution graphs. SonarQube provides fully automated analysis and continuous integration tools like Jenkins.

It is very important to remember that these kind of tools can generate false positive outcomes, i.e. report source line with bugs or "smelling code" which apparently they are not: it is important to correctly configure the tool (rules) in advance.

## Installation steps

In order to use it, SonarQube must be first installed somewhere. It is not essential to install it where a Platform installation resides, since there is a second remote component, named Sonar Scanner, to install where Platform server resides, which can analyze the source code and communicate with the SonarQuebe central instance. Consequently, SonarQube can serve multiple applications.&#x20;

In order to install it, follows these steps:

*   Download the .zip image of SonarQube Community Edition:

    [https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.0.65466.zip](https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.0.65466.zip)
* Create a folder where decompressing the .zip file (e.g. /opt/sonarqube)
* Change the ownership for the folder and subfolders: chown platform:platform -R \*
* set an env variable: export SONAR\_JAVA\_PATH=pathtojdk11/bin/java
* create a service for the starting command: /opt/sonarqube/bin/linux-x86-64/sonar.sh start

The remote agent to install where Platform server resides must be first downloaded and then installed, following these steps:

*   Download Sonar Scanner:

    [https://docs.sonarqube.org/latest/analyzing-source-code/scanners/sonarscanner/](https://docs.sonarqube.org/latest/analyzing-source-code/scanners/sonarscanner/)&#x20;
* Create the folder when uncompressing the .zip file (e.g. /opt/sonarscanner)
*   Change the ownership to the folder and subfolders: chown platform:platform -R \*

    \


## Configuration

Finally, SonarQube must be invoked by Platform. In order to do it, you have first to setup a few application parameters available in the QUALITY group, within the App Designer:

* **ESlint bin path** - the ESlint installation path, including the subfolder "bin", i.e. where the executable command resides; something like  "/opt/eslint/node\_modules/eslint/bin"
* **JUnit XML file path** - the output path where Platform will create XML files in JUnit format, related to the analysis outcome, for each action; something like "opt/xml/myapp/"; these output files can be helpful in an CI/CD environment like Jenkins, which can read this folder to fetch the analysis
* **System commands path** - This path is needed to correctly execute ESlint, which depends on some system commands; something like:  "/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/go/bin"
* **Server side js actions path** - The path where Platform will save all action sources, used by ESlink to analyze them; something like: "/opt/actions/myapp/"
