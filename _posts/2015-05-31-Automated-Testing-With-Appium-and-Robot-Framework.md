---
layout: post
title:  "Automated Testing With Appium and Robot Framework"
date:   2015-05-31 08:00:00
categories: automation_testing iOS
---

# Automated Testing With Appium and Robot Framework

## Installation

(These instructions assume python is installed. This was tested with Mac so, they might vary for other OS)

1. Install Appium. For Detailed [Instructions]({%post_url 2015-05-28-Getting-Started-With-Appium %})
2. Install pip for Python. [Instructions](https://pip.pypa.io/en/latest/installing.html)
3. Install Robot. For Detailed [Instructions](http://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html#installation-instructions)
	`pip install robotframework`
4. Install [Appium Library](https://github.com/jollychang/robotframework-appiumlibrary) from the link or use the following command.

	`pip install robotframework-appiumlibrary`
 

## Keyword Reference

[Appium Library](jollychang.github.io/robotframework-appiumlibrary/doc/AppimuLibrary.html)

## Writing our first TestCase

We are going to use UICatalog app that is available on [Apple's website](https://developer.apple.com/library/ios/samplecode/UICatalog/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007710-Intro-DontLinkElementID_2). We are dealing with 11.3 version here.

1. Compile UICatalog.app with either Xcode or commandline

>For commandline, Command is --
`xcodebuild -configuration ${BUILD_TYPE} -target ${TARGET_NAME} -arch ${CPU_ARCHITECTURE} -sdk ${SIMULATOR_OR_IOS_SDK}`
where --

>* `{Build_Type}` -- `Release` or `Debug`
* `{Target_Name}`-- <Your Target>
* `{CPU_ARCHITECTURE}`-- `i386` for Simulator, `armv6` or `armv7` for Devices
* `SIMULATOR_OR_IOS_SDK`-- Essentially looking for `iPhone` or `iPhoneSimulator`

So our commands would look like --

* `cd <UICatalog folder containing *.xcodeproj file>`
* `rm -rf build` (Assuming you have build folder)
*  if you are building for Simulator `xcodebuild -configuration Release -target UICatalog -arch i386 -sdk iphonesimulator8.2`
*  Or if you are building for iPhone 
	+ With Keys (In my case Found under *KeyChains ->Login->My Certificates*) -- `xcodebuild -configuration Release -target UICatalog -arch armv7 -sdk iphoneos8.2 CODE_SIGN_IDENTITY="iPhone Developer: user"`
		You may need to allow access to keys which is done by
		* Right clicking Certificate->GetInfo->"Always Trust"
		* Right clicking Key->GetInfo->Access Control -> "Allow all applications to ..."
	+ With Provision Profile(Found under *~/Library/MobileDevice/Provisioning\ Profiles/* -- `xcodebuild -configuration Release -target UICatalog -arch armv7 -sdk iphoneos8.2 PROVISIONING_PROFILE="<uuid>"`
* `ls build/Release-iphonesimulator/` (To List UICatalog.app)

2. Create a Robot file
	
	Robot files contain Settings, Variables, Keywords and TestCases. Some keywords are already [predefined](http://jollychang.github.io/robotframework-appiumlibrary/doc/AppimuLibrary.html) by the plugin. Rest we need to define them. You can see them in the Sample File.
	We are going to do following Testcases -
	* Open Application
	* Check Element Exists
	* Check Element with Text Exists
	* Click the Element
	* Scroll in the list
	* Put application to Background
	* Close the application
	* Close any other application.
	
	(Last two Test cases are important to ensure Appium closes the session properly)
	You can find the sample file [here](#Sample File Link)
	


## Reference --

1. [Robot Appium Plugin](https://github.com/jollychang/robotframework-appiumlibrary)
2. [XCode Build SO Link](http://stackoverflow.com/questions/5010062/xcodebuild-simulator-or-device)