---
layout: post
title:  "Getting Started With Appium"
date:   2015-05-28 08:00:00
categories: automation_testing iOS
---


## Appium Instructions -- Quick Start

Appium is a framework to do UIAutomation testing on iOS and Android

Here we look at Appium installation on Mac for iOS testing. In this part we look only at *installation and playing* with appium.

We are going to use UICatalog app that is available on [Apple's website](https://developer.apple.com/library/ios/samplecode/UICatalog/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007710-Intro-DontLinkElementID_2). We are dealing with 11.3 version here.

So lets get started --

## Steps to Install on MacOS --
Mac comes with Python and Ruby installed. But I do not recommend using inbuild ruby.

	
* Install RVM(Ruby Version Manager) from [here](https://rvm.io/rvm/install)

	*Only with Ruby* 

	`\curl -sSL https://get.rvm.io | bash -s stable --ruby`
	
* Install [Brew](http://brew.sh) if not installed
	
	`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

* Install Node.js 

	`brew install node`

* Install appium server

	`npm install -g appium`

* Create a custom Gemset *(assumes RVM is installed)*

	`rvm gemset create appium`

* Install Appium gem

	`gem install appium_console`
	
* Verify Installation was successful (You should see appium_console and appium_lib)

	`gem list|grep appium`

* Download [App](https://developer.apple.com/library/ios/samplecode/UICatalog/Introduction/Intro.html#//apple_ref/doc/uid/DTS40007710-Intro-DontLinkElementID_2) (if you havent yet)

### Running with Simulator
* Build app --
	* Goto (working) folder where you will find *.xcodeproj for the UICatalog project.
	* Check the sdks available on the disc by issuing command
	`xcodebuild -showsdks`
	* Build from command line using following commands. (Replace <simulator sdk> with foreg: iphonesimulator8.3)

	`xcodebuild -configuration Release -target UICatalog -arch i386 -sdk <simulator sdk>`
 
* Create appium.txt in your working folder. This file is read by Appium(appium_lib) as input.

	Sample appium.txt showing how to use Appium Server Capabilities [caps](https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/caps.md)
	
	+ `platformName = "iOS"`
	+ `app = "./build/Release-iphonesimulator/UICatalog.app"`
	+ `deviceName = "iPhone Simulator"`

* Start appium server in seperate tab.( I use iTerm for terminal)
 
	`appium`
 
* Start Console

	Goto folder where appium.txt is created. Ensure
 
	`arc`
 
 ### Running with Device
 * Build app --
	
	* Goto (working) folder where you will find *.xcodeproj for the UICatalog project.
	* Check the sdks available on the disc by issuing command
	`xcodebuild -showsdks`
	* Build from command line using following commands. 
		
		Replace
		
		+  <iphone sdk> with foreg: iphoneos8.3
		+  <Dev Certificate Name> with certificate found in keychain foreg: "iPhone Developer: abc(C31234)"
		+  <Provisioning Profile uuid> with provisioning profile found in keychain or use iPhone Configuration Utility foreg: "1234-efgh-ghjr-port"

	`xcodebuild -configuration Release -target UICatalog -sdk <iphone sdk> CODE_SIGN_IDENTITY="<Dev Certificate Name>" PROVISIONING_PROFILE="<Provisioning Profile uuid>"`
 
* Create appium.txt in your working folder. This file is read by Appium(appium_lib) as input.

	Sample appium.txt showing how to use Appium Server Capabilities [caps](https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/caps.md)
	
	+ `platformName = "iOS"`
	+ `app = "./build/Release-iphoneos/UICatalog.app"`
	+ `deviceName = "iPhone"`

* Start appium server in seperate tab.( I use iTerm for terminal)
	
	(find device uuid either using Xcode -> Orgnaniser or using iPhone Configuration Utility)

	`appium -U <device uuid>`
 
* Start Console

	Goto folder where appium.txt is created. Ensure
 
	`arc`

* Exploring Elements --

	1. By Command line -- Refer [here](http://appium.io/slate/en/tutorial/ios.html?ruby#page-command) and [here](https://saucelabs.com/resources/appium-bootcamp/appium-bootcamp-2013-chapter-3-interrogate-your-app)

		We look at only 4 commands

		* Page_class -- This will give bird's eye view of iOS app structure
		
			`page_class`

		* Page Elements (`page`command) -- This will list all elements. Further elements can be explored like by name or by id
			
			+ `page`
			+ `page 'UIAStaticText' `
		
		* Find Elements by name --

			+ `find('Egg Benedict')` (Returns element id)
			+ `find('Egg Benedict').name`(Returns Name Attribute for element)

		* Find Elements by id --
			
			+ `id('Egg').name`
		
		* Ending Session --
		
			+ `x`
	
	2. By Inspector -- Appium also provides with UIInspector. More info can be found [here](http://appium.io/slate/en/tutorial/ios.html?ruby#appium.app-inspector)


## Troubleshooting --

* *.. "`initialize': platformName must be set. Not found in options:"*

	Have a look at your appium.txt. Ensure all parameters are set under quotes.Refer Sample appium.txt [files](https://github.com/mrudulp/iOSSrc/tree/master/autotest/appiumTest/sampleApps/UICatalogObj_Swift/Objective-C/tests/appiumSample)

* "Message: A new session could not be created. (Original error: Could not initialize ideviceinstaller; make sure it is installed and works on your system)"

	Install ideviceinstaller from brew. Usually this is not required since appium is supposed to install that. But if it is still missing --

	`brew install ideviceinstaller`

 
## References

1. [Getting Started Installation Instructions](http://appium.io/getting-started.html)
2. [Brew](http://brew.sh)
3. [RVM](http://rvm.io)
4. [Getting Started, Tutorial](https://saucelabs.com/resources/appium-bootcamp/appium-bootcamp-chapter-1-get-started-with-appium)
5. [Running Tests](https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/running-tests.md)
6. [Running Appium Test](http://appium.io/slate/en/tutorial/ios.html?ruby#running-tests)
7. [Appium Server Capabilities](https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/caps.md)
8. [Appium iOS Commands](https://github.com/appium/ruby_lib/blob/master/docs/ios_docs.md)
