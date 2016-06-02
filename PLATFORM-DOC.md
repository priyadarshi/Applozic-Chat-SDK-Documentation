Explore Platform API's as per Application Admin or as per Application User.

**Required Authentication Headers For APPLICATION ADMIN:**
For Application Admin send following authentication headers with each API call to explore platform API's.

**request should contain these 3 headers**

| Header | Value  |
| ------------- | ----------- |
| Apz-Token | Authorization Code  |
| Apz-AppId | application key got in admin dashboard  |  
| Content-Type |  application/json  |  

**Apz-Token** : Basic Base64Encode of "email:password"

Authentication is done using BASIC authentication. Authorization Code is combination of  base64 value of email & password of  application admin.

**Example**- 
If the email of the admin(Logged in Applozic Dashboard) is  **jack@gmail.com** and password is **adminLoggedInApplozicDashboard**, 
then the Apz-Token will be: Basic amFja0BnbWFpbC5jb206YWRtaW5Mb2dnZWRJbkFwcGxvemljRGFzaGJvYXJk

**Apz-Token**: 



**Required Authentication Headers For APPLICATION USER**  

Authentication is done using BASIC authentication.

Use **deviceKey** from registration response to create Authorization Code and send **deviceKey** also in request header.

**deviceKey** is received when application user does registration using register/client API.
 
**Authorization Code** : Basic Base64Encode of userId:deviceKey

**Example**- 
If the userId is **robert** and deviceKey is **09c5d869-6d38-4d6b-9ebf-9de16cdab176**, then the authorization code will be:

Authorization Code**: Basic cm9iZXJ0OjA5YzVkODY5LTZkMzgtNGQ2Yi05ZWJmLTlkZTE2Y2RhYjE3Ng==

**All request from Device must contain the following 4 headers** -           

| Authorization | Authorization Code  |
| ------------- | ------ |
| UserId-Enabled | true |
| Application-Key | Your Application Key  |  
| Device-Key | received in registration response  | 

**Note:** Headers are required in each API call except user registration .ie register/client API.

# User API

### Register     

**Registration URL**: https://apps.applozic.com/rest/ws/register/client

**Method Type**: POST

**Content-Type**: application/json

**Request body**:  Json with the following properties:        

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| userId  | Yes  |   | User name  |
| emailId  | No  | null  | User email address  |
| password  | No  | null  | User account password  |
| displayName  | No  |   | Name you want to display to other user  |  
| applicationId  | Yes  |   | Your Applozic Application key configured in dashboard  |
| deviceType  | Yes  |   | 1 for Android, 4 for Apple   | 
| registrationId  | No  |   | Device GCM or APN registration id for push notification  | 
| pushNotificationFormat  | No  |   | 0 for Standard (GCM/APN) and 1 for PhoneGap   | 
| userTypeId  | No  |   | to identify different-2 type of user within application  |
| contactNumber  | No  |   | user contact number    |

**json**                         
```
{
  "userId":"robert",
  "deviceType":"4",
  "applicationId": "applozic-sample-app",
  "registrationId":"put-gcm-registration-id-here", 
  "pushNotificationFormat": "0",
  "contactNumber":"+911234567890"
}
```

**Response** : success Response Json to the request with following properties :-         

| Response  | Description |
| ------------- | ------------- |
| message | One of the following is returned: REGISTERED,REGISTERED.WITHOUTREGISTRATIONID, UPDATED |
| userKey | User key  |
| deviceKey  | User device key |
| lastSyncTime  | Time in miliseconds when user device last synced with server  |  
| contactNumber  | user contact number, received only if passed  | 
| currentTimeStamp  | Time in miliseconds when response is return from server | 

**json**
```
{
  "message": "REGISTERED.WITHOUTREGISTRATIONID",
  "userKey": "21fea543-2ade-494f-b905-6bab308d1b4f",
  "deviceKey": "09c5d869-6d38-4d6b-9ebf-9de16cdab176",
  "lastSyncTime": 1454328502029,
  "contactNumber": "+911234567890",
  "currentTimeStamp": 1454328502023
}
```

***Note** :- **deviceKey** need to be stored and  sent in request header in each API call.

The following will come in response in case of incomplete email and invalid application key resepectively:

**json**
```
{
  "message": "INCOMPLETE_EMAILID",
  "currentTimeStamp": 1454328359265
}
```

