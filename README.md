# QUICK START

### Overview 

Applozic Chat & Messaging SDK for your mobile and web apps

Applozic powers real time messaging across any device, any platform & anywhere in the world. Integrate our simple SDK to engage your users with image, file, location sharing and audio/video conversations.

Signup at [Applozic](https://www.applozic.com/) to get your application key.        


# ANDROID SDK    


### Overview         



Android chat and messaging library that lets you enable real time chat without developing or maintaining any infrastructure. 

### Getting Started       



####Step 1: Dependency

Add dependency in build.gradle


```
compile 'com.applozic.communication.uiwidget:mobicomkitui:3.27'    
```


Add packagingOptions in gradle android target:      


```
android {

        packagingOptions    
         {           
           exclude 'META-INF/DEPENDENCIES'      
           exclude 'META-INF/NOTICE'         
           exclude 'META-INF/LICENSE'      
           exclude 'META-INF/LICENSE.txt'    
           exclude 'META-INF/NOTICE.txt' 
           exclude 'META-INF/ECLIPSE_.SF'
           exclude 'META-INF/ECLIPSE_.RSA'
         }    
    }
                
```

####Step 2: Addition of Meta-data, Permissions, Services and Receivers in androidmanifest.xml:
           
        Meta-data
        
```
<meta-data android:name="com.applozic.application.key"
           android:value="YOUR_APPLOZIC_APPLICATION_KEY" /> <!-- Applozic Application Key -->

<meta-data android:name="com.applozic.mobicomkit.notification.icon" 
           android:resource="YOUR_LAUNCHER_ICON" />  <!-- Launcher Icon -->

<meta-data android:name="com.applozic.mobicomkit.notification.smallIcon"
           android:resource="YOUR_LAUNCHER_SMALL_ICON" /> <!-- Launcher white Icon -->
           
<meta-data android:name="share_text"
           android:value="YOUR INVITE MESSAGE" />  <!-- Invite Message -->
           
<meta-data android:name="main_folder_name"
           android:value="@string/default_media_location_folder" /> <!-- Attachment Folder Name -->

<meta-data android:name="com.google.android.geo.API_KEY"
            android:value="YOUR_GEO_API_KEY" />  <!--Replace with your geo api key from google developer console  --> 
<!-- For testing purpose use AIzaSyAYB1vPc4cpn_FJv68eS_ZGe1UasBNwxLI
To disable the location sharing via map add this line ApplozicSetting.getInstance(context).disableLocationSharingViaMap(); in onSuccess of Applozic UserLoginTask -->
           
<meta-data android:name="com.package.name" 
           android:value="${applicationId}" /> 
           
        
```
   **Note**: If you are **not using gradle build** you need to replace ${applicationId}  with your Android app package name

  
  Configure media location folder in your string.xml          
     
```
<string name="default_media_location_folder"><YOUR_APP_NAME></string> 
```
  
  
  Register at [Applozic](https://www.applozic.com/) to get the application key.

Permissions:          


```
<uses-permission android:name="<APP_PKG_NAME>.permission.C2D_MESSAGE" />
<uses-permission android:name="<APP_PKG_NAME>.permission.MAPS_RECEIVE" />
<permission android:name="<APP_PKG_NAME>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
<permission android:name="<APP_PKG_NAME>.permission.MAPS_RECEIVE" android:protectionLevel="signature" />
<uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"  />
<uses-permission android:name="android.permission.READ_CONTACTS" />
<uses-permission android:name="android.permission.WRITE_CONTACTS" />
<uses-permission android:name="android.permission.VIBRATE"/>
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.RECORD_AUDIO" />

  ```


Broadcast Registration For PushNotification:        
   
```
<receiver android:name="com.applozic.mobicomkit.uiwidgets.notification.MTNotificationBroadcastReceiver">
   <intent-filter>            
        <action android:name="${applicationId}.send.notification"/>                    
   </intent-filter>           
</receiver>                  
```

**Note**: If you are **not using gradle build** you need to replace ${applicationId}  with your Android app package name


Activity
   
```
 <activity android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
           android:configChanges="keyboardHidden|orientation|screenSize"
           android:label="@string/app_name"
           android:parentActivityName="<APP_PARENT_ACTIVITY>"
           android:theme="@style/ApplozicTheme"
           android:launchMode="singleTask" >
      <!-- Parent activity meta-data to support API level 7+ -->
<meta-data
           android:name="android.support.PARENT_ACTIVITY"
           android:value="<APP_PARENT_ACTIVITY>" />
 </activity>
                   
<activity android:name="com.applozic.mobicomkit.uiwidgets.people.activity.MobiComKitPeopleActivity"
          android:configChanges="keyboardHidden|orientation|screenSize"
          android:label="@string/activity_contacts_list"
          android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
          android:theme="@style/Applozic.People.Theme"
          android:windowSoftInputMode="adjustResize">
     <!-- Parent activity meta-data to support API level 7+ -->
<meta-data
          android:name="android.support.PARENT_ACTIVITY"
          android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
         <intent-filter>
                 <action android:name="android.intent.action.SEARCH" />
         </intent-filter>
<meta-data
          android:name="android.app.searchable"
          android:resource="@xml/searchable_contacts" />
</activity>

<activity android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.FullScreenImageActivity"
          android:configChanges="keyboardHidden|orientation|screenSize"
          android:label="Image"
 android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
          android:theme="@style/Applozic_FullScreen_Theme">
    <!-- Parent activity meta-data to support API level 7+ -->
<meta-data
          android:name="android.support.PARENT_ACTIVITY"
          android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
</activity>

<activity android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.ContactSelectionActivity"
            android:configChanges="keyboardHidden|orientation|screenSize"
            android:launchMode="singleTop"
            android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
            android:theme="@style/ApplozicTheme">
   <meta-data
            android:name="android.support.PARENT_ACTIVITY"
            android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
 </activity>

<activity android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.ChannelCreateActivity"
          android:configChanges="keyboardHidden|orientation|screenSize"
          android:launchMode="singleTop"
          android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
          android:theme="@style/ApplozicTheme">
     <meta-data
              android:name="android.support.PARENT_ACTIVITY"
              android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
</activity>

 <activity android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.ChannelNameActivity"
           android:configChanges="keyboardHidden|orientation|screenSize"
           android:launchMode="singleTop"
           android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
           android:theme="@style/ApplozicTheme">
</activity>

 <activity android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.ChannelInfoActivity"
           android:configChanges="keyboardHidden|orientation|screenSize"
           android:launchMode="singleTop"
           android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
           android:theme="@style/ApplozicTheme">
  <meta-data
           android:name="android.support.PARENT_ACTIVITY"
           android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
 </activity>

<activity
     android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.MobiComAttachmentSelectorActivity"
     android:configChanges="keyboardHidden|orientation|screenSize"
     android:launchMode="singleTop"
     android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
     android:theme="@style/ApplozicTheme"
     android:windowSoftInputMode="stateHidden|adjustResize">
 <meta-data 
           android:name="android.support.PARENT_ACTIVITY"
           android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
 </activity>
 
 <activity android:name="com.applozic.mobicomkit.uiwidgets.conversation.activity.MobicomLocationActivity"
            android:configChanges="keyboardHidden|orientation|screenSize"
            android:parentActivityName="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity"
            android:theme="@style/ApplozicTheme"
            android:windowSoftInputMode="adjustResize">
 </activity>
 ```
  
  
  Service
         
```          
<service android:name="com.applozic.mobicomkit.api.conversation.MessageIntentService"
          android:exported="false" />
              
<service android:name="org.eclipse.paho.android.service.MqttService"/>

<service android:name="com.applozic.mobicomkit.api.conversation.ApplozicIntentService"
         android:exported="false" />
             
<service android:name="com.applozic.mobicomkit.api.conversation.ApplozicMqttIntentService"
         android:exported="false" />
```


Receiver

```
<receiver android:name="com.applozic.mobicomkit.broadcast.NotificationBroadcastReceiver">
         <intent-filter>
                 <action android:name="applozic.LAUNCH_APP" />
         </intent-filter>
<meta-data
          android:name="activity.open.on.notification"
          android:value="com.applozic.mobicomkit.uiwidgets.conversation.activity.ConversationActivity" />
</receiver>

<receiver android:name="com.applozic.mobicomkit.broadcast.TimeChangeBroadcastReceiver">
         <intent-filter>
                 <action android:name="android.intent.action.TIME_SET" />
                 <action android:name="android.intent.action.TIMEZONE_CHANGED" />
         </intent-filter>
</receiver>

<receiver android:name="com.applozic.mobicomkit.broadcast.ConnectivityReceiver"
          android:exported="true" android:enabled="true">
          <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
                  <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
          </intent-filter>
</receiver>                  
```


Replace APP_PARENT_ACTIVITY with your app's parent activity.        


####Step 3: Register user account:     

UserLoginTask
     
```
UserLoginTask.TaskListener listener = new UserLoginTask.TaskListener() {                  

@Override          
public void onSuccess(RegistrationResponse registrationResponse, Context context)         
{           
   // After successful registration with Applozic server the callback will come here 
    ApplozicSetting.getInstance(context).showStartNewButton();//To show contact list.
    ApplozicSetting.getInstance(context).showStartNewGroupButton();//To enable group messaging
}                       

@Override             
public void onFailure(RegistrationResponse registrationResponse, Exception exception)         
{  
    // If any failure in registration the callback  will come here 
}};                      

User user = new User();          
user.setUserId(userId); //userId it can be any unique user identifier
user.setDisplayName(displayName); //displayName is the name of the user which will be shown in chat messages
user.setEmail(email); //optional                        
new UserLoginTask(user, listener, this).execute((Void) null);                                   
```

If it is a new user, new user account will get created else existing user will be logged in to the application.


####Step 4: Updating GCM registration id

In case, if you don't have the existing GCM related code, then copy the files from https://github.com/AppLozic/Applozic-Android-SDK/tree/master/app/src/main/java/com/applozic/mobicomkit/sample/pushnotification
to your project and add the following lines in the "onSuccess" method mentioned in Step 3.

To Enable Android Push Notification using Google Cloud Messaging (GCM) visit the below link http://www.applozic.com/blog/enable-android-push-notification-using-google-cloud-messaging-gcm/

After Registering project at https://console.developers.google.com Replace the value of GCM_SENDER_ID in GCMRegistrationUtils.java with your own project gcm sender id.
SenderId is a unique numerical value created when you configure your API project (given as "Project Number" in the Google Developers Console).            


```
 GCMRegistrationUtils gcmRegistrationUtils = new GCMRegistrationUtils(activity);          
 gcmRegistrationUtils.setUpGcmNotification();                      
```

If you already have a GCM code in your app, then copy the following code at the place where you are getting the GCM registration id.       
     
```
PushNotificationTask pushNotificationTask = null         
PushNotificationTask.TaskListener listener = new PushNotificationTask.TaskListener()   
{                  

@Override           
public void onSuccess(RegistrationResponse registrationResponse)             
{            
}            
@Override          
public void onFailure(RegistrationResponse registrationResponse, Exception exception)      
{             
} 

};                    

pushNotificationTask = new PushNotificationTask(pushnotificationId, listener, mActivity);            
pushNotificationTask.execute((Void) null);                          
```


####Step 5: Handling push notification

Add the following in your GcmBroadcastReceiver's onReceive method.     

       
```
if(MobiComPushReceiver.isMobiComPushNotification(intent))       
{            
MobiComPushReceiver.processMessageAsync(context, intent);               
return;          
}                     
```


####Step 6: Start chat activity:        

ConversationActivity
      
```
Intent intent = new Intent(this, ConversationActivity.class);            
startActivity(intent);                               
``` 
 
 
 For starting individual conversation thread, set "userId" in intent:        
 
           
```
Intent intent = new Intent(this, ConversationActivity.class);            
intent.putExtra(ConversationUIService.USER_ID, "devashish@applozic.com");             
intent.putExtra(ConversationUIService.DISPLAY_NAME, "Devashish Mamgain"); //put it for displaying the title.             
startActivity(intent);                              
```

####Step 7: On logout, call the following:       

Logout

```
 new UserClientService(this).logout();      
```
 
 
 Note: If you are running ProGuard, please add following lines:        
 
```
 #keep json classes                
 -keepclassmembernames class * extends com.applozic.mobicomkit.api.JsonMarker         
 {            
 !static !transient <fields>;                  
 }              
 #GSON Config          
-keepattributes Signature          
-keep class sun.misc.Unsafe { *; }           
-keep class com.google.gson.examples.android.model.** { *; }            
-keep class org.eclipse.paho.client.mqttv3.logging.JSR47Logger { *; }                                    
 ``` 


#### Running demo app

Open project in Android Studio to run the sample app in your device. Send messages between multiple devices. 


#### Display name for users

You can either choose to handle display name from your app or have Applozic handle it.
From your app's first activity, set the following to disable display name feature:

```
ApplozicClient.getInstance(this).setHandleDisplayName(false);
```

By default, the display name feature is enabled.



### UI Customization

####Changing the Chat Bubble Color add this line inside the UserLoginTask onSuccess()

Sent Message bubble color
 ```
ApplozicSetting.getInstance(context).setSentMessageBackgroundColor(int color); // it accepts the R.color.name
 ```
 
Received Message bubble color

 ```
ApplozicSetting.getInstance(context).setReceivedMessageBackgroundColor(int color); // it accepts the R.color.name
 ```

####Changing the Send Bubble Color add this line inside the UserLoginTask onSuccess()

 ```
ApplozicSetting.getInstance(context).setSendButtonBackgroundColor(int color); // it accepts the R.color.name
 ```

####To show the Online in Quick Chat Screen add this line inside the UserLoginTask onSuccess()

 ```
ApplozicSetting.getInstance(context).showOnlineStatusInMasterList();
 ```

####To show contact list add this line inside the UserLoginTask onSuccess()
 
 ```
 ApplozicSetting.getInstance(context).showStartNewButton();
```

####To show contact list FloatingActionButton  add this line inside the UserLoginTask onSuccess()
 
```
ApplozicSetting.getInstance(context).showStartNewFloatingActionButton();
```


For complete control over UI, you can also download open source chat UI toolkit and change it as per your designs : [https://github.com/AppLozic/Applozic-Android-SDK](https://github.com/AppLozic/Applozic-Android-SDK)

Import [MobiComKitUI Library](https://github.com/AppLozic/Applozic-Android-SDK/tree/master/mobicomkitui)  into your android project and add the following in the build.gradle file:

compile project(':mobicomkitui')


MobiComKitUI contains the ui related source code, icons, layouts and other resources which you can customize based on your design needs.

For your custom contact list, replace MobiComKitPeopleActivity with your contact list activity.

Sample app with integration is available under [app](https://github.com/AppLozic/Applozic-Android-SDK/tree/master/app)


### Messages             
Refer to the below documentation for a deeper integration if you wish to perform chat operation directly from your app's interface without using the Applozic UI toolkit:


####Account registration   
   
```
Class: com.applozic.mobicomkit.api.account.register.RegisterUserClientService      
```


```
new RegisterUserClientService(activity).createAccount
(USER_EMAIL, USER_ID, USER_PHONE_NUMBER, GCM_REGISTRATION_ID);         
 ``` 

####Send message   

```
Class: com.applozic.mobicomkit.api.conversation.MobiComConversationService         
```


```
 public void sendMessage(Message message)        
 {             
   ...        
 }                
```

Example: 
```
new MobiComConversationService(activity).sendMessage(new     
Message("contact@applozic.com", "hello test"));         
```


####Message list      

```
Class: com.applozic.mobicomkit.api.conversation.MobiComConversationService
```
  
i) Get single latest message from each conversation        

```
 public synchronized List<Message> getLatestMessagesGroupByPeople()        
 {            
  ...         
 }                              
```


ii) Get messages of logged in user with another user by passing userId, startTime and      
 endTime. startTime and endTime are considered in time in milliseconds from 1970.       


```
 public List<Message> getMessages(String userId, Long startTime, Long endTime)        
 {            
  ...           
 }                           
```



###  Contacts           



***Creating Contact list***         



You can create the contact list in two easy steps by using AppContactService.java api. Sample method **buildContactData()** for adding contacts is present in sample app MainActivity.java.

**Step 1: Creating contact object:**         

```
    Contact contact = new Contact();            
    contact.setUserId(<userId>);           
    (Unique ID to identify contact )                 
    contact.setFullName(<full name of contact>);                 
    contact.setEmailId(<EmailId>);               
    contact.setImageURL(<image http URL OR android resource drawable  >);               
    (in case of drawable use R.drawable.<resource_name>)                         
```

Example :        

```
    Contact contact = new Contact();                 
    contact.setUserId("adarshk");           
    contact.setFullName("Adarsh");               
    contact.setImageURL("R.drawable.applozic_ic_contact_picture_holo_light");           
    contact.setEmailId("github@applozic.com");                
```

**Step 2: Add contacts :**

After creating contact object in Step 1, add the contact using AppContactService.java add() method.
 
Example :        

```
    Context context = getApplicationContext();           
    AppContactService appContactService = new AppContactService(context);            
    appContactService.add(contact);                           
```



**AppContactService.Java at a glance**



AppContactService.java provides methods you need to add, delete and update contacts.

Add single contact
```
add(Contact contact)
```

Add multiple contacts
```
addAll(List<Contact> contactList)
```

Delete contact
```
deleteContact(Contact contact)
```

Delete contact by Id
```
deleteContactById(String contactId)
```

Read contact by Id
```
getContactById(String contactId )
```

Update contact
```
updateContact(Contact contact)
```

Update or Insert contact
```
upsert(Contact contact)
```



### Group 


**1) Group create Method**  

Create the Group with Group Name and Group Members. The below code illustrator creation of group 

  Class to import : com.applozic.mobicomkit.api.people.ChannelCreate            
  
  Class to import : com.applozic.mobicomkit.channel.service.ChannelService
  
  ```
new Thread(new Runnable() {
     @Override
           public void run() {
                String groupName = "Applozic Group"; // Name of group.
                List<String> groupMemberList = new ArrayList<String>(); // List Of unique group member Names.
                groupMemberList.add("member1");   // Put userId of the user
                groupMemberList.add("member2");
                groupMemberList.add("member3");
                groupMemberList.add("member4");

  // After adding group Members to List then pass the Group Name and Group Member List to constructor below

  ChannelCreate channelCreate = new ChannelCreate(groupName, groupMemberList); // The Constructor accepts the two parameter String Group Name and List of Group Members.

  Channel channel = ChannelService.getInstance(context).createChannel(channelCreate); // Instantiating the  group create and it accept the ChannelCreate object.
               }
           }).start();
 ```
 

**2) Add Member to group** 

 ``` 
 Intent addUserIntent = new Intent(context, ApplozicChannelIntentService.class);
 addUserIntent.putExtra(ApplozicChannelIntentService.CHANNEL_KEY, "channelKey"); //Replace channelKey with your channelKey i.e groupId
 addUserIntent.putExtra(ApplozicChannelIntentService.ADD_USER_TO_CHANNEL, "userId");// Replace the userId with which u want add the user into the group
 startService(addUserIntent);
 ```
 
 **3) Remove Member From the group**
  ```
 Intent removeUserIntent = new Intent(context, ApplozicChannelIntentService.class);
 removeUserIntent.putExtra(ApplozicChannelIntentService.CHANNEL_KEY, "channelKey");//Replace channelKey with your channelKey i.e groupId
 removeUserIntent.putExtra(ApplozicChannelIntentService.REMOVE_USER_ID_FROM_CHANNEL, "userId");// Replace the userId that which u want to Remove  user from the group
 startService(removeUserIntent);
 ```
 
 **4)To Change the Group Name**
 ```
  Intent changeGroupNameIntent = new Intent(context, ApplozicChannelIntentService.class);
  changeGroupNameIntent.putExtra(ApplozicChannelIntentService.CHANNEL_KEY, "channelKey");//Replace channelKey with your channelKey i.e groupId
  changeGroupNameIntent.putExtra(ApplozicChannelIntentService.CHANGE_CHANNEL_NAME, "newName"); //Replace the newName with group name
  startService(changeGroupNameIntent);
 ```






 # IOS SDK           


