# Source code static analysis using ESlint

ESLint is a **static code analysis tool** for identifying problematic patterns found in JavaScript code.  Rules used to evaluate the source code are configurable, and customized rules can be defined and loaded.&#x20;

ESLint covers both **code quality** and **coding style issues**. ESLint supports current standards of ECMAScript, and experimental syntax from drafts for future standards.&#x20;

It is very important to remember that these kind of tools can generate false positive outcomes, i.e. report source line with bugs or "smelling code" which apparently they are not: it is important to correctly configure the tool (rules) in advance.

## Installation steps

In order to use it, ESlint must be first installed in the same server where Platform resides.

In order to install it, follows these steps:

* download NodeJS if not installed locally yet: **curl -sL https://deb.nodesource.com/setup\_17.x | sudo bash -**
* install NodeJS: **sudo apt-get install -y nodejs**
* install ESlint: **npm init @eslint/config**
* initialize it: **npm init**
* change ownership of folders/files

## Configuration

Finally, ESlint must be invoked by Platform. In order to do it, you have first to setup a few application parameters within the App Designer:

* **ESlint bin path** - the ESlint installation path, including the subfolder "bin", i.e. where the executable command resides; something like  "/opt/eslint/node\_modules/eslint/bin"
* **JUnit XML file path** - the output path where Platform will create XML files in JUnit format, related to the analysis outcome, for each action; something like "opt/xml/myapp/"; these output files can be helpful in an CI/CD environment like Jenkins, which can read this folder to fetch the analysis
* **System commands path** - This path is needed to correctly execute ESlint, which depends on some system commands; something like:  "/usr/local/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/go/bin"
* **Server side js actions path** - The path where Platform will save all action sources, used by ESlink to analyze them; something like: "/opt/actions/myapp/"



\


