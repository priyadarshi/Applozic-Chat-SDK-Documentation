# PLATFORM API     

### Overview        


Integrate native app message communication to your product without developing and maintaining any infrastructure.
Are you looking for platform-native Sdks to integrate into your app. All you need to do is include the Applozic SDK as a library in your project and a couple of lines of code. We will take care of rest things from server hosting, database, maintenance to analytics.     


# Rest API       
 
 
 
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





** json **                         
```
{"userId":"robert","deviceType":"4","applicationId":"applozic-sample-app",
"registrationId":"put-gcm-registration-id-here", "pushNotificationFormat": "0"
}
```


**Response** : success Response Json to the request with following properties :-         



| Response  | Description |
| ------------- | ------------- |
| message | One of the following is returned: REGISTERED,REGISTERED.WITHOUTREGISTRATIONID, UPDATED |
| userKey | User key  |
| deviceKey  | User device key |
| lastSyncTime  | Time in miliseconds when user device last synced with server  |  
| currentTimeStamp  | Time in miliseconds when response is return from server | 




** json **                         
```
{    "message": "REGISTERED.WITHOUTREGISTRATIONID","userKey": "21fea543-2ade-494f-b905-6bab308d1b4f",
"deviceKey": "09c5d869-6d38-4d6b-9ebf-9de16cdab176","lastSyncTime": 1454328502029, "currentTimeStamp": 1454328502023}
```



***Note** :- **deviceKey** need to be stored and  sent in request header in each API call.




The following will come in response in case of incomplete email and invalid application key resepectively:




** json **                         
```
{  "message": "INCOMPLETE_EMAILID","currentTimeStamp": 1454328359265 }
```



** json **                         
```
{  "message": "INVALID_APPLICATIONID","currentTimeStamp": 1454328359295 }
```




****Authentication Headers From Device****    




Authentication is done using BASIC authentication.

Use **deviceKey** from above registration response to create Authorization Code and send **deviceKey** also  in request header.
 
**Authorization Code** : Basic Base64Encode of userId:deviceKey




**Example**- 
If the userId is **robert** and deviceKey is **09c5d869-6d38-4d6b-9ebf-9de16cdab176**, then the authorization code will be:

Authorization Code: Basic cm9iZXJ0OjA5YzVkODY5LTZkMzgtNGQ2Yi05ZWJmLTlkZTE2Y2RhYjE3Ng==




**All request from Device must contain the following 4 headers** -           


| Authorization: Authorization Code  |
| ------------- |
| UserId-Enabled:true |
| Application-Key:  Your Application Key  |  
| Device-Key:  received in registration response  | 





### Online Users List   

**Contact List URL**: https://apps.applozic.com/rest/ws/user/ol/list

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| pageSize  | No  |10   | list of user to be returned |


**Response:**
 ```  
{
  "mark": "true",
  "john": "true",
  "rachel": "true",
  "brett": "true",
  "kristen": "true",
  "robert": "false",
  "johnson": "false",
  "bob": "false",
  "liza": "false",
  "rohan": "false"
}

 ```
 
 
 **Note**

**1)** "true" means user is currently online, "false" means user is currently offline.





### Users display Name   

**Display Name  URL**: https://apps.applozic.com/rest/ws/user/info

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| userIds | yes  |  | list of unique userId |




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




#Message API



### Send   




**SEND MESSAGE URL**: https://apps.applozic.com/rest/ws/message/send

**Method Type**: POST

**Content-Type**: application/json

**Request Body**:


| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| to  | Yes  |   | UserId to which you want to send message |
| message  | Yes  |   | Text Message |



** sample **                         
```
{ "to":"John", "message":"Hi John" }
```



**Response**:-       



| Response  | Description |
| ------------- | ------------- |
| message key  | Request is successfully processed  |
| createdAt  | time in milliseconds |