### Overview        



iOS chat and messaging library that lets you enable real time chat without developing or maintaining any infrastructure.




### Getting Started                 




**Create your Application**

a )  [**Sign up**](https://www.applozic.com/signup.html) with Applozic to get your application key.

b ) Once you signed up create your Application with required details on admin dashboard. Upload your push notification certificate to our portal to enable real time notification.         


![dashboard-blank-content](https://raw.githubusercontent.com/AppLozic/Applozic-Chat-SDK-Documentation/master/Resized-dashboard-blank-page.png)         


c) After creating application, you will see your application key listed on admin dashboard. Please use same application key explained in further steps.          


![dashboard-blank-content](https://raw.githubusercontent.com/AppLozic/Applozic-Chat-SDK-Documentation/master/Resized-dashboard-content-page.png)         



**Installing the iOS SDK** 

**ADD APPLOZIC FRAMEWORK **
Clone or download the SDK (https://github.com/AppLozic/Applozic-iOS-SDK/tree/master/Framework/Applozic.framework)
Get the latest framework "Applozic.framework" from Applozic github repo [**sample project**](https://github.com/AppLozic/Applozic-iOS-SDK/tree/master/sampleapp)

**Add framework to your project:**

![dashboard-blank-content](https://raw.githubusercontent.com/AppLozic/Applozic-Chat-SDK-Documentation/master/Resized-adding-applozic-framework.png)        


i ) Paste Applozic framework to root folder of your project. 
ii ) Go to Build Phase. Expand  Embedded frameworks and add applozic framework.         



**Quickly Launch your chat**


You can test your chat quickly by adding below .h and .m file to your project.

[**DemoChatManager.h**](https://raw.githubusercontent.com/AppLozic/Applozic-iOS-SDK/master/sampleapp/applozicdemo/DemoChatManager.h)        

[**DemoChatManager.m**](https://raw.githubusercontent.com/AppLozic/Applozic-iOS-SDK/master/sampleapp/applozicdemo/DemoChatManager.m)  

Change applicationID in DemoChatManager and you are ready to launch your chat from your controller :)

Launch your chat

```
//Replace with your applicationId in DemoChatManager.h

#define APPLICATION_ID @"applozic-sample-app" 


//Launch your Chat from your controller.
 DemoChatManager * demoChatManager = [[DemoChatManager alloc]init];
    [demoChatManager launchChat:<yourcontrollerReference> ];

```

Detail about user creation and registraion:


**USER REGISTRATION :**

**Create a user : ** 
After your app login validation, copy the following code to create applozic user and register your user with applozic server.           


** Objective-C **   
```
 ALUser *user = [[ALUser alloc] init];           
 [user setApplicationId:@"applozic-sample-app"]; // REPLACE SAMPLE ID with your application key                
 [user setUserId:[self.userIdField text]]; //replace [self.userIdField text] with user's unique id here                    
 [user setEmailId:[self.emailField text]]; //optional                       
```
   
   
   **Register user with Applozic server :**       
   
   
** Objective-C **
```
  ALRegisterUserClientService *registerUserClientService = [[ALRegisterUserClientService alloc] init];           
  [registerUserClientService initWithCompletion:user withCompletion:^(ALRegistrationResponse *rResponse, 
  NSError *error)       
  {             
  if (error)        
  {             
     NSLog(@"%@",error);            
     UIAlertView *alertView = [[UIAlertView alloc] initWithTitle:@"Response"                
     message:rResponse.message delegate: nil cancelButtonTitle:@"Ok"          
     otherButtonTitles: nil, nil];            
     [alertView show];             
      return ;                  
  }                      
  
   if (rResponse && [rResponse.message containsString: @"REGISTERED"])               
   {                 
     ALMessageClientService *messageClientService = [[ALMessageClientService alloc] init];             
     [messageClientService addWelcomeMessage];             
     }        
     NSLog(@"Registration response from server:%@", rResponse);               
   }];                                       
```



**PUSH NOTIFICATION REGISTRATION AND HANDLING **

**a ) Send device token to applozic server:**

In your AppDelegate’s **didRegisterForRemoteNotificationsWithDeviceToken **method  send device registration to applozic server after you get deviceToken from APNS. Sample code is as below:             




** Objective-C **      
```
 - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)
   deviceToken       
   {                
  
    const unsigned *tokenBytes = [deviceToken bytes];            
    NSString *hexToken = [NSString stringWithFormat:@"%08x%08x%08x%08x%08x%08x%08x%08x",                 
    ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),             
    ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),             
    ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];              
    
    NSString *apnDeviceToken = hexToken;            
    NSLog(@"apnDeviceToken: %@", hexToken);                  
 
   //TO AVOID Multiple call to server check if previous apns token is same as recent one, 
   if different call app lozic server.           

    if (![[ALUserDefaultsHandler getApnDeviceToken] isEqualToString:apnDeviceToken])              
    {                         
       ALRegisterUserClientService *registerUserClientService = [[ALRegisterUserClientService alloc] init];          
       [registerUserClientService updateApnDeviceTokenWithCompletion
       :apnDeviceToken withCompletion:^(ALRegistrationResponse
       *rResponse, NSError *error)       
     {              
       if (error)         
          {          
             NSLog(@"%@",error);             
            return ;           
          }              
    NSLog(@"Registration response from server:%@", rResponse);                         
    }]; } }                                 

```


**b) Receiving push notification:**

Once your app receive notification, pass it to applozic handler for applozic notification processing.             


** Objective-C **      
  ```
  - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)dictionary         
  {            
   NSLog(@"Received notification: %@", dictionary);           
   
   ALPushNotificationService *pushNotificationService = [[ALPushNotificationService alloc] init];        
   BOOL applozicProcessed = [pushNotificationService processPushNotification:dictionary updateUI:
   [[UIApplication sharedApplication]     applicationState] == UIApplicationStateActive];             
  
    //IF not a appplozic notification, process it            
  
    if (!applozicProcessed)            
      {                
         //Note: notification for app          
    } }                                                           
```


**c) Handling app launch on notification click :**          