**json**
```
{
  "message": "INVALID_APPLICATIONID",
  "currentTimeStamp": 1454328359295
}
```
**Note:** No header required for registration API.



### Load Contact List   

**CONTACT LIST URL**: http://apps.applozic.com/rest/ws/user/filter

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| pageSize | No  | 500 | list of contacts to load |
| startTime | No  |  | pass to load more contact |
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to call API |

**Note:**: Pass **ofUserId** only if application Admin calling the API on behalf of any user.




**Example:** For API Call: 

```
http://apps.applozic.com//rest/ws/user/filter?pageSize=20
```

**Response:**

```  
{
"users": [
{
"userId": "mark",
"connected": false,
"lastSeenAtTime": 1461559344000,
"createdAtTime": 1461559342000,
"unreadCount": 0,
"deactivated": false
},
{
"userId": "john",
"connected": true,
"lastSeenAtTime": 1460801797000,
"createdAtTime": 1460803509000,
"unreadCount": 0,
"displayName": "Edward",
"deactivated": false
},
{
"userId": "chris",
"connected": true,
"createdAtTime": 1460803509000,
"unreadCount": 0,
"displayName": "adam",
"imageLink": "https://www.applozic.com/resources/images/applozic_logo.gif",
"deactivated": false
}
(20 users detail list...)

],
"lastFetchTime": 1460803509000,
"totalUnreadCount": 0
}
```  


**Note**:To load further contact list use **lastFetchTime** value and pass it in **startTime** parameter from next time onwards.




### Users display Name   

**Display Name  URL**: https://apps.applozic.com/rest/ws/user/info

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| userIds | yes  |  | list of unique userId |


**Note:**: Additional **ofUserId**  parameter not required in case of application admin too.


**Example:** For API Call: 

```
http://apps.applozic.com/rest/ws/user/info?userIds=robert&userIds=john&userIds=mark
```

**Response:**

```  
{
  "robert": "robbie",
  "john": "Mitchell"
}
```  
 
**Note**

**1)** Only users having display Name will return in response.


###User Detail List       

**Note**: API supported both by application admin and application user. No additional parameter **ofUserId** required for Admin.

**URL**: https://apps.applozic.com/rest/ws/user/detail

**Method Type**: GET

**Content-Type**: application/json

**Parameters**:         

| Parameter | Required | Description |
| ------------- | ------------- |
| userIds |  No    |list of UserId of the user  |
| phoneNumbers | No      |list of phoneNumber of the user  |


**Note**: Pass either userIds or phoneNumbers 

**Response**: 

```
[
 {
  "userId": "UserId1", // UserId of the user (String)
  "userName": "Name1", // Name of the user (String)
  "connected": true, // Current connected status of user, if "connected": true that means user is online (boolean)
  "lastSeenAtTime": 123456789,  // Timestamp of the last seen time of user (long) 
  "imageLink": "http://image.url", // Image url of the user
   "phoneNumber": "+912345678954" // phone number of user
 },
 {
  "userId": "UserId1", // UserId of the user (String)
  "userName": "Name1", // Name of the user (String)
  "connected": true, // Current connected status of user (boolean)
  "lastSeenAtTime": 123456789,  // Timestamp of the last seen time of user (long) 
  "imageLink": "http://image.url" // Image url of the user
 }
]
```





#Message API

### Send   

**Note:** For Application user purpose only.

**SEND MESSAGE URL**: https://apps.applozic.com/rest/ws/message/send

**Method Type**: POST

**Content-Type**: application/json

**Request Body**:

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| to  | Yes  |   | UserId to which you want to send message |
| message  | Yes  |   | Text Message |

**sample**                         
```
{
  "to":"John",
  "message":"Hi John"
}
```

**Response**:-       

| Response  | Description |
| ------------- | ------------- |
| message key  | Request is successfully processed  |
| createdAt  | time in milliseconds |

**sample**
```
{
  "messageKey": "5-22bf4626-9019-4a4a-8565-6c0e40ecda96-1454398305364",
  "createdAt": 1454398305000
}
```

### Multi User Send 

**URL**: https://apps.applozic.com/rest/ws/message/sendall

**Method Type**: POST

**Content-Type**: application/json

**Request Body** :               

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userNames  | No  |   | User Names to which you want to send message |
| groupIds  | No  |   | Group Ids to which you want to send message |
| messageObject  | Yes  |   | Message Container Object |
| message  | Yes  |   | Text Message |