** sample **                         
```
{ "messageKey": "5-22bf4626-9019-4a4a-8565-6c0e40ecda96-1454398305364",
  "createdAt": 1454398305000}
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



### List        

**MESSAGE LIST URL**: https://apps.applozic.com/rest/ws/message/list

**Method Type**: GET

**Request Body**:        

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| startIndex  | Yes  | 0  | Starting Index to fetch messages from list.  | 
| pageSize  | Yes  | 50  | Number of messages per page you want to fetch.  |
| startTime  | No  |   | Start Time from when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT.  |
| endTime  | No  |   | End Time upto when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT.  | 
 
 



**Note**: For fetching the next page of your message list startIndex value should be equal to the sum of pageSize value of all the previous calls.

**Response**:         




 ```  
{"message":[{"key":"5-35c2957b-8de0-482b-bea9-7c5c2e1dd2f4-1452080064726","userKey":"35c2957b-8de0-482b-bea9-7c5c2e1dd2f4","to":"michael","contactIds":"michael","message":"how are you","sent":true,"delivered":false,"read":false,"createdAtTime":1452080064000,"type":5,"source":1,"status":3,"pairedMessageKey":"4-35c2957b-8de0-482b-bea9-7c5c2e1dd2f4-1452080064726","contentType":0}]}      
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




**Note**:-


**1)** For Delete Conversation in Group send **groupId**  as a parameter.


**2)** For Delete Conversation in One to One Chat send **userId**  as a parameter.



**Response**:           




| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processedl  |
| error  |This will come if any exception occurs on server or all the parameters are null. In case of any exception contact contact@applozic.com  |
      



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
{"status":"success","generatedAt":1452342819495,"response":{"id":176,"name":"applozic","adminName":"nitin","membersName":["john","snow","krishi","lee"],"unreadCount":0,"type":2}}
```


### User's Group List



**LIST URL**:  https://apps.applozic.com/rest/ws/group/list 

**Method Type**: GET



**Parameters**:        



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| updatedAt | No  |   | lastSyncTime to the server  |
 


**Response**:   Response Json with success status :-         



 ```  
{"status":"success","generatedAt":1452345715245,"response":[{"id":177,"name":"Work-Group","adminName":"Marsh",
"membersName":["Kevin","Joe","Steve","Marsh"],"unreadCount":0,"type":2}]}   

 ```



**Note**: For the next sync call, pass "updatedAt" parameter to get details of only the modified group and newly added group of that user. Applozic API response contains "generatedAt" parameter which contains the timestamp at the time of server response. Use it as "updatedAt" for your next sync call.





### Delete 



**DELETE GROUP URL**:  https://apps.applozic.com/rest/ws/group/delete 

**Method Type**: GET



**Parameters**: 



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |



**Response**:  Json with success status :-  



 ```  
{"status":"success","generatedAt":1452347180639,"response":"success"}   

 ```



**Note**: Only Admin can delete the group otherwise the following error will come:

 ```  
{"status":"error","errorResponse":[{"errorCode":"AL-UN-01","description":"unauthorized user","displayMessage":"Unable to process"}],"generatedAt":1452348983616} 

 ```




### Remove Member 



**REMOVE GROUP MEMBER URL**:  https://apps.applozic.com/rest/ws/group/remove/member 

**Method Type**: GET



**Parameters**: 



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |
| userId   | Yes  |   | name of the user want to remove from group  |



**Response**:  Response Json  with success status :-  



 ```  
{"status":"success","generatedAt":1452347180639,"response":"success"}   

 ```



**Note**: Only Admin can remove the group member otherwise the following error will come:



 ```  
{"status":"error","errorResponse":[{"errorCode":"AL-UN-01","description":"unauthorized user","displayMessage":"Unable to process"}],"generatedAt":1452348983616} 

 ```


### Leave  



**LEAVE GROUP URL**:  https://apps.applozic.com/rest/ws/group/left 

**Method Type**: GET



**Parameters**: 



| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | Yes  |   | group unique id  |




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



**Response**: Response Json with success status :-  

 ```  
{"status":"success","generatedAt":1452347180639,"response":"success"}   

 ```

# Topic/Product API 


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
 

#Admin Api



 **Application To User**

Application can send automated in-app messages to users using Application to User Messaging API.


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




***Required Authentication Headers***



**request should contain these 3 headers**

| Header | Value  |
| ------------- | ----------- |
| Apz-Token | Authorization Code  |
| Apz-AppId | application key got in admin dashboard  |  
| Content-Type |  application/json  |  




Authentication is done using BASIC authentication. It is combination of email & password of admin user.


 
**Apz-Token** : Basic Base64Encode of email:password




**Example**- 

If the email of the admin(Logged in Applozic Dashboard) is  **jack** and password is **adminLoggedInApplozicDashboard**, 
then the Apz-Token will be:

Apz-Token: Basic amFjazphZG1pbkxvZ2dlZEluQXBwbG96aWNEYXNoYm9hcmQ=

Apz-AppId: application key of application for which admin want to send message. 

###User Details        

**URL**: https://apps.applozic.com/rest/ws/user/detail

**Method Type**: GET

**Content-Type**: application/json

**Parameters**:         

| Parameter  | Description |
| ------------- | ------------- |
| userIds | UserId for the user  |


**Response**: 

```
[
 {
  "userId": "UserId1", // UserId of the user (String)
  "userName": "Name1", // Name of the user (String)
  "connected": true, // Current connected status of user, if "connected": true that means user is online (boolean)
  "lastSeenAtTime": 123456789,  // Timestamp of the last seen time of user (long) 
  "imageLink": "http://image.url" // Image url of the user
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

***Required Authentication Headers***

**request should contain these 3 headers** -           

| Header | Value  |
| ------------- | ----------- |
| Apz-Token | Authorization Code  |
| Apz-AppId | application key got in admin dashboard  |  
| Content-Type |  application/json  |  


Authentication is done using BASIC authentication. It is combination of email & password of admin user.

**Apz-Token** : Basic Base64Encode of email:password


**Example**- 

If the email of the admin(Logged in Applozic Dashboard) is  **jack** and password is **adminLoggedInApplozicDashboard**, 
then the Apz-Token will be:

Apz-Token: Basic amFjazphZG1pbkxvZ2dlZEluQXBwbG96aWNEYXNoYm9hcmQ=

Apz-AppId: application key of application for which admin want to send message. 

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
 "message":"HI STEVE","senderName":"john", "to": "steve"   
}
```




**Response**:

| Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |


**sample response**
```
{"messageKey": "5-a97d66cd-67f9-42ba-aa61-a357455088ac-1456148218362", "createdAt": 1456148218000}
```







**Json required for contextual based messaging**




**json**
```
{
 "message":"Hello, I am interested in the product, can we chat?", "senderName":"john","to": "steve",
  "conversationPxy": {    "topicId":"prodct topic Id","topicDetail":"{\"title\":\"Product title\",\"subtitle\":\"subtitle of the product\",\"link\":\"product link url \",\"key1\":\" product Qty\",\"value1\":\"50\",\"key2\":\" product Price\",\"value2\":\"Rs.90\"}"    
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
{"messageKey":"5-a97d66cd-67f9-42ba-aa61-a357455088ac-1458039322283","conversationId":456,"createdAt":1458039322000}
```




***Required Authentication Headers***



**Request must contain the following 3 headers** -           

| Header | Value  |
| ------------- | ----------- |
| Apz-Token | Authorization Code  |
| Apz-AppId | application key got in admin dashboard  |  
| Content-Type |  application/json  |  



Authentication is done using BASIC authentication. It is combination of email & password of admin user .



**Apz-Token** : Basic Base64Encode of email:password




**Example**

If the email of the admin account used for registering to Applzoic is  **jack@gmail.com** and password is **test**, 
then the Apz-Token will be:

Apz-Token: Basic amFja0BnbWFpbC5jb206dGVzdA==

Apz-AppId: Application Key as shown in Applozic dashboard page.




  Contact us at ` github@applozic.com `
 