** Objective-C **    
```
 - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions    
  {                     
  // Override point for customization after application launch.                              
  NSLog(@"launchOptions: %@", launchOptions);                  
  if (launchOptions != nil)               
  {             
  NSDictionary *dictionary = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];         
  if (dictionary != nil)             
    {          
      NSLog(@"Launched from push notification: %@", dictionary);        
      ALPushNotificationService *pushNotificationService = [[ALPushNotificationService alloc] init];            
      BOOL applozicProcessed = [pushNotificationService processPushNotification:dictionary updateUI:NO];               
  if (!applozicProcessed)                 
     {            
       //Note: notification for app              
     } } }                                   
      return YES;                 
  }                             

```


**Launching applozic message screen** 

Below code will explain how to launch applozic message view. you can put this according to your need (like on click of any button, add any button at the navigation bar or tab ).            


** Objective - C **     
```
   UIStoryboard* storyboard = [UIStoryboard storyboardWithName:@"Applozic"              
   bundle:[NSBundle bundleForClass:ALMessagesViewController.class]];              
   UIViewController *theTabBar = [storyboard instantiateViewControllerWithIdentifier:@"messageTabBar"];          
   [self presentViewController:theTabBar animated:YES completion:nil];                     
```




**Launching specific user's conversation:
**
To launch conversation for a particular user (most common use case is to launch customer support conversation directly), use below code:         