**sample**
```
{
  "userNames" : ["UserName1", "UserName2", "UserName3"],
  "groupIds" : [1, 2, 3],
  "messageObject" : {
    "message":"Hi John"
  }
}
```

**Response** :- success Response Json to the request

###MESSAGE LIST

**URL**: https://apps.applozic.com/rest/ws/message/list

**Method Type**: GET

**Description**

1. If no user id or group id is passed to the api then this api returns the latest message of the calling user with each user or group which the user has chat with.
2. If the user id or group id is passed then api return the messages between the calling user and specified user.
3. If the group id is passed the api returns the messages of the specified group.



**Request Body**:        

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId  | No  |  | User Id of the user whose respective chat messages user want to fetch.  | 
| groupId  | No  |  | Group Id of the group for which messages need to be fetched.  | 
| startIndex  | Yes  | 0  | Starting Index to fetch messages from list.  | 
| pageSize  | Yes  | 50  | Number of messages per page you want to fetch.  |
| startTime  | No  |   | Start Time from when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT.  |
| endTime  | No  |   | End Time upto when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT.  |
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to call API |

**Note:**: Pass **ofUserId** only if application Admin calling the API on behalf of any user.



**Note**: For fetching the next page of your message list startIndex value should be equal to the sum of pageSize value of all the previous calls.

**Response**:
```  
{
  "message":[
    {
      "key":"5-35c2957b-8de0-482b-bea9-7c5c2e1dd2f4-1452080064726",
      "userKey":"35c2957b-8de0-482b-bea9-7c5c2e1dd2f4",
      "to":"michael",
      "contactIds":"michael",
      "message":"how are you",
      "sent":true,
      "delivered":false,
      "read":false,
      "createdAtTime":1452080064000,
      "type":5,
      "source":1,
      "status":3,
      "pairedMessageKey":"4-35c2957b-8de0-482b-bea9-7c5c2e1dd2f4-1452080064726",
      "contentType":0
    }
  ]
}      
```

**In Case of Error**:-  

| Response  | Description | 
| ------------- | ------------- | 
| error  | In case of any exception or error contact devashish@applozic.com  |

### Delete      

**DELETE MESSAGE  URL**: https://apps.applozic.com/rest/ws/message/delete

**Method Type**: GET 

**Parameters**:

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| key  | Yes  |   | Message unique key  |
| ofUserId  | No  |   |pass userId of user for which admin to delete message |

**Note:**: Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Response**:        

| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processed  |
| error  |This will come if any exception occurs on server. In case of any exception contact devashish@applozic.com  |

### Delete Conversation           

**DELETE CONVERSATION  URL** : https://apps.applozic.com/rest/ws/message/delete/conversation

**Method Type**: GET 

**Parameters**:          

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId  | No  |   | User for which you want to delete thread  |  
| groupId  | No  |   | Group for which you want to delete thread  |  
| applicationKey  | No  |   | applicationKey configured in dashboard  |
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to call API |

**Note:**: Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Note**:-

**1)** For Delete Conversation in Group send **groupId**  as a parameter.

**2)** For Delete Conversation in One to One Chat send **userId**  as a parameter.

**Response**:           

| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processedl  |
| error  |This will come if any exception occurs on server or all the parameters are null. In case of any exception contact contact@applozic.com  |

### Delete All           

**DELETE All  URL** : https://apps.applozic.com/rest/ws/message/delete/all

**Method Type**: GET

**Note:** Request param **ofUserId** required for application admin purpose only.

**Parameters**:          

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | No  |   | User for which application admin want to delete all messages  |  

**Response**:           

| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processed  |
| error  |This will come if any exception occurs. In case of any exception contact contact@applozic.com  |

# Group API

### Creation

**GROUP CREATION URL**: https://apps.applozic.com/rest/ws/group/create 

**Method Type**: POST 

**ContentType**: application/json


**Request Body**:   

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupName | Yes  |   | Name of the group |
| groupMemberList | Yes  |   |List of names of the  group members |
| type | No  | public  | Type of the group |

"type" parameters possible values

| Value  | Description |
| ------------- | ------------- |
| 1 | Private group : other users are not able to join this group voluntarily |
| 2 | Public Group : Users are able to search and join the group |
| 5 | Broadcast Group : User can send personal message to a group of Users |


**Note:** In case of Application Admin  **ofUserId** request param required too.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | Yes (in case of admin only) |   |pass userId of user on which behalf admin want to create group    |
    
