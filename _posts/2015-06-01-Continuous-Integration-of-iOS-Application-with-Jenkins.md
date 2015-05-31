---
layout: post
title:  "Continuous Integration of iOS Application with Jenkins."
date:   2015-06-01 08:00:00
categories: automation_testing iOS continuous_integration jenkins
---

# Continuous Integration of iOS Application with Jenkins.

We are going to look at Continuous Integration of iOS Application with Jenkins CI. We are going to use Appium for Test Automation and Robot Framework to write the tests.

These instructions were written for 1.6.614 version of Jenkins

## Installation

* We will install [Jenkins on Mac](#Link??)
* Appium Installation *Todo*
* Robot Installation *Todo*
 
## Configuration

Now we configure Jenkins. We first look at plugins to be used --

### Security

Before you start doing anything on Jenkins, you would need to enable Security. Please follow these steps carefully otherwise you will lock out Jenkins

* Enable Security ( Do not save yet)
* Now Under **Security Realm** select *Jenkins own* database
* Check "Allow users" to sign up
* Under **Authorization** select *Matrix-based* security
* Add a user(say "admin") and check all the permissions
* Remove all permissions for anonymous user
* Now Save
* Come back and signup with user "admin".

Now your security is setup and you are good to go.

### Plugins

#### Git Integration

* Install [Github Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Github+Plugin) (These instructions are valid for 1.11.3 version) 

	+ It will bring Other plugins such as Git,github-api plugin, etc...

* Now configure System for Github Integration

	+ Go to Manage System -> Configure System
	+ Verify under **Git Section** or "Git installations" it shows Git executable. If installation paths are not found it will show red mark next to the git path
	+ Goto Github Web hook section
		- Select "Let Jenkins auto-manage hook URLs"
		- Add username and OAuth token ( For generating OAuth token refer [Github instructions](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)
		- Test credentials. If it works you are good to go.

## Creating our First Job

* Click *"New Item"*
* Select *"Free-Style"*
* Enter Name for the Job **without spaces**

## Troubleshooting

1. Locked out Jenkins as a result of Security enabling
    * Look for config.xml and disable security from *true* to *false*. Also delete all 3 subsequent lines on security
    * config.xml can be either in `/var/lib/jenkins/config.xml` or `~/.jenkins/config.xml` path
	

## References:

1. [OrangeJuice Setting up Jenkins](http://orangejuiceliberationfront.com/setting-up-jenkins-for-github-and-xcode-with-nightlies/)
2. [Generating OAuth Tokens on github](https://help.github.com/articles/creating-an-access-token-for-command-line-use/)