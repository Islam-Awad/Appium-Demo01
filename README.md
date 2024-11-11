
# Appium + WebDriver.IO Demo Framework - Android & IOS Example

This project has been created to demonstrate how a QA Engineer can perform Mobile Testing using Appium + WebDriver.IO
More commands and insights about the integration at WebDriverIO Appium 

## Android Setup
#### Android Studio & ANDROID_HOME variable

Tested the following steps on MAC OS Monterrey:
* Android studio on Mac can be located at:
```bash
```
* We need to add a reference to a couple of folders inside of that SDK
   * Tools & Platform Tools
* Open the zshenv file to insert the ANDROID_HOME variable (i):
```bash
  
```
* Enter the environment variables and save the vim session (:wq!):
```bash
    
* Source and apply the changes in the system:
```bash
    source ~/.zshenv
```
* You can check if it was set correctly running the command:
```bash
    echo $ANDROID_HOME
```
* It should return something like: 
```bash
    /Users/[USER]/Library/Android/sdk

- - -


#### Download Appium Inspector
In order to find the correct locators to map elements, you will need to have this tool installed in your computer.

For this project you can use the following configuration:

| Server Key | Server Value |
| ------------- | ------------- |
| Remote Host | 0.0.0.0 |
| Remote Port | 4723 |
| Remote Path | / |

Android Desired Capabilities(Example)
| Desired Capability Key  | Desired Capability Value |
| ------------- | ------------- |
| platformName  | Android |
| platformVersion  | [OS VERSION / IMAGE]  |
| deviceName | [EMULATED_DEVICE_NAME] | 
| app | /[PROJECT_PATH]/[APP_NAME].apk |
| appium:automationName | UIAutomator2 |

IOS Desired Capabilities(Emulator - App)
| Desired Capability Key  | Desired Capability Value |
| ------------- | ------------- |
| platformName  | IOS |
| platformVersion  | [OS VERSION / IMAGE]  |
| deviceName | [EMULATED_DEVICE_NAME] | 
| app | /[PROJECT_PATH]/[APP_NAME].app |
| appium:automationName | XCUItest |

#### Install Apium 
Appium is an open source test automation framework for use with native, hybrid and mobile web apps. 
It drives iOS, Android, and Windows apps using the WebDriver protocol.

    npm install -g appium@next
```
Check the appium version using
```bash
    appium -v
```

#### Appium Doctor

Install it using the command 
```bash 
npm install appium-doctor -g
```
And then use the library:
```bash 
appium-doctor
```

#### Appium drivers
If you want Appium to work correctly, you need to download and have the android/ios driver in your system.
Run the commands:
```bash 
appium driver install xcuitest
appium driver install uiautomator2
```
Check the installed drivers using
```bash 
appium driver list
```


## Setup WebDriverIO

1- Run the command to create the package.json & continue with the installation process
```bash
    npm init wdio .
```
2- Using the WDIO Configuration Helper select the options you want to select. In my case I decided to use:  
* On my local machine
* Mocha
* No compiler
* Spect Location: Default
* Do you want WebDriverIO to generate some test files?: No
* Reporter: Spec
* No Plugin 
* Service: Appium
* Base URL: Default
* NPM Install: Yes

3- Add your tests at 
```bash
'./[yourProject]/specs/**/*.js'
```

4- Configure the app route at wdio.conf.js
* Declare where it is going to be located
```bash
const projectPath = require('path')
const androidAppPath = projectPath.join(process.cwd(), "app/android/Android-MyDemoAppRN.1.3.0.build-244.apk")
const iosAppPath = projectPath.join(process.cwd(),"app/ios/MyRNDemoApp.app");
```

* Set up the capabilities for Android(Emulator sample)
```bash
capabilities: [{
        platformName: 'Android', 
        "appium:device-name": 'Pixel 4 API 30(R)',
        "appium:platformVersion": "11.0",
        "appium:automationName": "UIAutomator2",
        "appium:app": androidAppPath,
        // "appium:appWaitActivity": "com.swaglabsmobileapp.MainActivity"(For OLD swaglabs app)
    }]
```
* Set up the capabilities for Android(Emulator sample)
```bash
capabilities: [{
        platformName: 'IOS',
        "appium:device-name": 'iPhone 13 Pro Max',
        "appium:platformVersion": "16.0",
        "appium:automationName": "XCUItest",
        "appium:app": iosAppPath,   
    }]
```

* Install Appium in your project
```bash
    npm install --save-dev appium@next
```

* Check if the drivers are still available, if not install them again:
```bash 
appium driver list
```
```bash 
appium driver install xcuitest
appium driver install uiautomator2
```

* Run your scripts using
```bash
npx wdio
```

## Setup WebDriverIO
if you want to run this project:

1- Install all the system requirements

2- Clone the project

3- Run: npm i

4- Download the android app and place it under app/android or app/IOS

5- npm run wdioIOS/wdioAndroid
