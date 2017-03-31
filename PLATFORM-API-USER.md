### User API

#### Login/Register User     

**Registration URL**: https://apps.applozic.com/rest/ws/register/client

**Method Type**: POST

**Content-Type**: application/json

**Request body**:  

**Json**                         
```
{
  "userId":"robert",
  "deviceType":"4",
  "applicationId":"applozic-sample-app",
  "registrationId":"put-gcm-registration-id-here", 
  "pushNotificationFormat": "0",
  "contactNumber":"+911234567890"
}
```

**Json Parameter Description**:

| Json Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| userId  | Yes  |   | User name  |
| email  | No  | null  | User email address  |
| password  | No  | null  | User account password  |
| displayName  | No  |   | Name you want to display to other user  |  
| applicationId  | Yes  |   | Your Applozic Application key configured in dashboard  |
| deviceType  | Yes  |   | 1 for Android, 4 for Apple   | 
| registrationId  | No  |   | Device GCM or APN registration id for push notification  | 
| pushNotificationFormat  | No  |   | 0 for Standard (GCM/APN) and 1 for PhoneGap   | 
| userTypeId  | No  |   | to identify different-2 type of user within application  |
| contactNumber  | No  |   | user contact number    |



**Response** : Success Response Json to the request with following properties :-   


**Json**
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

| Response Parameter  | Description |
| ------------- | ------------- |
| message | One of the following is returned: REGISTERED,REGISTERED.WITHOUTREGISTRATIONID, UPDATED |
| userKey | User key  |
| deviceKey  | User device key |
| lastSyncTime  | Time in miliseconds when user device last synced with server  |  
| contactNumber  | user contact number, received only if passed  | 
| currentTimeStamp  | Time in miliseconds when response is return from server | 


**Note** : **deviceKey** need to be stored and  sent in request header in each API call.

The following will come in response in case of no userId or application key passed:

**Json**
```
{
  "message": "INVALID_PARAMETER",
  "currentTimeStamp": 1454328359265
}
```

The following will come in response in case of no application found with the passed application key:

**Json** 
```
{
  "message": "INVALID_APPLICATIONID",
  "currentTimeStamp": 1454328359295
}
```
**Note** : No header required for registration API.


####User Details       

**Note** : API supported both by application admin and application user. No additional parameter **ofUserId** required for Admin.

**URL**: https://apps.applozic.com/rest/ws/user/v2/detail

**Method Type**: POST

**Content-Type**: application/json

**Json Example**                         
```
{ 
"userIdList" : ["userId1","userId2"]
}
```

**Json Parameter Description** 

|Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userIdList   | No  |   | List of userIds  |
| phoneNumberList | No  |   | List of phoneNumbers |

**Note**: Pass either userIdList or phoneNumberList

**Response**: 

```
[
 {
  "userId": "UserId1", // UserId of the user (String)
  "userName": "Name1", // Name of the user (String)
  "connected": true, // Current connected status of user, if "connected": true that means user is online (boolean)
  "lastSeenAtTime": 12345679,  // Timestamp of the last seen time of user (long)
  "createdAtTime": 148339090, //  Timestamp of the user's creation (long)
  "imageLink": "http://image.url", // Image url of the user
  "deactivated": false,   // user active/inactive status (boolean)
  "phoneNumber": "+912345678954", // phone number of user
  "unreadCount": 10,  // total unread message count
  "lastLoggedInAtTime": 1483342919147, //  Timestamp of the user's last logged in (long)
  "lastMessageAtTime": 1483343150550  //  Timestamp of the user's last message (long)
 },
 {
  "userId": "UserId2", // UserId of the user (String)
  "userName": "Name2", // Name of the user (String)
  "connected": true, // Current connected status of user (boolean)
  "lastSeenAtTime": 123456789,  // Timestamp of the last seen time of user (long) 
  "imageLink": "http://image.url" // Image url of the user
 }
]
```

#### Update User

**UPDATE User URL**: https://apps.applozic.com/rest/ws/user/update 

**Method Type**: POST

**ContentType**: application/json

**Request Body**:  

**Json**                         
```
{
  { "email" : "user email",
  "displayName" : "user display name",
  "imageLink" : "User profile image url",
  "statusMessage": "status Message"
 }
}
```
**Json Parameter Description** 

|Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| email   | No  |   | user email  |
| displayName | No  |   | display name of user |
| imageLink | No  |   | image link of the user |
| statusMessage | No  |   | status message of user |


**Note**: Pass **ofUserId** only if application Admin calling the API.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | Yes (in case of admin only) |   |pass userId of user for which admin want to update details.  |

**Response**: Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
```


#### Update User Password  

**Note**: User can update own password using API.

**Update Password  URL**: https://apps.applozic.com/rest/ws/user/update/password

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| oldPassword | yes  |  | existing password |
| newPassword | yes  |  | new password |



**Example:** For API Call: 

```
http://apps.applozic.com/rest/ws/user/update/password?oldPassword=12345&newPassword=1234567
```

**Response:**

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
``` 




#####Contact List   

**CONTACT LIST URL**: http://apps.applozic.com/rest/ws/user/filter

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| pageSize | No  | 500 | list of contacts to load |
| startTime | No  |  | pass to load more contact |
| userId  | No  |   | pass userId of user for which information has to be retrieved |
| role  | No  |   | pass role of users for which information has to be retrieved |


Roles:

| Parameter  |
| ------------- |
| BOT |
| USER |

**Example:** For API Call: 

```
http://apps.applozic.com/rest/ws/user/filter?pageSize=20
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

**Note** : To load further contact list use **lastFetchTime** value and pass it in **startTime** parameter from next time onwards.