**Parameter Example**:   (Suppose "TestUser" is the user calling group creation API)

**sample**  
```
{
  "groupName" : "Group Name",
  "groupMemberList" : ["UserName1", "UserName2", "UserName3"]
}
```

**Response** : Response Json  with success status :-  

**json**                         
```
{
  "status":"success",
  "generatedAt":1452342819495,
  "response":{
    "id":176,
    "name":"applozic",
    "adminName":"nitin",
    "membersName":["john","snow","krishi","lee"],
    "unreadCount":0,
    "type":2
  }
}
```

### User's Group List

**LIST URL**:  https://apps.applozic.com/rest/ws/group/list 

**Method Type**: GET

**Parameters**:        

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| updatedAt | No  |   | lastSyncTime to the server  |
| ofUserId  | No  |   |pass userId of user for which admin want to load the group list   |

**Note:**: Pass ofUserId only if application Admin calling the API on behalf of any user.

**Response**:   Response Json with success status :-         

```
{
  "status":"success",
  "generatedAt":1452345715245,
  "response":[
    {
      "id":177,
      "name":"Work-Group",
      "adminName":"Marsh","membersName":["Kevin","Joe","Steve","Marsh"],
      "unreadCount":0,"type":2
    }
  ]
}   
```

**Note**: For the next sync call, pass "updatedAt" parameter to get details of only the modified group and newly added group of that user. Applozic API response contains "generatedAt" parameter which contains the timestamp at the time of server response. Use it as "updatedAt" for your next sync call.

### Delete 

**DELETE GROUP URL**:  https://apps.applozic.com/rest/ws/group/delete 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |
| ofUserId  | No  |   |pass userId of group admin user for which application admin want to delete the group   |

**Note:**: Pass ofUserId only if application Admin calling the API on behalf of group admin user.

**Response**:  Json with success status :-  

```
{"status":"success","generatedAt":1452347180639,"response":"success"}   
```

**Note**: Only Group Admin can delete the group otherwise the following error will come:

```
{
  "status":"error",
  "errorResponse":[
    {
      "errorCode":"AL-UN-01",
      "description":"unauthorized user",
      "displayMessage":"Unable to process"
    }
  ],
  "generatedAt":1452348983616
}
```

### Remove Member 

**REMOVE GROUP MEMBER URL**:  https://apps.applozic.com/rest/ws/group/remove/member 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |
| userId   | Yes  |   | userId of the user want to remove from group  |
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to remove member |

**Note:**: Pass ofUserId only if application Admin calling the API on behalf of any user.

**Response**:  Response Json  with success status :-  

```  
{"status":"success","generatedAt":1452347180639,"response":"success"}
```

**Note**: Only Admin can remove the group member otherwise the following error will come:

```  
{
  "status":"error",
  "errorResponse":[
    {
      "errorCode":"AL-UN-01",
      "description":"unauthorized user",
      "displayMessage":"Unable to process"
    }
  ],
  "generatedAt":1452348983616
}
```

### Leave  

**LEAVE GROUP URL**:  https://apps.applozic.com/rest/ws/group/left 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |
| ofUserId  | No  |   |pass userId of user application admin want to remove |

**Note:**: Pass ofUserId only if application Admin calling the API on behalf of any user.

**Response**: Response Json with success status :-  

```  
{"status":"success","generatedAt":1452347180639,"response":"success"}
```

### Add Member

**ADD GROUP MEMBER URL**:  https://apps.applozic.com/rest/ws/group/add/member 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |
| userId   | Yes  |   | name of the user want to add to the group  |
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to add member  |

**Note:**: Pass ofUserId only if application Admin calling the API on behalf of any user.

**Response**:  Response Json with success status :-  

```  
{"status":"success","generatedAt":1452347180639,"response":"success"}
```

### Change Name

**CHANGE GROUP NAME URL**:  https://apps.applozic.com/rest/ws/group/change/name 

**Method Type**: POST

**ContentType**: application/json

**Request Body**:  

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId| Yes  |   | group unique id |
| newName | Yes  |   |new name of group |
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to change group name |

**Note:**: Pass ofUserId only if application Admin calling the API on behalf of any user.

**Response**: Response Json with success status :-  

```  
{"status":"success","generatedAt":1452347180639,"response":"success"}
```

### Check User : check user exist in a group or not

