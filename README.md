### Running Old Android-Based Projects
Configuring Old Gradle Builds for New Android Studio Versions (3.3 → Latest)
- Steps for Project Configuration on New Android Studio Versions
#### 1. Cleanup
   Delete any locally generated .gradle files from previous Android projects.
   If this is a fresh installation, skip this step.
#### 2. Update Gradle Wrapper
   Navigate to gradle/wrapper/gradle-wrapper.properties
   Modify the distributionUrl at the bottom:
   distributionUrl=https\://services.gradle.org/distributions/gradle-8.5-bin.zip
   Gradually upgrade Gradle versions if necessary (8.5 → 8.9 → 11).
   Ensure JDK version is 17.

#### 3. Update Build System
   Modify the project-level build.gradle to use a compatible Android tools version:
   dependencies {
   classpath 'com.android.tools.build:gradle:8.2.0'
   }

#### 4. Update Kotlin Version
   Change the Kotlin version to 1.9.22.

#### 5. Update compileSdk & targetSdk
   In app/build.gradle, update:
   android {
   compileSdk 34
   defaultConfig {
   targetSdk 34
   }
   }

#### 6. Migrate Dependencies
   Update dependencies in app/build.gradle to match newer implementations.
   After updating dependencies, check your source files and layout files for import adjustments.
   Ensure:
   AppCompat references are updated to AndroidX versions.
   ConstraintLayout and other external libraries are migrated properly.

#### 7. Add Namespace (Required for New Gradle Versions)
   In app-level build.gradle, define the namespace:
   namespace "com.xxx.xxx"

#### 8. Enable AndroidX
   In gradle.properties, add:
   android.useAndroidX=true

#### 9. Modify AndroidManifest.xml
   Add android:exported="true" for your launcher activity:
   <activity android:name=".MainActivity"
   android:exported="true"
   android:label="@string/app_name"
   android:launchMode="singleTop">
   </activity>

#### 10. Ensure Java & Kotlin Compiler Consistency
    Modify app/build.gradle to add compile options:

    android {
    compileOptions {
    sourceCompatibility JavaVersion.VERSION_17
    targetCompatibility JavaVersion.VERSION_17
    }
    kotlinOptions {
    jvmTarget = "17"
    }
    }

#### 11. Verify JDK Settings
    In Android Studio:
    File → Settings → Build → Build Tools → Gradle → Check JDK Version
    Ensure JDK is set to 17.

#### 12. Invalidate caches and restart for a clean build.