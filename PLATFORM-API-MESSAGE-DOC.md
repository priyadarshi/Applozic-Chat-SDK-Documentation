###Message API

#### Send Message

**Note** : API supported both by application admin and application user.

**SEND MESSAGE URL**: https://apps.applozic.com/rest/ws/message/v2/send

**Method Type**: POST

**Content-Type**: application/json

**Request Body**:

**Note** : Request body in case of **One to One message send**. 

**Json**                         
```
{
  "to":"John",
  "message":"Hi John"
}
```

**Json Parameter Description**: 

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| to  | Yes  |   | UserId to which you want to send message |
| message  | Yes  |   | Text Message |




**Note** : Request body in case of **Group message send**. 

**Json**                         
```
{
 "clientGroupId": "group Unique Identifier",  
  "message":"Hi John"
}
```


**Json Parameter Description**:

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId  | Yes  |   | Unique identifier of the group with respect to client |
| message  | Yes  |   | Text Message |




**Note** : In case of Application Admin  **ofUserId** request param required too.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | Yes (in case of admin only) |   |pass userId of user on which behalf admin want to create group    |

**Response** Same in both case: **One to One** and **Group Message Send**

**Json**
```
{
  "messageKey": "5-22bf4626-9019-4a4a-8565-6c0e40ecda96-1454398305364",
  "createdAt": 1454398305000
}
```

| Response Parameter  | Description |
| ------------- | ------------- |
| message key  | Request is successfully processed  |
| createdAt  | time in milliseconds |


####Message Metadata

To add metadata for a message, send the metadata object inside the message object while sending message. The same metadata object will be received in message list api with message object. The metadata object is a map with string keys and values.

**Sample Message Object Json with Metadata**:          

```json
{
  "to":"John",
  "message":"Hi John",
  "metadata" : {
    "key1" : "value1",
    "key2" : "value2"
  }
}
```

####Smart Messaging Using Metadata

Add specific metadata for a message, send the metadata object inside the message object while sending message. Message metadata type can be **HIDDEN**, **PUSHNOTIFICATION**, **ARCHIVE**.

**Sample Message Object Json with Metadata**:          

```json
{
  "to": "John",
  "message": "Hidden Message",
  "metadata": {
    "category": "HIDDEN"
  }
}
```

 
"category" value can be:

| value  |
| ------------- |
|  HIDDEN |
| PUSHNOTIFICATION |
| ARCHIVE|




#### Broadcast Message

**URL**: https://apps.applozic.com/rest/ws/message/sendall

**Method Type**: POST

**Content-Type**: application/json

**Request Body** :  

**Json**
```
{
  "userNames" : ["UserName1", "UserName2", "UserName3"],
  "clientGroupIds" : ["1", "2", "3"],
  "messageObject" : {
    "message":"Hi John"
  }
}
```

**Json Parameter Description**:

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userNames  | No  |   | User Names to which you want to send message. Limit 50 |
| clientGroupIds  | No  |   | List of Group unique identifiers to which you want to send message. Limit 50 |
| messageObject  | Yes  |   | Message Container Object |
| message  | Yes  |   | Text Message |

**Note** : In case of Application Admin  **ofUserId** request param required too.

**Request Parameter**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | Yes (in case of admin only) |   |pass userId of user on which behalf admin want to create group    |



**Response** : success Response Json to the request

####Message list

**URL**: https://apps.applozic.com/rest/ws/message/v2/list

**Method Type**: GET

**Description**

1. If no user id or group id is passed to the api then this api returns the latest message of the calling user with each user or group which the user has chat with.
2. If the user id is passed then api return the messages between the calling user and specified user.
3. If the group id is passed the api returns the messages of the specified group.