** Objective - C **        
```
UIStoryboard* storyboard = [UIStoryboard storyboardWithName:@"Applozic"                 
bundle:[NSBundle bundleForClass:ALChatViewController.class]];             
ALChatViewController *chatView =(ALChatViewController*) [storyboard 
instantiateViewControllerWithIdentifier:@"ALChatViewController"];                
chatView.contactIds =@"<USER_ID>";//SET specific USER'S ID                  
UINavigationController *conversationViewNavController = 
[[UINavigationController alloc] initWithRootViewController:chatView]; 
[self presentViewController:conversationViewNavController animated:YES completion:nil];                               
    
```    
    
    
 **Note : make sure you have already registered your login user(User Registration) and completed  push notification registration before launching Applozic message screen.**          
    
    
    
****Logout****           
    
    
    
    
Paste the following code on logout.             
    
    
** Objective - C **           
  ```
  ALRegisterUserClientService *registerUserClientService = [[ALRegisterUserClientService alloc] init];              
  [registerUserClientService logout];                       
  ```
  
  
  
### Contacts             




Applozic framework provides convenient APIs for building your own contact. Developers can build and store contacts in three different ways. 

 **Build your contact:** 

** a ) Simple method to create your contact is to create contact object.
**                 




** Objective - C **        
```
ALContact *contact1 = [[ALContact alloc] init];              
contact1.userId = @"adarshk"; // unique Id for user               
contact1.fullName = @"Adarsh Kumar"; // Fullname of the contact.               

//Display name for contact. This name would be displayed to the user in chat and contact list.                  
contact1.displayName = @"Adarsh";               
contact1.email = @"github@applozic.com"; //Email Id for the contact.              
//Contact image url. Contact image would be downloaded automatically from URL.                  
ontact1.contactImageUrl =@"https://www.applozic.com/resources/images/applozic_logo.gif";        
contact1.localImageResourceName = @"adarsh.jpg"; // If this field is mentioned,
Contact image will be taken from local storges.   
```


**b) Creating contact from dictionary:
**
You can directly create contact from dictionary, all you have to do is just pass a dictionary while initialising object.          




** Objective -C **  
```
  //Contact ------- Example with dictonary 
  NSMutableDictionary *demodictionary = [[NSMutableDictionary alloc] init]; 
  [demodictionary setValue:@"adarshk" forKey:@"userId"]; 
  [demodictionary setValue:@"Adarsh Kumar" forKey:@"fullName"]; 
  [demodictionary setValue:@"Adarsh" forKey:@"displayName"];  
  [demodictionary setValue:@"github@applozic.com" forKey:@"email"]; 
  [demodictionary setValue:@"https://www.applozic.com/resources/images/applozic_logo.gif" forKey:@"contactImageUrl"]; 
  [demodictionary setValue:nil forKey:@"localImageResourceName"];              
  ALContact *contact5 = [[ALContact alloc] initWithDict:demodictionary];                   
```




**b) Building contact from JSON:
**           



** Objective -C **       
```
//Contact -------- Example with json                   
NSString *jsonString =@"{\"userId\": \"applozic\",\"fullName\": \"Applozic\",
\"contactNumber\": \"9535008745\",\"displayName\":  \"Applozic Support\",
\"contactImageUrl\": \"https://www.applozic.com/resources/images/applozic_logo.gif\",\"email\":       
\"devashish@applozic.com\",\"localImageResourceName\":\"sample.jpg\"}";                   
ALContact *contact4 = [[ALContact alloc] initWithJSONString:jsonString];                        
 ```
 
 
 
 **Add Your Contact:** 


**Add single contact API
**


** Objective - C **    

 ```
 -(BOOL)addContact:(ALContact *)contact;
 ```
 
 Example:
 ```
 ALContact *contact  = [[ALContact alloc] init];              
 contact.userId      = @"adarshk";      // Unique Id for user               
 contact.fullName    = @"Adarsh Kumar"; // Fullname of the contact.  
 contact.displayName = @"Adarsh";       // Name on display
 
 ALContactService * alContactService = [[ALContactService alloc] init];                   
 [alContactService addContact:contact]; 
```


Below are additional APIs for contact load, update and delete and requires a ALContact object or array of ALContact objects. 

** Objective - C **            
```

#  Fetch/Load contact API
/*  Use "userId" for <key> and contact's user id string as <value> for below API */
  - (ALContact *)loadContactByKey:(NSString *) key value:(NSString*) value
  
#   Update APIS                 
  -(BOOL)updateContact:(ALContact *)contact                    
  -(BOOL)updateListOfContacts:(NSArray *)contacts
 
#  Add contact(s) APIs              
  -(BOOL)addListOfContacts:(NSArray *)contacts          
  -(BOOL)addContact:(ALContact *)contact
 
#    Deleting APIS               
  //For purging single contact 
  -(BOOL)purgeContact:(ALContact *)contact             
  
  //For purging multiple contacts                
  -(BOOL)purgeListOfContacts:(NSArray *)contacts
  
  //For purging all contacts at once              
  -(BOOL)purgeAllContacts 
  
 ```
 

### **Contextual Conversation**
 
 Applozic SDK provide APIs which let you set and customise the chat’s context. Developers can create a ‘Conversation’ and launch a chat with context set. 

