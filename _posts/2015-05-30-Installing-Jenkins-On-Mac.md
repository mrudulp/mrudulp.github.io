---
layout: post
title:  "Installing Jenkins on Mac"
date:   2015-05-30 08:00:00
categories: automation_testing iOS continuous_integration jenkins
---

Jenkins is a popular open source Continuous Integration tool.

We look at Jenkins installation on MacOs --

* Install HomeBrew
* Install java
* Install Jenkins

`brew install jenkins`

* Create a copy of plist with *Jenkins* user

    + Make a copy of default plist

    `cp /usr/local/opt/jenkins/homebrew.mxcl.jenkins.plist /usr/local/opt/jenkins/org.jenkins-ci.plist`

    + Add *jenkins* user
    
    `vi /usr/local/opt/jenkins/org.jenkins-ci.plist`

* Now Copy this plist to LaunchDaemons folder.

` sudo cp /usr/local/opt/jenkins/org.jenkins-ci.plist /Library/LaunchDaemons/`

* Load Jenkins plist

`sudo launchctl load -w /Library/LaunchDaemons/org.jenkins-ci.plist`

* Goto browser and type http://localhost:8080
	
	Wow!! you have Jenkins up & running

## Reference:

1.	[Savvyapps](http://savvyapps.com/blog/continuous-integration-ios-jenkins/)

2.	[ShashikantJagtap](http://shashikantjagtap.net/adventures-with-jenkins-macosx-linux/)
 