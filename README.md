# Publish android/flutter apk or bundle to Google Play Store
#### Here, we deploy our release apk and bundles using jenkins server to Google play store
#### Please, go through the below link for the steps and better understanding you need to do for deployment

Link: https://plugins.jenkins.io/google-play-android-publisher/

## Now start with the Step - 1

#### Signing info in Gradle file for release apk or bundle build 

Create new file at root directory of project and name it keystore.properties and enter this 4 entries in it(with your values).

```
   storeFile=/key/file/path.jks 
   keyAlias=key0
   storePassword=notasecret
   keyPassword=notasecret

```

##### Note: 'storeFile' path has .jks file at the time of build apk and be sure the credentials are correct.

And reference this file and values in build.gradle like this.

```
      // Load keystore
      def keystorePropertiesFile = rootProject.file("/path/to/your/keystore.properties")
      def keystoreProperties = new Properties()
      keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
      android {
      
      signingConfigs{
         release {
            storeFile file(keystoreProperties['storeFile'])
            storePassword keystoreProperties['storePassword']
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
               }
         }
         buildTypes {
         release {
            signingConfig signingConfigs.release
         ...
            }
           }
      }
   }
```

### Now, Enabling play console API access and getting json file.

   -  Going to API access page in developer console and linking your project by clicking on link **(Google Play Console -> Settings -> API Access)**.
         
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_link_to_cloud.png?raw=true)

   - Create A project on **Google Cloud** for Google Play Console to link, if you already have then use that project.
         
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_project_link_with_console.jpg?raw=true)
    
   - Open that project, We need to set up API access client by creating service account. You will see option to create service account on the same page below          under **‘Service Accounts’** section.
   
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_create_service_account.jpg?raw=true)
         
   - Once your service account is set up, go to **Google API Console**, open up credentials from left navigation,
     click on create credentials -> Service account key -> Choose your service account -> Choose **JSON** and click create.
     This will download JSON key file in your browser. Do not share this file with anyone.
     
     
     
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_service_ac_created.jpg?raw=true)

     
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_key_section_ad.jpg?raw=true)
     
     
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_json_key_create.png?raw=true)
      
      
         
   -  Now after creating Service Account you need to add App and Grant permissions for the application on **Play Console Api Access Page**.

      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_linked_google_cloud.jpg?raw=true)
      
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_link_sevice_account.jpg?raw=true)
      
      ##### Add Application
      
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_add_app_in_service.jpg?raw=true)
      
      #### Give Permissions

      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/pd_give_permissions.jpg?raw=true)

         
  

   ### Now, add the service account credentials to Jenkins
   
   -  Navigate to your Jenkins instance. Select "Credentials" from the Jenkins sidebar, at the top-level, or from within the folder where the credential should         live. Choose a credentials domain and click "Add Credentials"
    
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jk_manage_credentials.jpg?raw=true)
      

      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jk_add_credential.jpg?raw=true)

    
   -  From the "Kind" drop-down, choose "Google Service Account from private key". Enter a meaningful name for the credential, as you'll need to select it during       build configuration, or enter it into your Pipeline configuration. Choose the "JSON key" type. Upload the .json file that was downloaded by the Google API         Console. Click "OK" to create the credential.
   
   
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jk_add_json_to_cred.jpg?raw=true)
      
      
 
   #### Now, I hope you added all signing info to your build.gradle file and updated the code on your preferred branch.
   
   ### Now, let's start deployment to play store.
   
   -  Create a new free-style software project. Ensure, via whatever build steps you need, that the file(s) you want to upload will be available in the build's         workspace. Add the "Upload Android AAB/APK to Google Play" post-build action. Select the credential name from the drop-down list. The credential must belong       to the Google Play account which owns the app to be uploaded.

      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jk_new_item.png?raw=true)
      
   - Copy articrafts from other projects builds.
  
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jk_copy_articrafts.jpg?raw=true)


   -  Enter paths and/or patterns pointing to the AAB or APKs to be uploaded
        This can be a glob pattern, e.g. 'build/app/outputs/apk/release/**.apk' for release apk and 'build/app/outputs/bundle/release/**.aab' for release bundle
        
      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jk_selecting_cred.jpg?raw=true)

    
   -  Enter the release track to which the files should be assigned. This can be a built-in track like 'production', a testing track like 'beta', or a custom           track name. Note that custom track names are case-sensitive (though the plugin will attempt to determine the correct track). Optionally specify an in-app         update priority.

      ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jk_selecting_track.png?raw=true)


   -  If nothing is entered, the default value (0, lowest priority) will be set by Google Play. 
      As shown in above image, Optionally choose "Add language" to associate release notes with the uploaded file(s).
       
   - Build the project and open the build console to get status of deployment.

       ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jk_build_to_store.jpg?raw=true)


       ![alt_text](https://github.com/deepanshuDPS/Jenkins-Android-CI-CD/blob/main/jk_build_console.jpg?raw=true)

      
 
 ## If you get error or failure then try to resolve that error or share with us as issues, if any thing is missing in our Documentation.
 
 ### Thank You