**CHECK USER URL**:  https://apps.applozic.com/rest/ws/group/check/user 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |
| userId   | Yes  |   | userId of the user identify in group  |
| ofUserId  | No  |   |pass userId of user exist in a group on behalf of which application admin want to check other user  |

**Note:**: Pass ofUserId only if application Admin calling the API on behalf of any user.

**Response**:  API response: in case of success:-  

```  
{
"status": "success","generatedAt": 1463673355057,"response": true/false
}
```



### Multiple Group Creation

**MULTIPLE GROUP CREATION URL**: https://apps.applozic.com/rest/ws/group/create/multiple

**Method Type**: POST 

**ContentType**: application/json

**Request Body**:   

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupName | Yes  |   | Name of the group |
| groupMemberList | Yes  |   |List of names of the  group members |
| type | No  | public  | Type of the group |

"type" parameters possible values

| Value  | Description |
| ------------- | ------------- |
| 1 | Private group : other users are not able to join this group voluntarily |
| 2 | Public Group : Users are able to search and join the group |
| 5 | Broadcast Group : User can send personal message to a group of Users |

**Note:** In case of Application Admin  **ofUserId** request param required too.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | Yes (in case of admin only) |   |pass userId of user on which behalf admin want to create  multiple group    |
    
**Parameter Example**:   (Suppose "TestUser" is the user calling group creation API)

**sample**  
```
 [
 { "groupName" : "MultiGroup1",
  "groupMemberList" : [ "kevin","john"]
 },
 { "groupName" : "MultiGroup2",
  "groupMemberList" : [ "jade"]
 }
 
]

```

**Response** : Response Json  with success status :-  

**json**                         
```
{
  "status": "success",
  "generatedAt": 1464793892242,
  "response": [
    {
      "id": 496,
      "groupId": "496",
      "name": "MultiGroup1",
      "adminName": "TestUser",
      "membersName": [
        "kevin",
        "TestUser",
        "john"
      ],
      "users": [
        {
          "id": "1d18ac83-5e00-4663-bdb8-91cc1354b63d",
          "userId": "John",
          "connected": false,
          "createdAtTime": 1457714415000,
          "unreadCount": 0,
          "deactivated": false
        },
        {
          "id": "8bb2f211-1083-4032-8187-5bc6db1c2080",
          "userId": "kevin",
          "connected": true,
          "lastSeenAtTime": 1457449548000,
          "createdAtTime": 1457449539000,
          "unreadCount": 0,
          "phoneNumber": "+912345678923",
          "deactivated": false
        }
      ],
      "unreadCount": 0,
      "type": 2
    },
    {
      "id": 497,
      "groupId": "497",
      "name": "MultiGroup2",
      "adminName": "TestUser",
      "membersName": [
        "TestUser",
        "jade"
      ],
      "users": [
        {
          "id": "39fcf05f-572d-4efb-8e34-8a4004f1bb37",
          "userId": "jade",
          "connected": false,
          "createdAtTime": 1464681811000,
          "unreadCount": 0,
          "deactivated": false
        }
      ],
      "unreadCount": 0,
      "type": 2
    }
  ]
}
```




### Add User To Multiple Group

**ADD USER TO MULTIPLE GROUP URL**:  https://apps.applozic.com/rest/ws/group/add/user

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupIds   | Yes  |   | List of group unique id  |
| userId   | Yes  |   | unique id of the user want to add to the group  |
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to add member  |

**Note:**: Pass ofUserId only if application Admin calling the API on behalf of any user.


**sample**  
```
https://apps.applozic.com/rest/ws/group/add/user?groupIds=490&groupIds=491&groupIds=493&userId=jack
```


**Response**:  Response Json with success status :-  

```  
{"status":"success","generatedAt":1452347180639,"response":"success"}
```

**Note**: Groups for the passed groupIds and the user for the passed userId should exist in that application.





#Topic/Product API 

### Retreive Conversation Id

**URL**: https://apps.applozic.com/rest/ws/conversation/id

**Method Type**: POST

**Content-Type**: application/json

**Request Body**
```
{
  "topicId" : "Topic id of the conversation",
  "topicDetail" : "Topic detail of the conversation",
  "applicationKey" : "Application key",
  "userId" : "unique id of the receiver user", // or "groupId": "groupId  receive from group creation API"
  "status" : "Status flag of the conversation"
}
```

**Note**

1.In case of One to One chat  pass **userId**  and in case of group chat pass **groupId** in request body.

**Behavior**

1. Call retrieve conversation API with Status flag as NEW, OPEN, DEFAULT.

