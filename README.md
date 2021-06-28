# New Job and Build Flutter Apk
### Here, we create a new job for our Flutter application project


#### Dashboard>>New Item>> Enter Item name and select free style project

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/ad_new_item.png?raw=true)


#### Press Ok and Go to Source Code Management -> Check Git and give:


   -  Repository URL: Git URL to your repo. Take this URL from Github. It should be a format of https://github.com/{username}/{project_name}.git

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/ad_repository_error.jpg?raw=true)


   -  Credentials: Select the one you created now or before. ( username and password of your github account as global properties)

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/ad_add_credentials.png?raw=true)

   -  Branches to build: branch_name (here /main used)

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/ad_choose_credentials.jpg?raw=true)

   -  Additional behavious  - Wipe out repository and force clone the branch before build

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/ad_additional_behaviour.png?raw=true)
  
  
### Note:
#### To use gradlew to build apks you have the following dir. and files in root path of repository as shown in picture

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/ad_gradle_structure.png?raw=true)

   - For update or upgrade flutter (for flutter sdk update, if not updated) (global path for flutter also necessary as global variables of jenkins)
      ```
         flutter pub update
         flutter pub upgrade
      ```

  
   -  Build  - Choose Execute shell and write these commands
   
      ```
         flutter clean
         flutter build apk
      ```

   
![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/flutter_build.png?raw=true)


   -  Post Actions  - Choose Archive the artifacts and enter save location for workspace : **/*.apk  and Save.

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/ad_post_actions.png?raw=true)


   -  Build Job  - Now click Build Job in your project, build starts in seconds and you can see logs on clicking jobs in progess

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/ad_build_job.jpg?raw=true)


   -  If you get status of build success then the apk will stored in your workspace and will look like the given below image

![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/ad_build_successful.jpg?raw=true)


#### If you get error or failure then try to resolve that error or share with us as issues, if any thing is missing in our Documentation.

#### Deploy on playstore Android/Flutter Build Apk/Bundle using git repository, visit this branch :
  https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/tree/deploy_on_playstore









