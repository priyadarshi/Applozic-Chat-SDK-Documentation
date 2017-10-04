API's for application admin purpose only

**Application To User**

Application can send automated in-app messages to users using Application to User Messaging API.

**Note** : Send authentication headers in API call required by Application Admin.

#### Create User        

**URL**: https://apps.applozic.com/rest/ws/user/v2/create

**Method Type**: POST

**Content-Type**: application/json

**Request Body**:

**Json**
```
{
  "userId": "DemoUser", 
  "password": "Demo User password",
  "displayName": "Display Demo User Name", 
  "imageLink": "User profile image url", 
  "email": "User Email", 
  "createdAtTime": 1456148218000, // if want to create user on specific time
   "roleName":"BOT" // if want to create application Bot user
}
```

**Json Parameter Description**:

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId | Yes  |   |pass unique id of user  |
| password | No  |   |password of user  |
| displayName | No  |   |display name of user  |
| imageLink | No |   |image link of user  |
| email | No  |   |email of user  |
| createdAtTime | No  |   |time in miliseconds  |
| authenticationTypeId | No  | 0  |used for user authentication  |
| roleName | No  | USER  | want to create user of specific type then pass: BOT  |

Roles:

| Parameter  |
| ------------- |
| BOT |
| USER |

Authentication:

| Parameter Name  |Value |Description|
| ------------- |-------|-----------|
| authenticationTypeId |0 |Verification from client side|
| authenticationTypeId |1 |Verification from applozic using password|

**Note** :

**1)** User password is required in case of **BOT** User creation.

**2)** By default role is **USER** if roleName is not passed.

 


**Response**: 

```
{
  "status": "success",
  "generatedAt": 1470903020662,
  "response": "success"
}
```



#### Set User Password  

**Note**: Application admin can set any user password.

**Set User Password  URL**: https://apps.applozic.com/rest/ws/user/set/password

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| userId | yes  |  | unique identifier for user |
| password | yes  |  |  password for user |



**Example:** For API Call: 

```
http://apps.applozic.com/rest/ws/user/set/password?userId=jack&password=1234567
```

**Response:**

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
``` 



#### Merge Users

**Note** : API supported only by application admin. No additional header **Of-User-Id** required for Admin.

**URL**: https://apps.applozic.com/rest/ws/user/merge?userId=user1&mergeUserId=user2

**Method Type**: GET

**Content-Type**: application/json

**Parameters**:         

| Parameter | Required | Description |
| --------- | -------  | ----------- |
| userId |  Yes | UserId of the user in which data will be merged  |
| mergeUserId | Yes | UserId of the user which will be merged  |

**Response**:           

| Parameter  | Description | 
| ------------- | ------------- | 
| success | Request is successfully processed  |
| error |This will come if any exception occurs on server or all the parameters are null. In case of any exception contact resolve@applozic.com  |


#### Delete User

**DELETE USER URL**: https://apps.applozic.com/rest/ws/user/delete 

**Method Type**: POST

**ContentType**: application/json

 **Note**: Pass **Of-User-Id** header. **Of-User-Id** is the userId of the user to which application admin want to delete .


**Response**: Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
```


### Dispatch Message   

**DISPATCH MESSAGE URL**: https://apps.applozic.com/rest/ws/message/dispatch

**Description** : 

1.Message Dispatch API behave same as Message Send API, but used by Application Admin.

2.Message Dispatch API supports One to One, group based and contextual based messaging.

3.Application Admin can send Message on behalf of one user to another user on back date also. (Used for data migration from your Server to Applozic Sever)

**Method Type**: POST

**Content-Type**: application/json

**Request body**:  

**Json required for One to One based messaging**:

**Json**
```
{
  "message":"HI STEVE",
  "senderName":"john",
  "to": "steve"   
}

```

**Json Parameter Description**:

|Json Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| senderName | Yes  |   | unique Id of  message sender user  |
| to | Yes  |   | unique Id of message receiver user  |
| message  | Yes |   | message content to be passed  |
| oldTimestamp  | No |   | create message  timestamp   |



**Response**:



**Json**
```
{
  "messageKey": "5-a97d66cd-67f9-42ba-aa61-a357455088ac-1456148218362",
  "createdAt": 1456148218000
}
```

| Response Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |

**Json required for group based messaging**:

**Json**
```
{
  "message":"message content",
  "groupId":114209 //groupId received while group creation.
}
```

**Response**:



**Json**
```
{
  "messageKey": "5-agpzfmFwcGxvemljchMLEgZTdVVzZXIYgICAgLrcvwsM-1464093115599",
  "createdAt": 1456148218000
}
```

| Response Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |

**Json required for contextual based messaging**:

**Json**
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



**Json**
```
{
  "messageKey":"5-a97d66cd-67f9-42ba-aa61-a357455088ac-1458039322283",
  "conversationId":456,
  "createdAt":1458039322000
}
```