2. If no conversation is found, new conversation will be created.

Status Behavior

NEW: The previous conversation will get ended and new conversation will be created.

OPEN: If the conversation is closed, it will be re-opened.

DEFAULT: return the conversation as it is.

***Required Authentication Headers***

**request should contain these 3 headers** -

| Header | Value |
| ------------- | ------------ |
| Authorization | Authorization Code  |
| UserId-Enabled | true |
| Application-Key | Your Application Key  |  
| Device-Key | Received in registration response  | 

Authentication is done using BASIC authentication. It is combination of email & password of admin user .

**Response**:  success Response Json to the request
```
{
  "status" : "success",
  "response" : {
    "id" : Group Id (integer),
    "name" : "Group Name",
    "adminName" : "Group Admin User Name",
    "membersName" : [ List of members user names],
    "unreadCount" : (Int) message unread count for the logged in user,
    "type" : Group type,
    "conversationPxy" : {
      "id" : (Int)Conversation id,
      "topicId" : "Topic id of the conversation",
      "topicDetail" : "Topic Detail for the conversation",
      "created" : (true/false) if the conversation is created or not in this api,
      "closed" : (true/false) if the conversation is closed,
      "groupId" : (Int) Group id of the respected group,
    }
  }
}
```

# Block/Unblock API

### Block User     

**BLOCK USER  URL**: https://apps.applozic.com/rest/ws/user/block

**Method Type**: GET 

**Parameters**:         

| Parameter  | Response | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId | Yes  |   |pass unique id of user you want to block  |

**Response**:  Response Json with success status :-  

```
{"status":"success","generatedAt":1452347180639,"response":"success"}   
```

### Unblock User    

**UNBLOCK USER  URL**: https://apps.applozic.com/rest/ws/user/unblock

**Method Type**: GET 

**Parameters**:         

| Parameter  | Response | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId | Yes  |   |pass unique id of user you want to unblock  |

**Response**:  Response Json with success status :-  

```  
{"status":"success","generatedAt":1452347180639,"response":"success"}   
``` 

### API's for application admin purpose only

**Application To User**

Application can send automated in-app messages to users using Application to User Messaging API.

**Note:** Send authentication headers in API call  mention in section-1.

### Create User        

**URL**: https://apps.applozic.com/rest/ws/user/create

**Method Type**: POST

**Content-Type**: application/json

**Response**: 

```
{"Success"}
```

**Request Body**                         
```
{
  "userId": "DemoUser", 
  "displayName": "Display Demo User Name", 
  "imageLink": "User profile image url", 
  "email": "User Email", 
  "createdAt": 1456148218000
}
```





###Dispatch Message      

**DISPATCH MESSAGE URL**: https://apps.applozic.com/rest/ws/message/dispatch

**Method Type**: POST

**Content-Type**: application/json

**Request body**:  Json with the following properties: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| senderName | Yes  |   | unique Id of  message sender user  |
| to | Yes  |   | unique Id of message receiver user  |
| message  | Yes |   | message content to be passed  |
| oldTimestamp  | No |   | create message  timestamp   |

**sample request**
```
{
  "message":"HI STEVE",
  "senderName":"john",
  "to": "steve"   
}
```

**Response**:

| Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |

**sample response**
```
{
  "messageKey": "5-a97d66cd-67f9-42ba-aa61-a357455088ac-1456148218362",
  "createdAt": 1456148218000
}
```

**Json required for group based messaging**

**json**
```
{
  "message":"message content",
  "groupId":114209 //groupId received while group creation.
}
```

**Response**:

| Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |

**sample response**
```
{
  "messageKey": "5-agpzfmFwcGxvemljchMLEgZTdVVzZXIYgICAgLrcvwsM-1464093115599",
  "createdAt": 1456148218000
}
```

**Json required for contextual based messaging**

**json**
```
{
  "message":"Hello, I am interested in the product, can we chat?",
  "senderName":"john",
  "to": "steve",
  "conversationPxy": {
    "topicId":"prodct topic Id",
    "topicDetail": "topic detail string"    
  }   
}
```

**Response**:      

| Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |
| conversationId | open conversation to chat on topic |

**json**
```
{
  "messageKey":"5-a97d66cd-67f9-42ba-aa61-a357455088ac-1458039322283",
  "conversationId":456,
  "createdAt":1458039322000
}
```

Contact us at ` github@applozic.com `
