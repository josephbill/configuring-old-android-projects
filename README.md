## RUNNING OLD ANDROID BASED PROJECTS 
### based on old gradle builds i.e. Android studio versions 3.3 >>

#### Steps for project configurations on new AS versions.

1. Delete any local .gradle files generated from previous Android work , If first time install skip this
2. In the projects gradle folder i.e. gradle -> wrapper -> edit this line at the footer section of this slide in the gradle-wrapper.properties version to 8.5 >>> 8.9 >>> 11 , JDK 17 >>>
3. Change the android tools build version in the project’s build.gradle file to match a version compatible with change in 2.
4. Update the kotlin version specified to 1.9.22 >>>
nb/ update the app/build.gradle  compileSDK and target SDK to a more recent version 34.
5. Proceed to update the app/build.gradle dependencies blocks to match newer implementations versions of libraries. :: this change will cause a corresponding import change for the classes referenced in our source files and layout files: check the code files to make adjustments once the migration is done for the dependencies.
      Migrate any reference of appCompat to match android x versions
      Constraint layouts  
      Any external library plugins used
6. New gradle versions require a namespace specification in the build.gradle file , this is a unique identifier for your app’s resources and components.
7. Enable androidx in the gradle.properties file add this line :: android.useAndroidX=true
8. Modify the android manifest file to include android:exported = true option for the launcher class.
9. To ensure consistency in the Java and Kotlin compilers we will add compile options and kotlin options blocks in our android block in the app/build.gradle  file 


Gradle-wrapper.properties change 
distributionUrl=https\://services.gradle.org/distributions/gradle-8.5-bin.zip

Check JDK settings on file -> settings -> build -> build tools -> gradle -> check JDK version

Project :: build.gradle change
classpath 'com.android.tools.build:gradle:8.2.0'

        App level :: build.gradle change 
        Namespace = “package name i.e. com.xxx.xxx”
        android{ … other configs compileOptions {
                                                  sourceCompatibility = JavaVersion.VERSION_17
                                                  targetCompatibility = JavaVersion.VERSION_17
                                                }
                                                kotlinOptions {
                                                jvmTarget = "17"
                                                }
                 }

        Manifest change 
        <activity android:name=".MainActivity"
                     android:exported="true"
                     android:label="@string/app_name"
                     android:launchMode="singleTop">
            

