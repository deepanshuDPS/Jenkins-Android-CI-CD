# Jenkins-Android-CI-CD
### Here are some steps I used for using Jenkins for android build apk/bundle and Deployment to playstore (CI/CD) [Without Pipeline]


### First of all, What is jenkins?
##### Jenkins is a free and open source automation server. It helps automate the parts of software development related to building, testing, and deploying, facilitating continuous integration and continuous delivery.

For more info - https://www.jenkins.io/

### Why we need to build apks/bundle on Jenkins for testing, if we can share apks and bundle with other sharing sources like Google Drive, Clouds etc.?
##### As of my experience, jenkins gives us a own server of localhost or may be a company/organization server integrated on jenkins. And we use these servers tracking our android build and testing test cases according to requirement within the organization.


### Is it the part of Android Application Development?
##### This is a good question when we are starting android development for ourself not for the organization. But I think it is a good topic for all the developers to learn gradle features of android on this automated server. The main purpose of this topic is to build apk/bundles and deployment of release apks/bundle to play store without signing and opening Google Play Console again and again.

##### If you are interested in learning that how to build apks/bundles and deployment (CI/CD) of application on (Internal/alpha/beta/Production) track of Google play console, I hope this documentation will help you to acheive this task.


## Installing jenkins server on Linux/Windows/MacOs
#### Follow all steps as per given in the references and be sure your OS configured with all the requirements.

Linux Reference: https://www.jenkins.io/doc/book/installing/linux/

Windows Reference: https://www.jenkins.io/doc/book/installing/windows/

MacOs Reference: https://www.jenkins.io/doc/book/installing/macos/

## Steps
  
  Step 1 — Installing Jenkins 
  
  Step 2 — Starting Jenkins
  
  Step 3 — Opening the Firewall
  
  Step 4 — Setting Up Jenkins

Reference (example ubuntu): https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-18-04

### Note:
#### I suggest you to choose " Install suggested plugins " in 'Step 4', when these plugins are installed successfully then we will see what are the remaining plugins we need for our Android build and deployment setup.


![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/suggested_plugins.png?raw=true)


#### After creating jenkins first admin user and confirming the appropriate information, you are ready to use jenkins.

### Open browser and enter your " Jenkins Url " to visit the main Jenkins dashboard:
##### In my case, I used http://localhost:8080 or http://myIp:8080 ( in your case the jenkins URL may be different )


![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/my_jenkins.jpg?raw=true)


##### Now, after installing suggested plugins successfully, you need some more plugins to generate build or deployment. 
###### To Install - Open Jenkins: Manage Jenkins >> Mange Plugins >> Available
##### List of plugins: 
  - Android Signing Plugin
  - Copy Artifact Plugin
  - GitHub Integration Plugin ( if your project repository are on github otherwise you need plugins for Gitlab, Bitbucket etc.)
  - Google Play Android Publisher Plugin
  - Gradle Plugin
  - Google OAuth Credentials plugin

#### Now, After these installations, we ended up with jenkins setup and plugin.

## Set global variables to jenkins (Configure Jenkins)
#### In this part, we will explore how to set global variable for our jenkins server to use our path of PC/laptop for gradles and builds.

##### Open Jenkins: Manage Jenkins >> Configure System >> Global properties >> Environment variables and add:

#### ANDROID_HOME

ANDROID_HOME : /var/lib/jenkins/android-sdk

You can download Android sdk on jenkins home path to use above given path 

**Reference**: https://www.serverkaka.com/2019/03/generate-android-apk-from-source-code-jenkins.html


![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jenkins_android_sdk.png?raw=true)


and if you have already on your system then use your system path

ANDROID_HOME : /home/deepanshu/Android/Sdk


![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/global_properties.png?raw=true)


#### JAVA_HOME

JAVA_HOME : /usr/lib/jvm/java-8-oracle


(If you are developing Flutter project then you need to set and configure Flutter Path also)

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/flutter_path.png?raw=true)


**Reference**: https://medium.com/globant/flutter-jenkins-getting-started-4d2e036567b


## Now After Global Variables Setup, Start a new Job to build APK

#### For Android Build Apk using git repository, visit this branch :
  https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/tree/android_build_apk
  
#### For Flutter Build Apk using git repository, visit this branch :
  https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/tree/flutter_build_apk
  

















