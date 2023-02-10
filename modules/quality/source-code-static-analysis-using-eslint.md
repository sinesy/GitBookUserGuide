# Source code static analysis using ESlint

ESLint is a **static code analysis tool** for identifying problematic patterns found in JavaScript code.  Rules used to evaluate the source code are configurable, and customized rules can be defined and loaded.&#x20;

ESLint covers both **code quality** and **coding style issues**. ESLint supports current standards of ECMAScript, and experimental syntax from drafts for future standards.&#x20;

It is very important to remember that these kind of tools can generate false positive outcomes, i.e. report source line with bugs or "smelling code" which apparently they are not: it is important to correctly configure the tool (rules) in advance.

## Installation steps

In order to use it, ESlint must be first installed in the same server where Platform resides.

In order to install it, follows these steps:

* with sudo
* prepare a folder where Platform would save all action source code (e.g. /opt/actions/\<myApplicationId> ) and change dir to it
* download NodeJS if not installed locally yet: **curl -sL https://deb.nodesource.com/setup\_17.x | sudo bash -**
* install NodeJS: **sudo apt-get install -y nodejs**
*   install ESlint: **npm init @eslint/config**

    ✔ How would you like to use ESLint? · style

    ✔ What type of modules does your project use? · esm

    ✔ Which framework does your project use? · none

    ✔ Does your project use TypeScript? · No / Yes

    ✔ Where does your code run? · browser

    ✔ How would you like to define a style for your project? · guide

    ✔ Which style guide do you want to follow? · google

    ✔ What format do you want your config file to be in? · JavaScript

    Checking peerDependencies of eslint-config-standard@latest

    The config that you've selected requires the following dependencies:



    eslint-config-standard@latest eslint@^8.0.1 eslint-plugin-import@^2.25.2 eslint-plugin-n@^15.0.0 eslint-plugin-promise@^6.0.0

    ✔ Would you like to install them now? · No / Yes

    ✔ Which package manager do you want to use? · npm


* initialize it: **npm init**
* change ownership of folders/files

## Configuration

Finally, ESlint must be invoked by Platform. In order to do it, you have first to setup a few application parameters available in the QUALITY group,  within the App Designer:

* **ESlint bin path** - the ESlint installation path, including the subfolder "bin", i.e. where the executable command resides; something like  "/opt/actions/myApplicationId/node\_modules/eslint/bin"
* **JUnit XML file path** - the output path where Platform will create XML files in JUnit format, related to the analysis outcome, for each action; something like "opt/xml/myApplicationId/"; these output files can be helpful in an CI/CD environment like Jenkins, which can read this folder to fetch the analysis
* **System commands path** - This path is needed to correctly execute ESlint, which depends on some system commands; something like:  "/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/go/bin"
* **Server side js actions path** - The path where Platform will save all action sources, used by ESlink to analyze them; something like: "/opt/actions/myApplicationId/"

## Using ESlint

Once completed these steps, you can start using ESlint: the next time the App Designer is opened, a new folder will be available in the action detail (for server-side/GAE js actions), where all bugs/smelling code is reported:

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

In this grid are reported all lines of code in the current action which could contain bugs or "smelling code". The columns in this grid are related to:

* Line of code where the issue is located
* Character nr where the issue starts
* Message related to the issue
* Category, i.e. the kind of issue, one of
  * layout
  * problems
  * suggestions
* Type: either a bug or a warning (code smelling)

Again, not always these recommendations are correct: it is possible that ESlink would classify some lines of code as false positive cases.

Each time a developer saves the source code for the action, ESlint is invoked behind the scenes and this list is refreshed.

In addition, in the actions list grid, the column named "Errors in static analysis" is refreshed with the outcome of the analysis:

![](<../../.gitbook/assets/image (2).png>)

More precisely, a green mark is reported in case there are NOT any bugs. In case of warnings only, the mark remains green.

Moreover, an **XML file** (in JUnit format) is generated on the specified folder (see the related app parameter) which can be later used by a continuous integration tool like **Jenkins**.

It is also possibile to **schedule a process** to automatically perform the analysis for all actions, which can be helpful the first time to analyze all already existing actions.\