The picture below shown depicts the context header set below the navigation bar.Suppose a buyer want to have context chat with seller 'Adarsh' on product macbook pro.

 ![picture alt](https://raw.githubusercontent.com/AppLozic/Applozic-iOS-SDK/master/images/contextBased.png "Context-based header view")

__ALConversationProxy__ is a class which let you build your conversation context

ALConversationProxy have three type of properties as following:          


   1.**topicId**: A unique ID for your Topic/context you want to chat.                        
   2.**userId**: User ID of person you like to start your chat with.                    
   3.**alTopicDetail**:
      Topic **title**                                               
      Topic **subtitle**             
      Image **link**                
      **key1**  and  **value1**: For ex. key1 be “Product ID” and value1 be “569-01”            
      **key2**  and  **value2**: For ex. key1 be “Price” and value2 be “Rs.1,50,00”              



**Key1 and Key2 is a placeholder to store with respective value1 and value2 values**

** Objective - C **            

```
ALConversationProxy * alConversationProxy = [[ALConversationProxy alloc] init];
alConversationProxy.topicId = @”buyMacPro";
alConversationProxy.userId = @"adarshk"
   
ALTopicDetail * alTopicDetail	= [[ALTopicDetail alloc] init];
alTopicDetail.title 		 	= @”Mac Book Pro";
alTopicDetail.subtitle 	  	= @"13’ Retina";
alTopicDetail.link = @"http://d.ibtimes.co.uk/en/full/319949/macbook-pro-13in-retina.jpg";
alTopicDetail.key1      	 	= @"Product ID";
alTopicDetail.value1    		= @"mac-pro-r-13";
alTopicDetail.key2      		= @"Price”;
alTopicDetail.value2    		= @"Rs.1,04,999.0";

NSData *jsonData = [NSJSONSerialization dataWithJSONObject:alTopicDetail.dictionary  
options:NSJSONWritingPrettyPrinted error:nil];
NSString *topicDetails = [[NSString alloc] initWithData:jsonData    encoding:NSUTF8StringEncoding];
 
alConversationProxy.topicDetailJson = topicDetails;
```

**       API to create conversation using ALConversationProxy object            **

```
-(void)createConversation:(ALConversationProxy *)alConversationProxy withCompletion:(void(^)(NSError *error,ALConversationProxy * proxy ))completion;
```



### UI Customization           




Applozic SDK provides various UI settings to customise chat view eaisly. If you are using __DemoChatManager.h__ explained in the  earlier section, you can put all your settings in below method. 

```
-(void)ALDefaultChatViewSettings;
```

If you have your own implementation, you should set UI Customization setting on successfull registration of user.

Below section will explain UI settings provided by Applozic SDK.


#### Received Message bubble color

__Objective-C__
```
[ALApplozicSettings setColorForReceiveMessages: [UIColor colorWithRed:255.0/255 green:255.0/255 blue:255.0/255 alpha:1]];
```

__Swift__
```
ALApplozicSettings.setColorForReceiveMessages(UIColor(red: 255/255, green: 255/255, blue: 255/255, alpha:1))
```

#### Send Message bubble color

__Objective-C__
```
[ALApplozicSettings setColorForSendMessages: [UIColor colorWithRed:66.0/255 green:173.0/255 blue:247.0/255 alpha:1]];
```

__Swift__
```
ALApplozicSettings.setColorForSendMessages(UIColor(red: 66.0/255, green: 173.0/255, blue: 247.0/255, alpha:1))
```

#### Set Colour for Navigation Bar

__Objective-C__
```
[ALApplozicSettings setColorForNavigation: [UIColor colorWithRed:66.0/255 green:173.0/255 blue:247.0/255 alpha:1]];
```

__Swift__
```
ALApplozicSettings.setColorForNavigation(UIColor(red: 66.0/255, green: 173.0/255, blue: 247.0/255, alpha:1))
```

#### Set Colour for Navigation Bar Item

__Objective-C__
```
[ALApplozicSettings setColorForNavigationItem: [UIColor whiteColor]];
```

__Swift__
```
ALApplozicSettings.setColorForNavigationItem(UIColor.whiteColor())
```

#### Hide/Show profile Image

__Objective-C__
```
[ALApplozicSettings setUserProfileHidden: NO];
```

__Swift__
```
ALApplozicSettings.setUserProfileHidden(false)
```

#### Hide/Show Tab Bar

__Objective-C__
```
[ALUserDefaultsHandler setBottomTabBarHidden: YES];
```

__Swift__
```
ALUserDefaultsHandler.setBottomTabBarHidden(false)
```

#### Hide/Show Logout Button (refresh button in sample app)

__Objective-C__
```
[ALUserDefaultsHandler setLogoutButtonHidden: YES];
```

__Swift__
```
ALUserDefaultsHandler.setLogoutButtonHidden(false)
```

#### Hide/Show Refresh Button

__Objective-C__
```
[ALApplozicSettings hideRefreshButton: NO];
```

__Swift__
```
ALApplozicSettings.hideRefreshButton(flag)
```

#### Set Title For Conversation Screen

__Objective-C__
```
[ALApplozicSettings setTitleForConversationScreen: @"Recent Chats"];
```

__Swift__
```
ALApplozicSettings.setTitleForConversationScreen("Recent Chats")
```

#### Set Font Face

__Objective-C__
```
[ALApplozicSettings setFontaFace: @"Helvetica"];
```

__Swift__
```
ALApplozicSettings.setFontFace("Helvetica")
```

#### Set Group Option

__Objective-C__
```
[ALApplozicSettings setGroupOption: YES];
```

__Swift__
```
ALApplozicSettings.setGroupOption(true)
```
This method is used when group feature is required . It will disable group functionality when set to NO.




### **Channel API** 

This section explain about convenient SDK APIs  related to group.  

__Class to import :__ Applozic/ALChannelService.h 

#### 1. Add new Channel

You can create a Channel/Group by simply calling createChannel method. The callback argument (channelKey) will be unique ChannelId/GroupId created by applozic server. You need to store this for any further operations( like : add member, remove  member, delete group/channel etc) on Channel/Group.  
```
-(void) createChannel:(NSString *) channnelName andMemberList:(NSMutableArray *) memberArray withCompletion:(void(^)(NSNumber *channelKey)) completion
```
__Parameters:__

__channelName :__ Name of group

__memberArray :__ Array of contactId/userid of members

 
#### 2. Add New member to Channel
 ```
-(BOOL) addMemberToChannel:(NSString *) userId andChannelKey:(NSNumber *) channelKey
 ``` 	  	
__Parameters:__

__userId :__ contactId/userId

__channelkey :__ channel key/GroupId of your channel where member will be added.

__Return Type :__ BOOL

If member added successfully then it will return YES else NO. 
 
__NOTE:__ Only admin can add member to the group/channel. For more detail see check Admin section.


#### 3.  Remove Member from Channel
 ```
-(BOOL) removeMemberFromChannel:(NSString *)userId andChannelKey:(NSNumber *)channelKey
 ```
__Parameters:__

__userId :__ contactId OR userId

__channelkey :__ channel key of your channel from which member will be removed.

__Return Type :__ BOOL

If member removed successfully then it will return YES else NO. 

__NOTE:__ Only admin can add member to the group/channel. For more detail see check Admin section.
 

#### 4.   Delete Channel
```
-(BOOL) deleteChannel:(NSNumber *) channelKey
```
__Parameters:__

__channelkey :__ channel key of your channel from which member will be removed.

__Return Type :__ BOOL

If channel deleted successfully then it will return YES else NO. 

__NOTE:__ Only admin can add member to the group/channel. For more detail see check Admin section.
 

#### 5.   Leave Channel
```
-(BOOL) leaveChannel:(NSNumber *) channelKey andUserId:(NSString *) userId
```
__Parameters:__

__channelkey :__ channel key of your channel whom you are leaving.

__userId:__ userid  of leaving user

__Return Type :__ BOOL

If member leaved successfully then it will return YES else NO. 


#### 6. Rename Channel
 ```
-(BOOL) renameChannel:(NSNumber *) channelKey andNewName:(NSString *) newName
 ```
__Parameters:__

__newName :__ new name of channel you wish to give

__channelkey :__ channel key of your channel whom you are renaming.

__Return Type :__ BOOL

If renamed successfully then it will return YES else NO. 


#### 7. Check Admin

This method is to check whether the current user is channel/group admin or not.
As group admin have rights to do delete channel, remove  channel and add new member to channel. it is suggested to call this method to check admin rights before performing operations.
```
-(BOOL) checkAdmin:(NSNumber *) channelKey
```
__Parameters:__

__channelkey :__ channel key of your channel

__Return Type :__ BOOL

If renamed successfully then it will return YES else NO.                   








# APPLOZIC WEB PLUGIN     

### Overview      


Integrate messaging into your mobile apps and website without developing or maintaining any infrastructure. Sign up at https://www.applozic.com         


### Getting Started          





****Applozic messaging jQuery plugin****

Javascript chat and messaging plugin that lets you enable real time chat using websockets in your website without developing or maintaining any infrastructure.



Add Applozic messaging plugin into your web application :-


**Step 1: Sign up at  https://www.applozic.com/  to get the application key.**

**Step 2: For the standard user interface, add the following Applozic messaging plugin script file before **`</head>`** into your web page :- **              

```
<script type="text/javascript">
   (function(d, m){var s, h;       
   s = document.createElement("script");
   s.type = "text/javascript";
   s.async=true;
   s.src="https://apps.applozic.com/sidebox.app";
   h=document.getElementsByTagName('head')[0];
   h.appendChild(s);
   window.applozic=m;
   m.init=function(t){m._globals=t;}})(document, window.applozic || {});
</script>
```
 
**Step 3: Copy and paste below script before **`</body>`** to initialize plugin :-** 

``` 
<script type="text/javascript">
  window.applozic.init({userId: 'PUT_USERID_HERE', appId: 'PUT_APPLICATION_KEY_HERE', desktopNotification: true,  notificationIconLink: "PUT_LOGO_IMAGE_LINK_HERE"});
</script>
```    


Above options description :-    

```
 userId: 'UNIQUE USER ID OF ACTIVE USER'               // loggedIn user Id (required)   
 appId: 'YOUR APPLICATION KEY'                         // obtained from Step 1 (required)     
 desktopNotification: true or false                    // optional
 notificationIconLink : 'YOUR WEB APP LOGO'            // required for desktop notification (optional)                             
```

**Note** : desktopNotification support only for chrome browser, notificationIconLink will be display in desktop notification


**Step 4: Some additional options which you can configure while plugin initialization in Step 3 :-**

```
 1) onInit : 'PASS_YOUR_FUNCTION_NAME_HERE'                               // Type - FUNCTION (optional)
  Callback function which execute after plugin initialized. You can write your own logic inside this function to execute on plugin initialization. Example given in Step 5
 2) contactDisplayName: 'PASS_YOUR_FUNCTION_NAME_HERE'                    // Type - FUNCTION (optional)
  Function should return USER_DISPLAY_NAME by taking USERID as input parameter. Example given in Step 6        
 3) contactDisplayImage: 'PASS_YOUR_FUNCTION_NAME_HERE'                   //Type - FUNCTION (optional)
  Function should return USER_IMAGE_URL by taking USERID as a input parameter. Example given in Step 7
 4) accessToken: 'PASS_USER_ACCESS_TOKEN_HERE'                            //Type - String (optional)    
 Access token is to authenticate user from your end. To enable access token authentication you have to configure authentication url in admin dashboard. 
```
For more detail about access token, read :**https://www.applozic.com/developers.html#authentication-url**.


**Step 5: Sample code for **onInit()** function :-** 

You can write javascript function to execute your logic on plugin initialization -

Sample :     

 ```
  function onInit(response) {
      if (response === "success")
         {
            // write your logic here
         }
  };
  
  ```

Sample code for **CONTACT_JSON** used as a reference in Step 6 and Step 7 :-     

```
var CONTACT_JSON ={"USERID_1": {"displayName": "Devashish",
                      "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"},
                    "USERID_2": { "displayName": "Adarsh", "photoLink":    
                        "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                    "USERID_3": { "displayName": "Shanki", "photoLink":  
                        "https://www.applozic.com/resources/images/applozic_icon.png"}
                  }; 
 ```


**Step 6: Sample code for **contactDisplayName()** function :-** 

You  can write javascript function which return USER DISPLAY NAME on basis of userId

Sample :     

```   
 function contactDisplayName(USERID)  {                      
   var contact = CONTACT_JSON[USERID];               
        if (typeof contact !== 'undefined')             
          {                                      
           return contact.displayName;                  
         } 
 }                     
```

**Step 7: Sample code for **contactDisplayImage()** function :-** 

You can write javascript function to return USER IMAGE LINK on basis of userId 

Sample code -

```
  function contactDisplayImage(USERID)  {                        
    var contact =  CONTACT_JSON[USERID];                       
    if (typeof contact !== 'undefined')                      
      {                       
        return contact.photoLink;          
      }
  }                            
 ```

 
**Step 8: Function to **LOAD CONTACTS** (optional) :-**

If you want to load all contacts directly use below function - 
```
 $applozic.fn.applozic('loadContacts', 'PUT_CONTACT_LIST_JSON_HERE');
```

Sample code for **CONTACT_LIST_JSON** used as a reference in step 8 :-  

```
var CONTACT_LIST_JSON = 
          {"contacts": [{"userId": "USER_1", "displayName": "Devashish", 
                          "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                        {"userId": "USER_2", "displayName": "Adarsh", 
                          "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                        {"userId": "USER_3", "displayName": "Shanki",
                          "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}
                        ]
         };       

```

**NOTE**- Call **loadContacts** function only after plugin initailization. For reference use **init()** function explained in Step 5.

You don't need to use functions explained in Step 6 and Step 7 if loading all contacts dynamically as explaind in Step 8  

**Step 9: Function to load(open) individual tab conversation dynamically (optional) :-**

```
 $applozic.fn.applozic('loadTab', 'PUT_OTHER_USERID_HERE');  // user Id of other person with whom you want to open conversation 

 ``` 
 
**Step 10: Anchor tag or button to load(open) individual tab conversation directly (optional) :-**

You can add the following html into your code to directly open a conversation with any user -   

```
<a href="#" class="applozic-launcher" data-mck-id="PUT_OTHER_USERID_HERE" data-mck-name="PUT_OTHER_USER_DISPLAY_NAME_HERE">CHAT BUTTON</a>
 ```        
 
 **Note** - Data attribute **mck-name** is optional in above tag          
 
 
**Step 11: To add auto suggest users list in search field use below html element id (optional) :-** 

You can bind auto suggest plugin on input search field of id given below -      

```
mck-search 
```

**Step 12: To show **online/offline** status (optional) :- **

You can add the following attributes to your html element for real time online/offline status update -

Class Attributes - 
**mck-user-ol-status** and **n-vis**

Data Attribute - 
**mck-id**

Example -

```
<div class="mck-user-ol-status n-vis" data-mck-id='PUT_OTHER_USERID_HERE'></div>
```        

**Step 13: Topic or product based conversation (BUYER/SELLER CHAT) (optional) :-**


These are attributes requires on chat button or anchor tag -

Class Attribute -
**applozic-wt-launcher**

Data Attriutes - 
**mck-id ,mck-name** and **mck-topicid**


Example :-      

```
<a href="#" class="applozic-wt-launcher" data-mck-id="PUT_USERID_HERE" data-mck-name="PUT_DISPLAYNAME_HERE" data-mck-topicid="PUT_TOPICID_HERE">CHAT ON TOPIC</a>       
```         


Define callback function in your code to return topic(product) details on basis of topicId (detail should be in same JSON format as given below) :-           

```
function getTopicDetail(topicId) 
   {
      return TOPIC_DETAIL;  // object sample define below
   }
```

Json format of TOPIC_DETAIL :-

```
 var TOPIC_DETAIL= {'title': 'topic-title',      // Product title
                     'subtitle': 'sub-title',     // Product subTitle or Product Id
                     'link' :'image-link',        // Product image link
                     'key1':'key1' ,              // Small text anything like Qty (Optional)
                     'value1':'value1',           // Value of key1 ex-10 (number of quantity) Optional
                     'key2': 'key2',              // Small text anything like MRP (product price) (Optional)
                     'value2':'value2'            // Value of key2 ex-$100  (Optional)
                  };
 
```         
**NOTE** - Topic details will be displayed on conversation tab.

Additional options to configure in plugin initialize code in step 3 :- 

```
  getTopicDetail : 'PUT_YOUR_FUNCTION_NAME_HERE'    // Type - FUNCTION
  topicBox :  true or false                                     //  Set true if want to display topic details in conversation box
  
 ```

Sample code :-          

```
<script type="text/javascript">window.applozic.init({userId: 'PUT_USERID_HERE', appId: 'PUT_APPLICATION_KEY', getTopicDetail: getTopicDetail, topicBox : true});
</script>
```        


If want to send message about topic details directly on chat button click, then use class attribute **applozic-tm-launcher** in chat button instead of **applozic-wt-launcher**

Sample  code :-       

```
<a href="#" class="applozic-tm-launcher" data-mck-id="PUT_USERID_HERE" data-mck-name="PUT_DISPLAY_NAME_HERE" data-mck-topicid="PUT_TOPICID_HERE">Chat on topic</a>
```


**Step 14: Function to get **USER DETAIL** (optional) :-**

Call below given function to get user details like totalUnreadCount, lastSeenAt time etc -

```
  $applozic.fn.applozic('getUserDetail', {callback: getUserDetail});
```    

Callback function to receive response (used as a reference in above function) :-   


```
function getUserDetail(response) {
   if(response.status === 'success') {
      // write your logic
   }
}
```

Response Sample :-      

```
response = {'status' : 'success' ,                     // or error
            'data':  {'totalUnreadCount': 15           // total unread count for user          
                     'users':                          // Array of other users detail
                        [{"userId":"USERID_1","connected":false,"lastSeenAtTime":1453462368000,"createdAtTime":1452150981000,"unreadCount":3}, 
                        {"userId":"USERID_2","connected":false,"lastSeenAtTime":1452236884000,"createdAtTime":1452236884000,"unreadCount":1}]                  
                                
                     }
           }
```     


### Customization     



****Applozic messaging jQuery plugin****

Integrate messaging plugin into your web application.

A light weight jQuery plugin for integrating chat and messaging into your web page to directly send and receive messages to other users via **Applozic** messaging platform and also to see your latest conversations.


**Step 1: Sign up at https://www.applozic.com/  to get the application key.**


**Step 2: For UI customization, checkout  https://github.com/AppLozic/Applozic-Web-Plugin/tree/master/message/advanced 

Open  message.html file as a reference and add all scripts and html in your web page in same order as given in message.html.**


**Step 3: Initialize plugin using script given below (Initialize once page load completely, preferable in document.ready function) :-**  

```
  $applozic.fn.applozic({{userId: 'PUT_USERID_HERE', appId: 'PUT_APPLICATION_KEY_HERE', desktopNotification: true,  notificationIconLink: "PUT_LOGO_IMAGE_LINK_HERE"}); 
```

**Step 4: Configure value in above script :-**     

description - 

 ```
 userId: 'UNIQUE USER ID OF ACTIVE USER'                                   // loggedIn user Id (required)   
 appId: 'YOUR APPLICATION KEY'                                             // obtained from Step 1 (required)     
 desktopNotification: true or false                                        // optional
 notificationIconLink : 'YOUR WEB APP LOGO'                                // required for desktop notifications (optional)                                   
```
**Note** : desktopNotification support only for chrome browser, notificationIconLink will be display in desktop notification

**Step 5: Some additional options which you can configure while plugin initialization in Step 3 :-**


```
 1) onInit : 'PASS_YOUR_FUNCTION_NAME_HERE'                               // Type - FUNCTION (optional)
  Callback function which execute after plugin initialized. You can write your own logic inside this function to execute on plugin initialization. Example given in Step 6
 2) contactDisplayName: 'PASS_YOUR_FUNCTION_NAME_HERE'                    // Type - FUNCTION (optional)
  Function should return USER_DISPLAY_NAME by taking USERID as input parameter. Example given in Step 7        
 3) contactDisplayImage: 'PASS_YOUR_FUNCTION_NAME_HERE'                   //Type - FUNCTION (optional)
  Function should return USER_IMAGE_URL by taking USERID as a input parameter. Example given in Step 8
 4) accessToken: 'PASS_USER_ACCESS_TOKEN_HERE'                            //Type - String (optional)    
 Access token is to authenticate user from your end. To enable access token authentication you have to configure authentication url in admin dashboard. 
```
For more detail about access token, read :**https://www.applozic.com/developers.html#authentication-url**.

**Note** : Examples of callback functions and json format is given in below in step 7,8 and also given in message.html

**Step 6: Sample code for **onInit()** function :-** 

You can write javascript function to execute your logic after plugin initialization

Sample -     

 ```
  function onInit(response) {
    if (response === "success")
      {
        // write your logic here
      }
  };
  
```

Sample code for **CONTACT_JSON** used as a reference in Step 7 and Step 8 :-     

```
var CONTACT_JSON ={"USER_1": {"displayName": "Devashish",
                      "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"},
                    "USERID_2": { "displayName": "Adarsh", "photoLink":    
                        "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                    "USERID_3": { "displayName": "Shanki", "photoLink":  
                        "https://www.applozic.com/resources/images/applozic_icon.png"}
                  }; 
 ```


**Step 7: Sample code for **contactDisplayName()** function :- **

You  can write javascript function which return USER DISPLAY NAME on basis of userId

Sample :-     

```   
 function contactDisplayName(USERID)  {                      
   var contact = CONTACT_JSON[USERID];               
   if (typeof contact !== 'undefined')            
      {                                      
         return contact.displayName;                  
      } 
 }                     
```

**Step 8: Sample code for **contactDisplayImage()** function :- **

You can write javascript function to return USER IMAGE LINK on basis of userId 

Sample code :-

```
  function contactDisplayImage(USERID)  {                        
    var contact =  CONTACT_JSON[USERID];                       
    if (typeof contact !== 'undefined')                      
      {                       
        return contact.photoLink;          
      }
  }                            
 ```

 
** Step 9: Function to **LOAD CONTACTS** (optional) :-**

If you want to load all contacts directly use below function :- 
 
```
 $applozic.fn.applozic('loadContacts', 'PUT_CONTACT_LIST_JSON_HERE');
```

Sample code for **CONTACT_LIST_JSON** used as a reference in above script :-  

```
var CONTACT_LIST_JSON = 
          {"contacts": [{"userId": "USER_1", "displayName": "Devashish", 
                          "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                        {"userId": "USER_2", "displayName": "Adarsh", 
                          "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                        {"userId": "USER_3", "displayName": "Shanki",
                          "photoLink": "https://www.applozic.com/resources/images/applozic_icon.png"}
                        ]
         };       

```

**NOTE**- Call **loadContacts** function only after plugin initailization. For reference use **init()** function explained in Step 6.

You don't need to use functions explained in step 7 and step 8 if loading all contacts dynamically as explaind in step 9  


**Step 10 : To customize layout of plugin :-**

You can modify **mck-sidebox-1.0.css** class located at -      

``` 
  https://github.com/AppLozic/Applozic-Web-Plugin/blob/master/message/advanced/css/app/mck-sidebox-1.0.css 
```

**Step 11: To add auto suggest users list in search field (optional) :-**

You can bind auto suggest plugin on input search field with id given below -

```
mck-search 
```


**Step 12: Function to load(open) individual tab conversation dynamically (optional) :-**

```
 $applozic.fn.applozic('loadTab', 'PUT_OTHER_USERID_HERE');  // user Id of other person with whom you want to open conversation 

 ``` 
 
**Step 13: Anchor tag or button to load(open) individual tab conversation directly (optional) :-**

You can add the following html into your code to directly open a conversation with any user -   

```
<a href="#" class="applozic-launcher" data-mck-id="PUT_OTHER_USERID_HERE" data-mck-name="PUT_OTHER_USER_DISPLAY_NAME_HERE">CHAT BUTTON</a>
 ```        
 
 **Note** - Data attribute **mck-name** is optional in above tag.          
 

**Step 14: To show **online/offline** status (optional) :-**

You can add the following attributes to your html element for real time online/offline status update -

Class Attributes - **mck-user-ol-status** and **n-vis**

Data Attribute - **mck-id**

Example :-

```
<div class="mck-user-ol-status n-vis" data-mck-id='PUT_OTHER_USERID_HERE'></div>
```

**Step 15: Topic or product based conversation (BUYER/SELLER CHAT) (optional) :-**

These are attributes requires on chat button or anchor tag -

Class Attribute - **applozic-wt-launcher**

Data Attriutes - **mck-id, mck-name** and **mck-topicid**

Example :-
```
<a href="#" class="applozic-wt-launcher" data-mck-id="PUT_USERID_HERE" data-mck-name="PUT_DISPLAY_NAME_HERE" data-mck-topicid="PUT_TOPICID_HERE">CHAT ON TOPIC</a>       
```
Define callback function in your code to return topic(product) details on basis of topicId (detail should be in same JSON format as given below) :-

```
function getTopicDetail(topicId) 
  {
     return TOPIC_DETAIL;  // object sample define below
  }
```

JSON format of **TOPIC_DETAIL** :-

```
 var TOPIC_DETAIL={'title': 'topic-title',        // Product title
                     'subtitle': 'sub-title',     // Product subTitle or Product Id
                     'link' :'image-link',        // Product image link
                     'key1':'key1' ,              // Small text anything like Qty (Optional)
                     'value1':'value1',           // Value of key1 ex-10 (number of quantity) Optional
                     'key2': 'key2',              // Small text anything like MRP (product price) (Optional)
                     'value2':'value2'            // Value of key2 ex-$100  (Optional)
                  };

```

**NOTE** :- These detail will be displayed on conversation tab.


Additional options to configure in plugin initialize code in step 3 :-

```
  getTopicDetail : 'PUT_YOUR_FUNCTION_NAME_HERE'    // Type - FUNCTION
  topicBox :  true or false                        // Set true if want to display topic details in conversation box

```

Sample code to configure above options :-

```
<script type="text/javascript">window.applozic.init({userId: 'PUT_USERID_HERE', appId: 'PUT_APPLICATION_KEY', getTopicDetail: getTopicDetail, topicBox : true});
</script>
```

If you want to send message about topic details directly on chat button click, then use class attribute **applozic-tm-launcher** in chat button instead of **applozic-wt-launcher**

Sample code :-

```
<a href="#" class="applozic-tm-launcher" data-mck-id="PUT_USERID_HERE" data-mck-name="PUT_DISPLAY_NAME_HERE" data-mck-topicid="PUT_TOPICID_HERE">Chat on topic</a>
```

**Step 16: Function to get USER DETAIL  (optional) :-**

Call below given function to get user details like Total unread count, last seen at etc

```
  $applozic.fn.applozic('getUserDetail', {callback: getUserDetail});
```

Call below given function to get user details like totalUnreadCount, lastSeenAt time etc :-

```
function getUserDetail(response) {
   if(response.status === 'success') {
      // write your logic
   }
 }
```

Response sample :-

```
response = {'status' : 'success' ,                    // or error
            'data':{'totalUnreadCount' : 15           // total unread count for user          
                     users':                          // Array of other users detail
                       [{"userId":"USERID_1","connected":false,"lastSeenAtTime":1453462368000,"createdAtTime":1452150981000,"unreadCoun t":3}, 
                       {"userId":"USERID_2","connected":false,"lastSeenAtTime":1452236884000,"createdAtTime":1452236884000,"unreadCount":1}]                  
                     }
           }            
```

### Lightweight - Plugin                       



****Applozic light weight messaging jQuery plugin.****

Integrate messaging plugin into your web application.

Add Applozic messaging plugin into your web application for real time messaging communication 
via  Applozic functions. 

**Step 1: Sign up at  https://www.applozic.com/   to get the application key.**

**Step 2: For the standard user interface, add the following Applozic messaging plugin script file before **`</head>`** into your web page:   **              





```          
<script type="text/javascript" src="https://www.applozic.com/resources/lib/js/apz-notify.min.js"></script>      
<script type="text/javascript" src="https://www.applozic.com/resources/sidebox/js/app/apz-client-1.0.js"></script>        
```               


**Step 3: Initialize Plugin :- **
Create **APPLOZIC** instance by configuring your options            



```      
 var applozic = new APPLOZIC({'baseUrl': "https://apps.applozic.com",
                              'userId': 'PUT_USERID_HERE',                   // LoggedIn userId
                              'appId': 'PUT_APPLICATION_KEY_HERE',           // obtained from Step 1 (required)
                              'onInit': 'PASS_YOUR_FUNCTION_NAME_HERE'       // Type - FUNCTION (optional)
                            });        
```              
**Note** :- Initialize plugin on page load probably inside  **$(document).ready()**. 
function before **`</body>`** 

**onInit**  callback function execute after plugin initialized. You can write your own logic inside this function. Example given below

Sample code for **onInit()** function :-

Sample code -

```
  function onInit(response) {
    if (response === "success")
       {
         // write your logic here
       }
  };

```
On **`success`** response of above **onInit** callback function you can send and receive messages by calling Applozic functions directly as explained in Step 5 and Step 6 


**Step 4:  Subscribe to Applozic events and implement your own logic :-**         


Following are the events with example:                    

```        
applozic.events = {onConnect: function () {
                        console.log('connected successfully');
                  }, onConnectFailed: function () {
                       console.log('connection failed');
                  }, onMessageDelivered: function (obj) {
                       console.log('onMessageDelivered: ' + obj);
                  }, onMessageRead: function (obj) {
                       console.log('onMessageRead: '  + obj);
                  }, onMessageReceived: function (obj) {
                       console.log('onMessageReceived: ' + obj);
                  }, onMessageSentUpdate: function (obj) {
                       console.log('onMessageSentUpdate: ' + obj);
                  }, onUserConnect: function (obj) {
                       console.log('onUserConnect: ' + obj);
                  }, onUserDisconnect: function (obj) {
                       console.log('onUserDisconnect: ' + obj);
                  },
                };              
  ```               
  
  
**Events description**:

1) ** onConnect** : triggered when user subscribed successfully.      


