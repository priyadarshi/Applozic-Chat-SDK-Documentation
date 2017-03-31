### Contextual (Topic/Product) Chat 

#### Conversation Id

Retreive Conversation Id

**URL**: https://apps.applozic.com/rest/ws/conversation/v2/id

**Method Type**: POST

**Content-Type**: application/json

**Request Body**:
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


**Response**:  success Response Json to the request in case of **userId** passed
```
{
  "status": "success",
  "generatedAt": 1473936678880,
  "response": {
    "id": "Group Id (integer)",             // internally creating virtual group
    "clientGroupId": "Group Id (integer)",
    "name": "Group Name",
    "membersId": "[ List of members user names]",
    "removedMembersId": "[]",
    "unreadCount": "(Int) message unread count for the logged in user",
    "type": "Group type",
    "conversationPxy": {
      "id": "(Int)Conversation id",  // pass as "conversationId" in request body for topic based send message
      "topicId": "Topic id of the conversation",
      "topicDetail": "Topic Detail for the conversation",
      "userId": "unique id of the receiver user", // pass as "to" in request body for topic based send message
      "created": "(true/false) if the conversation is created or not in this api",
      "closed": "(true/false) if the conversation is closed",
      "senderUserName": "userId who is initiating topic based chat",
      "status": "status of the conversation",
      "groupId": "(Int) Group id of the virtually created group"
    },
    "createdAtTime": 1473933607470,
    "userCount": 2
  }
}
```


**Response**:  success Response Json to the request in case of **groupId** passed
```
{
  "status": "success",
  "generatedAt": 1473936678880,
  "response": {
    "id": "Group Id (integer)",
    "clientGroupId": "140891",
    "name": "Group Name",
     "adminId": "userId of group admin ",
    "membersId": "[ List of members userIds]",
    "removedMembersId": "[]",
    "unreadCount": "(Int) message unread count for the logged in user",
    "type": "Group type",
    "conversationPxy": {
      "id": "(Int)Conversation id",     // pass as "conversationId" in request body for topic based send message
      "topicId": "Topic id of the conversation",
      "topicDetail": "Topic Detail for the conversation",
      "userId": " userId of User with whom topic based chat initiated",
      "created": "(true/false) if the conversation is created or not in this api",
      "closed": "(true/false) if the conversation is closed",
      "senderUserName": "userId who is initiating topic based chat",
      "status": "status of the conversation",
      "groupId": "(Int) Group id of the respected group"  // pass as "groupId"  in request body for topic based send message
    },
    "imageUrl": "Group image Url",
    "createdAtTime": 1473933607470,
    "userCount": "group user count"
  }
}
```

####Topic based Send Message

**TOPIC BASED SEND MESSAGE URL**: https://apps.applozic.com/rest/ws/message/send

**Method Type**: POST

**Content-Type**: application/json

**Request Body**:

**Note** : Request body in case of **One to One, Topic based message send**. 

**Json**                         
```
{
  "to":"unique id of the receiver user",
  "message":"Message text",
  "conversationId": "Receive in Retreive Conversation Id API"
}
```

**Json Parameter Description**: 

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| to  | Yes  |   | UserId to which you want to send message |
| message  | Yes  |   | Text Message |
| conversationId  | Yes  |   | unique id of topic based conversation |




**Note** : Request body in case of **Group, Topic based message send**. 

**Json**                         
```
{
 "groupId": "group Unique Identifier",  
  "message":"Message text"
  "conversationId": "Receive in Retreive Conversation Id API"
}
```


**Json Parameter Description**:

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId  | Yes  |   | Unique identifier of the group with respect to client |
| message  | Yes  |   | Text Message |
| conversationId  | Yes  |   | unique id of topic based conversation |



**Json**
```
{
  "messageKey": "5-22bf4626-9019-4a4a-8565-6c0e40ecda96-1454398305364",
  "conversationId": 670,
  "createdAt": 1454398305000
}
```

| Response Parameter  | Description |
| ------------- | ------------- |
| message key  | message unique id |
| createdAt  | time in milliseconds |
| conversationId  | unique id of topic based conversation |


#### Close Conversation

**CLOSE CONVERSATION URL**:  https://apps.applozic.com/rest/ws/conversation/close

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| id   | Yes  |   | unique conversation identifier  |

**Note**: Conversation is close based on unique conversation identifier.


**Response**:  Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```


#### Close Topic based Conversation

**CLOSE TOPIC BASED CONVERSATION**:  https://apps.applozic.com/rest/ws/conversation/closeall

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| topicId  | Yes  |   |unique topic id of the conversation  |
| withUserId  | Yes  |   | unique user identifier   |


**Note**: Conversation is close based on unique topic identifier.

**Response**:  Response String with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```


