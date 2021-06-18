# New Job and Build android Apk
### Here, we create a new job for our Android application project


#### Dashboard>>New Item>> Enter Item name and select free style project

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/android_build_apk/ad_new_item.png?raw=true)


#### Press Ok and Go to Source Code Management -> Check Git and give:


   -  Repository URL: Git URL to your repo. Take this URL from Github. It should be a format of https://github.com/{username}/{project_name}.git

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/android_build_apk/ad_repository_error.jpg?raw=true)


   -  Credentials: Select the one you created now or before. ( username and password of your github account as global properties)

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/android_build_apk/ad_add_credentials.png?raw=true)

   -  Branches to build: branch_name (here /main used)

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/android_build_apk/ad_choose_credentials.jpg?raw=true)

   -  Additional behavious  - Wipe out repository and force clone the branch before build

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/android_build_apk/ad_additional_behaviour.png?raw=true)
  
  
### Note:
#### To use gradlew to build apks you have the following dir. and files in root path of repository as shown in picture

  Use image for gradlew directory sample
  
   -  Build  - Choose Execute shell and write these commands
   
![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/android_build_apk/ad_build.png?raw=true)


   -  Post Actions  - Choose Archive the artifacts and enter save location for workspace : **/*.apk  and Save.

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/android_build_apk/ad_post_actions.png?raw=true)


   -  Build Job  - Now click Build Job in your project, build starts in seconds and you can see logs on clicking jobs in progess

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/android_build_apk/ad_build_job.jpg?raw=true)


   -  If you get status of build success then the apk will stored in your workspace and will look like the given below image

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/android_build_apk/ad_build_successful.jpg?raw=true)


#### If you get error or failure then try to resolve that error or share with us as issues, if any thing is missing in our Documentation.











