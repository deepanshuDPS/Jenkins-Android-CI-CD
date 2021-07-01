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

         
   -  Add json credentials to jenkins manage credentials








