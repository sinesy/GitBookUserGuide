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

* **SonarQube URL** - the SonarQube remote server URL, used by the local Sonar Scanner tool; something like  "http://localhost:9000"
* **SonarQube username/password** - the credentials to use to access to SonarQube remote server
* **Sonar Scanner base dir -** the local server path where Sonar Scanner has been installed
* **Sonar Scanner key -** after SonarQube installation, you have first to create a project within the SonarQube backend for the current Platform app: use a project id equals to the application\_id of the Platform app. During this process, you will generate a key to use later for the Sonar Scanner remote tool: set it here
* **Server side js actions path** - The path where Platform will save all action sources, used by Sonar Scanner to analyze them; something like: "/opt/actions/myapp/"

## Using SonarQube

Once completed these steps, you can start using SonarQube: the next time the App Designer is opened, a new folder will be available in the action detail (for server-side/GAE js actions), where all bugs/smelling code is reported:

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

This grid is shared by ESlint tool too and here are reported all lines of code in the current action which could contain bugs or "smelling code". The columns in this grid are related to:

* Line of code where the issue is located
* Character nr where the issue starts
* Message related to the issue
* Category, i.e. the kind of issue, one of
  * layout
  * problems
  * suggestions
* Type: either a bug or a warning (code smelling)

Again, not always these recommendations are correct: it is possible that SonarQube would classify some lines of code as false positive cases.

In addition, in the actions list grid, the column named "Errors in static analysis" is updated (not refreshed) with the outcome of the analysis:

![](<../../.gitbook/assets/image (21).png>)

More precisely, a green mark is reported in case there are NOT any bugs. In case of warnings only, the mark remains green.

Moreover, an **XML file** (in JUnit format) is generated on the specified folder (see the related app parameter) which can be later used by a continuous integration tool like **Jenkins**.

The analysis carried out by SonarQube cannot be done in real time as for ESlint; consequently, a **scheduled process** must be defined to perform the analysis of all actions: after its execution, the actions list column "Errors in static analysis" is updated.

This is helpful both on&#x20;

* SonarQube side, where the web app can show all metrics and suggestions about the analysis
* Jenkins, to get a CI reporting about the current state of the app, before a delivery.