2) **onConnectFailed** :  triggered when user failed to subscribe.         

3)  **onMessageDelivered** : triggered when message is delivered. Response contains message key.  Response object- {'messageKey': 'delivered-message-key'}.      


4) **onMessageRead** : triggered when delivered message is read on other end. Response contains message key.
 Response object - {'messageKey': 'delivered-message-key'}.       
 
 
5) **onMessageReceived** : triggered when new message received. Response contains message
Response object -  {'message': message}  // Message json format given in Step 6.         



6) **onMessageSentUpdate** : triggered when message sent successfully to server. Response contains messageKey.
 Response  object- {'messageKey': 'sent-message-key'}.      
 
 
 
7) **onUserConnect **: triggered when some other user comes online. Response contains user Id.
 Response object - {'userId': 'connected-user-Id'}           
 
 
 
8) **onUserDisconnect** : triggered when some other user goes offline. Response contains user Id.
Response object - {'userId': 'disconnected-user-id', 'lastSeenAtTime' : 'time in millsec'}           




**Step 5 : Send Message function :- **                 

```               
applozic.sendMessage(message, {'callback': sendMessageCallbackFunction});
```        

**message** json include :-         

```     
message = {'to': 'PUT_USERID_HERE',                          // receiver user id
           'message': 'PUT_MESSAGE_TEXT_HERE'                //  message text
          };     
```       

