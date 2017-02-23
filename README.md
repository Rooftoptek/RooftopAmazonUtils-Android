# RooftopAmazonUtils-Android

A library that gives you access to the Rooftop cloud platform from your Android app with [Amazon Authorization](https://developer.amazon.com/public/apis/engage/login-with-amazon/docs/create_android_project.html). For more information about Rooftop and its features, see the website and getting started.

## Download

To download SDK with gradle use the next tips.

<b> Step 1: </b>

Set the url to download the sdk in top-level (project-level) build.gradle file

```groovy
allprojects {
  repositories {
    ***
    maven { url 'https://raw.githubusercontent.com/Rooftoptek/Rooftop-SDK-Android/<release name>/releases/' }
    maven { url 'https://raw.githubusercontent.com/Rooftoptek/RooftopAmazonUtils-Android/<release name>/releases/' }
}
```

Url example for release 0.5.0:

```groovy
maven { url 'https://raw.githubusercontent.com/Rooftoptek/RooftopAmazonUtils-Android/0.5.0/releases/' }
```

<b> Step 2: </b>

Set the dependency of the "RooftopAmazonUtils" in the build.gradle file of the main module

```groovy
dependencies {
  ***
  compile(group: 'io.rftp', name: 'rooftopamazonutils', version: '<release name>')
}
```

<b> Step 3: </b>

Download and add to a project Amazon Authorization Library as it is specified at official [Amazon Documentation] (https://developer.amazon.com/public/apis/engage/login-with-amazon/docs/install_sdk_android.html)

## Initialisation

To initialize SDK use the next tips.

<b> Step 1: </b>

Set android minSdkVersion not less than 15

<b> Step 2: </b>

Configure AndroidManifest.xml file of the main project:

  A. Set the permissions:
  
```groovy
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

  B. Set rooftop credentials like meta-data in "application" section.

  B0. Modify AndroidManifest.xml:
  
```groovy
<application
***>
***
  <activity
    android:name="com.amazon.identity.auth.device.workflow.WorkflowActivity"
    android:theme="@android:style/Theme.NoDisplay"
    android:allowTaskReparenting="true" android:launchMode="singleTask">
    <intent-filter>
      <action android:name="android.intent.action.VIEW"/>
      <category android:name="android.intent.category.DEFAULT"/>
      <category android:name="android.intent.category.BROWSABLE"/>
      <!-- android:host must use the full package name found in Manifest General Attributes -->
      <data
        android:host="${applicationId}"
        android:scheme="amzn"/>
    </intent-filter>
  </activity>
    
  <meta-data
    android:name="io.rftp.APPLICATION_ID"
    android:value="@string/rooftop_app_id" />
  <meta-data
    android:name="io.rftp.IDENTITY_POOL_ID"
    android:value="@string/rooftop_identity_pool_id" />
  <meta-data
    android:name="io.rftp.CLIENT_KEY"
    android:value="@string/rooftop_client_key" />
</application>
```

  B1. Put your credentials in strings.xml:

```groovy
<resources>
  ***
  <string name="rooftop_app_id">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
  <string name="rooftop_identity_pool_id">xx-xxxx-x:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</string>
  <string name="rooftop_client_key">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
</resources>
```

  B2. Add api_key.txt file to asset folder as it specified in [Amazon Android SDK doc](https://developer.amazon.com/public/apis/engage/login-with-amazon/docs/create_android_project.html).

<b> Step 3: </b>

Call Rooftop.initialize(*) and RooftopAmazonUtils.initialize(*) in onCreate(*) method of the Application class of the project

```java
public class MyApplication extends Application {
  @Override
  public void onCreate() {
    super.onCreate();
    ***
    Rooftop.initialize(this);
    RooftopAmazonUtils.initialize(this);
  }
}
```

<i> If you don't have your own Application class, create one. Specify usage of your MyApplication class in AndroidManifest-file:</i>

```groovy
<application
  ***
  android:name=".MyApplication">
    ***
</application>
```

<b> Step 4: </b>

Call RooftopAmazonUtils.create(*) in the Activity/Fragment where will be called login method:

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);

  RooftopAmazonUtils.create(this);

  setContentView(R.layout.activity_main);

  ***
}
```

## Basic API calls

<b> Login with Amazon </b>

Call corresponding login method from RooftopAmazonUtils SDK

```java
RooftopAmazonUtils.logIn();
```

<b> Logout with Amazon </b>

```java
AuthorizationManager.signOut(Context context, final Listener<Void, AuthError> listener);
```

For more information about Basic Rooftop API calls, see the website and getting started.

## License

```groovy
Copyright (c) 2016-present, RFTP Technologies Ltd.
All rights reserved.

```