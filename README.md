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

   -  Going to API access page in developer console and linking your project by clicking on link.
   -  We need to set up API access client by creating service account. You will see option to create service account on the same page below under ‘Service Accounts’ section.
   -  Click on ‘grant access’ and give required permissions.
   -  Download json
   -  Add json credentials to jenkins manage credentials