**sendMessageCallback()** response :-                   

```    
response = {'status' : 'success',                                     // or 'error'
            'message' : {'key': 'MESSAGE_IDENTIFIER',
                         'from': "SENDER_USERID",   
                         'to': 'RECEIVER_USERID',
                         'message': "MESSAGE_TEXT",
                         'type': 'outbox',
                         'timeStamp': 'MESSAGE_CREATED_TIMESTAMP'    // in milliseconds
                         'status': "MESSAGE__CURRENT_STATUS"        // (sent, delivered or read)
                        }                                 
           }        
```         



**Step 6:  Get **Message List** function :- **        

```
applozic.messageList(params, {'callback': messageListCallbackFunction});
```        

 **params** include :-           

 
 ```
 params = { 'id': 'PUT_USERID_HERE'};               // other userid with whom conversations fetch
 ```            
 
 **messageListCallbackFunction** response :-                

 
 ```
 response = {'status' : 'success',                     // or error
             'messages' :[]                           // Array of messages  (message format given below)     
           }
```         

**message** json format :-           

```
message = {key: "MESSAGE_IDENTIFIER",
           from: "SENDER_USERID",         
           to: 'RECEIVER_USERID',
           message: "MESSAGE_TEXT",
           type: 'inbox or outbox',
           status: "MESSAGE__CURRENT_STATUS",        // For outbox message  (sent, delivered or read)
                                                    // For inbox messsage (read, unread)
           timeStamp: 'MESSAGE_CREATED_TIMESTAMP'          
           }
```              
# PLATFORM API   

**For Platform API vist : https://www.applozic.com/platform.html ** 

#Message Fallback Time

Message Fallback Time is the duration in which if message is not delivered to end user then message will be delivered though mail as a fallback. For message fallback our api requires receiver user emailId which need to pass during registration and also you have to configure message delivery fallback time in dashboard for your app.  




#Webhook Url

Webhook Url is configured by application admin in Applozic Dashbaord for getting json of each message sent by one user to another.

**Response**: Response json received on configured url:


 ```  
{"key":"5-67f73984-2efe-4422-a522-d181cec5bd5d-1457958424015","from":"lee","to":"kevin","message":"hello","timeStamp":1457958424000}
 ```
 
#Authentication Url

Authentication Url is configured by application admin in Applozic Dashbaord for authenticating users from your side. The Url should accept POST request with following two paramters.
The user should provide the access token in the "accessToken" option while plugin initialization.

| Parameter  | Description |
| ------------- | ------------- |
| username | UserName of the user who should be authenticated |
| token | Access token for the specified user |

**Response**: Response text received on configured url:

 ```  
true : If user is authenticated
false : If user is not authenticated.
 ```


Source: https://www.applozic.com/developers.html
For more details, visit: https://www.applozic.com