**Request Body**:        

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId  | No  |  | User Id of the user whose respective chat messages user want to fetch.  | 
| groupId  | No  |  | Group Id of the group for which messages need to be fetched. | 
| startIndex  | Yes  | 0  | Starting Index to fetch messages from list.  | 
| pageSize  | Yes  | 50  | Number of messages per page you want to fetch.  |
| endTime  | No  |   |Pass  oldest time from the fetched messages to load more older messages  |
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to call API |

**Note** : Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Note** : To load more older messages in list pass endTime parameter with oldest message time received in messages list.

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

**In Case of Error** :

| Response  | Description | 
| ------------- | ------------- | 
| error  | In case of any exception or error contact resolve@applozic.com  |


#### Message Info 

**Message Info URL**: https://apps.applozic.com/rest/ws/message/info

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| key | yes  |  | unique identifier of message|


**Example:** For API Call: 

```
https://apps.applozic.com/rest/ws/message/info?key=5-226299-1490015022917
```

**Response:**

**In case of One to One Message**:

**Note:** Suppose user1 sends a message to user2

```  
{
  "status": "success",
  "generatedAt": 1490168160713,
  "response": [
    {
      "userId": "user2",
      "deliveredAtTime": 1490168151068,
      "status": 4      // delivered to user2
    }
  ]
}
``` 


**In case of Group Message:

**Note:** Suppose user1 sends a message to group having users: user2, user3, user4

```  
{
  "status": "success",
  "generatedAt": 1490168526401,
  "response": [
    {
      "userId": "user2",
      "deliveredAtTime": 1490168482844,
      "status": 4     // delivered to user2
    },
    {
      "userId": "user3",
      "deliveredAtTime": 1490168483132,
      "readAtTime": 1490168523731,
      "status": 1    // read by user3
    }
  ]
}
```
**Note:** message is neither delivered nor read by user4.




#### Delete Message     

**DELETE MESSAGE  URL**: https://apps.applozic.com/rest/ws/message/delete

**Method Type**: GET 

**Parameters**:

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| key  | Yes  |   | Message unique key  |
| ofUserId  | No  |   |pass userId of user for which admin to delete message |

**Note** : Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Response**:        

| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processed  |
| error  |This will come if any exception occurs on server. In case of any exception contact resolve@applozic.com  |


#### Delete Conversation           

**DELETE CONVERSATION  URL** : https://apps.applozic.com/rest/ws/message/delete/conversation

**Method Type**: GET 

**Parameters**:          

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId  | No  |   | User for which you want to delete thread  |  
| groupId  | No  |   | Group for which you want to delete thread  |  
| ofUserId  | No  |   |pass userId of user on behalf of which application admin want to call API |

**Note** : Pass **ofUserId** only if application Admin calling the API on behalf of any user.

**Note** :

**1)** For Delete Conversation in Group send **groupId**  as a parameter.

**2)** For Delete Conversation in One to One Chat send **userId**  as a parameter.

**Response**:           

| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processed  |
| error  |This will come if any exception occurs on server or all the parameters are null. In case of any exception contact resolve@applozic.com  |




#### Delete User Messages Older Than X days

**Delete User Messages URL**: https://apps.applozic.com/rest/ws/user/messages/delete

**Method Type**: POST

**Request Parameters**:  

**Note**: Pass **ofUserId** only if application Admin calling the API.

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| days | Yes  |  | Delete chat history older than X days |
| ofUserId  | Yes (in case of  Application admin only) |   |pass userId of user for which admin want to delete messages.  |



**Response**: Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
```



#### Delete All Chats         

**DELETE All  URL** : https://apps.applozic.com/rest/ws/message/delete/all

**Method Type**: GET

**Note** : Request param **ofUserId** required for application admin purpose only.

**Parameters**:          

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| ofUserId  | No  |   | User for which application admin want to delete all messages  |  

**Response**:           

| Parameter  | Description | 
| ------------- | ------------- | 
| success  | Request is successfully processed  |
| error  |This will come if any exception occurs. In case of any exception contact resolve@applozic.com  |