| Response Parameters  | Description |
| ------------- | ------------- |
| messageKey |message key  |
| createdAt | Time in miliseconds when response is return from server |
| conversationId | open conversation to chat on topic |



#### Close Topic/Product based Conversation

**CLOSE TOPIC/PRODUCT BASED CONVERSATION**:  https://apps.applozic.com/rest/ws/conversation/closeall

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| topicId  | Yes  |   |List of unique topic id of the conversation  |
| userId  | No  |   | unique user identifier   |
| withUserId  | No  |   | unique user identifier   |


**Note** :

**1)** Pass  only list of topicId to close all the conversations regarding that topicIds.

**2)** Pass all three parameters (**topicId**,**userId**,**withUserId**) to close any specific Conversation on certain topic between two user.


**Response**:  Response String with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```

#### Message History Export

**Note** : API supported only by application admin. No additional header **Of-User-Id** required for Admin.

**URL**: https://apps.applozic.com/rest/ws/analytics/message

**Method Type**: GET

**Content-Type**: application/json

**Accept**:

1. application/json (Default) : For return type as json
2. application/octet-stream : For returning as Excel.

**Parameters**:         

| Parameter | Required | Description |
| --------- | -------  | ----------- |
| applicationId | Yes | Your Applozic Application key configured in dashboard |
| startIndex | No | Starting Index to fetch messages from list |
| pageSize | No | Number of messages per page you want to fetch |
| from | No | UserId of the sender for the fetched message |
| to | No | UserId of the receiver for the fetched message |
| startTime | No | Start Time from when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT |
| endTime | No | End Time upto when you want to fetch message list. It is number of milliseconds since January 1, 1970, 00:00:00 GMT |
| messageType | No | Message type of the message to check |
| period | No | if startTime is not passed. amount of period to check the message |
| timeUnit | No | Time unit of the period |

messageType : Possible Values:

1. MessageDelivered
2. MessageUnDelivered
3. MessageRead
4. MessageUnRead

timeUnit : Possible Values:

1. MilliSeconds
2. Second
3. Minute
4. Hour
5. Day
6. Week
7. Month
8. Year

**Response**:           

**Response**:  Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1463673355057,  // time value at which response is generated from server
  "response": [
    {
      "id" : "5-agpzfmFwcGxvemljchMLEgZTdVVzZXIYgICAgLrcvwsM-1464093115599",
      "fromUserId" : "john",
      "toUserId" : "steve",
      "groupName" : null,
      "content" : "Hello",
      "createdAtTime" : 1458039322000,
      "deliveredAtTime" : 1458039322000,
      "readAtTime" : 1458039322000
    }
  ]
}  
```


##### Load Application's Group List

**Group Filter URL**: https://apps.applozic.com/rest/ws/group/filter

**Method Type**: GET

**parameters**: 

| Parameter  | Required | Default | Description |
| ------------- | ------------- | ------------- | ------------- |       
| pageSize | No  | 500 | list of groups to load |
| endTime | No  |  | pass to load more group |




**Example:** For API Call: 

```
https://apps.applozic.com/rest/ws/group/filter?pageSize=2
```

**Response:**

``` 
{
  "status": "success",
  "generatedAt": 1487156976360,
  "response": {
    "users": [],
    "groups": [
      {
        "id": 2101199,
        "clientGroupId": "2101199",
        "name": "phonegapprivate",
        "adminName": "vipinpro",
        "adminId": "vipinpro",
        "membersName": [
          "sonupro",
          "phonegapdemo",
          "vipinpro"
        ],
        "membersId": [
          "sonupro",
          "phonegapdemo",
          "vipinpro"
        ],
        "removedMembersId": [],
        "unreadCount": 0,
        "type": 1,
        "createdAtTime": 1487155124542,
        "userCount": 3,
        "groupUsers": [
          {
            "userId": "phonegapdemo",
            "role": 3
          },
          {
            "userId": "sonupro",
            "role": 3
          },
          {
            "userId": "vipinpro",
            "role": 1
          }
        ],
        "childKeys": [],
        "childClientGroupIds": []
      },
      {
        "id": 2092165,
        "clientGroupId": "2092165",
        "name": "two",
        "adminName": "sunil",
        "adminId": "sunil",
        "membersName": [
          "sunil",
          "xyz"
        ],
        "membersId": [
          "sunil",
          "xyz"
        ],
        "removedMembersId": [],
        "unreadCount": 0,
        "type": 7,
        "createdAtTime": 1487088852348,
        "userCount": 2,
        "groupUsers": [
          {
            "userId": "xyz",
            "role": 3
          },
          {
            "userId": "sunil",
            "role": 1
          }
        ],
        "childKeys": [],
        "childClientGroupIds": []
      }
    ],
    "devices": [],
    "lastFetchTime": 1487088852348,
    "lastFetchIndex": 1,
    "totalUnreadCount": 0
  }
} 

```  

**Note** : To load further group list use **lastFetchTime** value and pass it in **endTime** parameter from next time onwards.
