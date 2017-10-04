#### Create Group

**GROUP CREATION URL**: https://apps.applozic.com/rest/ws/group/v2/create 

**Method Type**: POST 

**ContentType**: application/json


**Request Body**:   

**Json**  
```
{
  "clientGroupId":"Client Group Id",  // optional
  "groupName" : "Group Name",
  "groupMemberList" : ["UserName1", "UserName2", "UserName3"],
  "imageUrl": "Group image Url",
 "admin":"UserName"
}
```
**Json Parameter Description**: 

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId | No  |   | Unique identifier of the group with respect to client |
| groupName | Yes  |   | Name of the group |
| groupMemberList | Yes  |   |List of userIds of the  group members |
| type | No  | public  | Type of the group |
| imageUrl | No  |  | image url for group |
| admin | No  |  | set another user as admin of group |

**Note** : 

**1)** If group already exist in your system, pass that group unique identifier in **clientGroupId** to use the same with Applozic.

**2)** If **clientGroupId** is not passed then Applozic will generate a unique id for the group which should be used as **clientGroupId** for all API calls.

"type" parameters possible values

| Value  | Description |
| ------------- | ------------- |
| 1 | Private group : Other users are not able to join this group voluntarily |
| 2 | Public Group : Users are able to search and join the group |
| 5 | Broadcast Group : User can send personal message to a group of Users |
| 6 | Open Group : Any user can send the message to this group without being the member of this group |


**Note** : In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user on which behalf admin want to create group.
 

**Response** : Response Json  with success status :-  

```json
{
  "status": "success",
  "generatedAt": 1464854985171,  // time value at which response is generated from server
  "response": {
    "id": 274457,
    "clientGroupId": "Client Group Id",
    "name": "Group Name",
    "adminId": "TestUser",
    "membersId": [
      "UserName2",
      "UserName3",
      "UserName1",
      "TestUser"
    ],
    "users": [
      {
        "id": "77749a25-b260-4e37-aa62-12b8dfc64657",
        "userId": "UserName2",
        "connected": false,
        "createdAtTime": 1464854985050,
        "unreadCount": 0,
        "deactivated": false
      },
      {
        "id": "05c576da-538d-4f46-aa34-8ba4bccf98f0",
        "userId": "UserName3",
        "connected": false,
        "createdAtTime": 1464854985057,
        "unreadCount": 0,
        "deactivated": false
      },
      {
        "id": "894591fc-a48a-4e0a-ae9b-fd5125002f46",
        "userId": "UserName1",
        "connected": false,
        "createdAtTime": 1464854985062,
        "unreadCount": 0,
        "deactivated": false
      }
    ],
    "unreadCount": 0,
    "type": 2
  }
}
```

#### Multiple Group Creation

**MULTIPLE GROUP CREATION URL**: https://apps.applozic.com/rest/ws/group/v2/create/multiple

**Method Type**: POST 

**ContentType**: application/json

**Request Body**: 

**Json**  
```
[
  {
    "clientGroupId": "GroupId1",  //optional
    "groupName" : "MultiGroup1",
    "groupMemberList" : [ "kevin","john"]
  },
  {
    "groupName" : "MultiGroup2",
    "groupMemberList" : [ "jade"]
  }
]
```

**Json Parameter Description**:

| Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId | No  |   | Unique identifier of the group with respect to client |
| groupName | Yes  |   | Name of the group |
| groupMemberList | Yes  |   |List of userIds of the  group members |
| type | No  | public  | Type of the group |

**Note** : 

**1)** If group already exist in your system, pass that group unique identifier in **clientGroupId** to use the same with Applozic.

**2)** If **clientGroupId** is not passed then Applozic will generate a unique id for the group which should be used as **clientGroupId** for all API calls.

"type" parameters possible values

| Value  | Description |
| ------------- | ------------- |
| 1 | Private group : Other users are not able to join this group voluntarily |
| 2 | Public Group : Users are able to search and join the group |
| 5 | Broadcast Group : User can send personal message to a group of Users |

**Note** : In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user on which behalf admin want to create group.

**Response** : Response Json  with success status :-  

**Json**                         
```
{
  "status": "success",
  "generatedAt": 1464793892242,  // time value at which response is generated from server
  "response": [
    {
      "id": 496,
      "clientGroupId": "GroupId1",
      "name": "MultiGroup1",
      "adminId": "TestUser",
      "membersId": [
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
      "clientGroupId": "497", // same as Applozic group Id.
      "name": "MultiGroup2",
      "adminId": "TestUser",
      "membersId": [
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

#### Group Info

**LIST URL**:  https://apps.applozic.com/rest/ws/group/v2/info 

**Method Type**: GET

**Parameters**:        

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId | No  |   | Group Id of the group  |
| clientGroupId  | No  |   | Client Group id of the group |

**Note** : 

**1)** Either pass **groupId** or **clientGroupId** to get the group information.

**Response**:   Response Json with success status :-
```
{
  "status": "success",
  "generatedAt": 1465310497564,
  "response": {
      "id": 496,
      "clientGroupId": "GroupId1",
      "name": "MultiGroup1",
      "adminId": "TestUser",
      "membersId": [
        "kevin",
        "john",
        "TestUser"
      ],
      "removedMembersId": [],
      "unreadCount": 0,
      "type": 2,
      "imageUrl": "https://www.applozic.com/resources/images/applozic_logo.gif",
      "createdAtTime": 1473836906978,
      "userCount": 3
    }
}
```

#### User's Group List

**LIST URL**:  https://apps.applozic.com/rest/ws/group/v2/list 

**Method Type**: GET

**Parameters**:        

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| updatedAt | No  |   | lastSyncTime to the server  |

**Note** : In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user for which admin want to load the group list.

**Response**:   Response Json with success status :-         

```
{
  "status": "success",
  "generatedAt": 1465310497564,    // time value at which response is generated from server
  "response": [
    {
      "id": 496,
      "clientGroupId": "GroupId1",
      "name": "MultiGroup1",
      "adminId": "TestUser",
      "membersId": [
        "kevin",
        "john",
        "TestUser"
      ],
      "removedMembersId": [],
      "unreadCount": 0,
      "type": 2
    },
    {
      "id": 497,
      "clientGroupId": "497",
      "name": "MultiGroup2",
      "adminId": "TestUser",
      "membersId": [
        "jade",
        "TestUser"
      ],
      "removedMembersId": [],
      "unreadCount": 0,
      "type": 2
    }
  ]
}
```

**Note**: For the next sync call, pass "updatedAt" parameter to get details of only the modified group and newly added group of that user. Applozic API response contains "generatedAt" parameter which contains the timestamp at the time of server response. Use it as "updatedAt" for your next sync call.


#### Add User to Group

**ADD GROUP MEMBER URL**:  https://apps.applozic.com/rest/ws/group/add/member 

**Method Type**: POST

**ContentType**: application/json

**Request Body**: 

**Json**                         
```
{
	"userId":"user unique identifier ",
	"clientGroupId":"group unique identifier"	
}
```

**Json Parameter Description**: 

|Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId   | Yes  |   | User unique identifier to be added in group  |
| clientGroupId | Yes  |   | Group  unique identifier |


**Note** : In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user on behalf of which application admin want to add member.

**Response**:  Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```


#### Add users to Many Groups

**URL**:  https://apps.applozic.com/rest/ws/group/add/users

**Method Type**: POST

**ContentType**: application/json

**Request Body**:  

**Json** 
```
  { 
  "userIds":["userId1","userId2","userId3"],
	"clientGroupIds":["groupId1","groupId2"]
 }
```
**Json Parameter Description**: 

|Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupIds   | Yes  |   | List of Group unique identifiers  |
| userIds   | Yes  |   | List of Unique ids of the users to be added to the group  |


**Note**: In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user on behalf of which application admin want to add users.

**Response**:  Response Json with success status :-  
```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```

**Note**: Groups for the passed clientGroupIds and the user for the passed userIds should exist in that application.


### Remove User from Group 

**REMOVE GROUP MEMBER URL**:  https://apps.applozic.com/rest/ws/group/remove/member 

**Method Type**: POST

**ContentType**: application/json

**Request Body**: 

**Json**                         
```
{
	"userId":"user unique identifier ",
	"clientGroupId":"group unique identifier"	
}
```

**Json Parameter Description**: 

|Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId   | Yes  |   | User unique identifier to be removed from group  |
| clientGroupId | Yes  |   | Group  unique identifier |


**Note** : In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user on behalf of which application admin want to remove member.


**Response**:  Response Json  with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```

**Note**: Only Group Admin can remove the group member from private group otherwise the following error will come:

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
  "generatedAt":1452348983616  // time value at which response is generated from server
}
```



#### Leave Group

**LEAVE GROUP URL**:  https://apps.applozic.com/rest/ws/group/left 

**Method Type**: POST

**ContentType**: application/json

**Request Body**: 

**Json**                         
```
{
	"clientGroupId":"group unique identifier"	
}
```

**Json Parameter Description**: 

|Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId | Yes  |   | Group  unique identifier |


**Note**: In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user for which application admin want to leave the group.

**Response**: Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
```

#### Remove Users From Many Groups

**URL**:  https://apps.applozic.com/rest/ws/group/remove/users

**Method Type**: POST

**ContentType**: application/json

**Request Body**:  

**Json** 
```
  { 
  "userIds":["userId1","userId2","userId3"],
	"clientGroupIds":["groupId1","groupId2"]
 }
```
**Json Parameter Description**: 

|Json Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupIds   | Yes  |   | List of Group unique identifiers  |
| userIds   | Yes  |   | List of Unique ids of the users to be removed from the group  |


**Note**: In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user on behalf of which application admin want to remove users.

**Response**:  Response Json with success status :-  
```  
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```
**Note**: Groups for the passed clientGroupIds and the user for the passed userIds should exist in that application.


####Remove User From All Groups        

**Note** : API supported both by application admin and application user. 

**URL**: https://apps.applozic.com/rest/ws/user/remove/group/all

**Method Type**: GET


| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId   | Yes  |   | user unique identifier  | 


**Note**: In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user to which admin want to remove from groups.


**Note**: API will remove User from **Private**, **Public** and **Open** Group.

**Response**: 

```
{
  "status": "success",
  "generatedAt": 1452347180639, // time value at which response is generated from server
  "response": "success"
}
```


#### Update Group

**UPDATE GROUP URL**: https://apps.applozic.com/rest/ws/group/update 

**Method Type**: POST

**ContentType**: application/json

**Request Body**:  

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupId   | No  |   | Group unique identifier |
| clientGroupId   | No  |   | Client Group unique identifier |
| newName | No  |   | New name of group |
| imageUrl | No  |   | image url of the group |

**Note**: In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user on behalf of which application admin want to change group name. Pass either groupId or clientGroupId.

**Response**: Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
```
**Note** Group Admin can update any group user role by passing following request body:

**Request Body**: 

```  
{
  "clientGroupId": "group unique identifier",
  "users": [
    {
      "userId": "user unique identifier",
      "role": 1
    },
    {
      "userId": "user unique identifier",
      "role": 1
    }
  ]
}
```
**Role**: 

| Parameter  | Value | Description | Privilege |
| ------------- | ------------- | ------------- |       
| role | 1 |  role will be admin | Full Access to group  |
| role | 2 |  role will be moderator | Add/remove users , Group Info update|
| role | 3|  role will be member |Group Info update|


**Note** Group Admin can update group existing meta data value and can pass new meta data as well in request body:

**Request Body**: 

``` 

{
  "clientGroupId": "226583",
  
  "metadata":{
    "HIDE":"true",
    "GROUP_ICON_CHANGE_MESSAGE": "Icon Changed"

  }
}
```


#### Update Group User Properties

**Url**: https://apps.applozic.com/rest/ws/group/user/update

**Method Type**: POST

**ContentType**: application/json

**Request Body**:  

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| userId   | No  |   | User identifier for One - One conversation |
| id   | No  |   | Group unique identifier  |
| clientGroupId   | No  |   | Client Group unique identifier  |
| notificationAfterTime   | No  |   | Time Interval for which notification has be be disabled |

**Note**: In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of user on behalf of which application admin want to update group user properties.

**Response**: Response Json with success status :-  

```  
{
  "status": "success",
  "generatedAt": 1452347180639,  // time value at which response is generated from server
  "response": "success"
}
```

#### Group - Is User Present
Check if user is part of a Group

**CHECK USER URL**:  https://apps.applozic.com/rest/ws/group/check/user 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId   | Yes  |   | Group unique identifier  |
| userId   | Yes  |   | UserId of the user identify in group  |

**Note**: In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is userId of user exist in a group on behalf of which application admin calling th API.

**Response**:  API response: in case of success :-  

```  
{
  "status": "success",
  "generatedAt": 1463673355057,  // time value at which response is generated from server
  "response": true/false
}
```

#### Group Users Count 

**URL**:  https://apps.applozic.com/rest/ws/group/user/count

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupIds   | Yes  |   | List of Group unique identifiers  |


**Response**:  Response Json with success status :-  
```  
{
  "status": "success",
  "generatedAt": 1469293877608,
  "response": [
    {
      "id": 503,
      "clientGroupId": "503",
      "userCount": 3
    },
    {
      "id": 504,
      "clientGroupId": "clientGroupId",
      "userCount": 5
    }
  ]
}
```

### Group Delete 

**DELETE GROUP URL**:  https://apps.applozic.com/rest/ws/group/delete 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| clientGroupId   | Yes  |   | Group unique identifier  |

**Note**: In case of Application Admin **Of-User-Id** header required too. **Of-User-Id** is the userId of group admin user, on behalf of which application admin want to delete the group.

**Response**:  Json with success status :-  

```
{
  "status": "success",
  "generatedAt": 1463673355057,  // time value at which response is generated from server
  "response": true
}  
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
  "generatedAt":1452348983616   // time value at which response is generated from server
}
```

###  OPEN Channel (or Group)

**URL**:  https://apps.applozic.com/rest/ws/group/v2/channel 

**Method Type**: GET

**Parameters**: 

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| pageSize  | No  | 50  | Number of Open channel need to be fetch.  |
| endTime  | No  |   | pass  lastFetchTime as endTime(fetched in API response) to load  more channel list   |

**Response**:  Json with success status :-  

```
{
  "status": "success",
  "generatedAt": 1487742549494,
  "response": {
    "groupPxys": [
      {
        "id": 40689,
        "clientGroupId": "40689",
        "name": "OPEN_GROUPSS_TYPE_ID",
        "adminName": "beneton",
        "adminId": "beneton",
        "memberUserKeys": [
          "29c97be5-6d3f-4aaf-95c0-f282650f5c14",
          "a7b2d8ab-cc4d-47ed-9a31-0362c6a75975"
        ],
        "membersName": [
          "beneton",
          "banglow"
        ],
        "membersId": [
          "beneton",
          "banglow"
        ],
        "removedMembersId": [],
        "unreadCount": 0,
        "type": 6,
        "createdAtTime": 1487689414972,
        "userCount": 2,
        "groupUsers": [
          {
            "userId": "banglow",
            "status": 0,
            "unreadCount": 0,
            "role": 3,
            "deleted": false
          },
          {
            "userId": "beneton",
            "status": 0,
            "unreadCount": 0,
            "role": 1,
            "deleted": false
          }
        ],
        "childKeys": [],
        "childClientGroupIds": [],
        "metadata": {
          "AL_CATEGORY": "Drop",
          "Key": "VALUE"
        }
      }
    ],
    "lastFetchTime": 1487689414972
  }
}
```

**Note**: To load more open channel pass "endTime" parameter in API call. Pass "lastFetchTime" as "endTime" in API call.

### Group Metadata

To add metadata for a group, send the metadata object inside the group object while creating group. The same metadata object will be received in group list api with group object. The metadata object is a map with string keys and values.

**Sample Group Object Json with Metadata**:          

```json
{
 "clientGroupId":"Client Group Id",
 "groupName" : "Group Name",
 "groupMemberList" : ["UserName1", "UserName2", "UserName3"],
 "imageUrl": "Group image Url",
 "metadata" : {
   "key1" : "value1",
   "key2" : "value2"
 }
}
```

### Group Settings

 This will helpful for altering the default message template for the group. 

Note: If the template is sent as blank, then no alert notification is sent to devices and receive message silently.

**Update metadata of the group as the following property keys**:          

- CREATE_GROUP_MESSAGE
- REMOVE_MEMBER_MESSAGE
- ADD_MEMBER_MESSAGE
- JOIN_MEMBER_MESSAGE
- GROUP_NAME_CHANGE_MESSAGE
- GROUP_ICON_CHANGE_MESSAGE
- GROUP_LEFT_MESSAGE
- DELETED_GROUP_MESSAGE
- GROUP_USER_ROLE_UPDATED_MESSAGE
- ALERT
- HIDE

**Following place holders will be replaced**

- :adminName = admin name of the group
- :groupName = group name
- :userName = user name for which the action is performed 
- :role = role of user 

Perform the group create, update, add member, remove etc actions on the group. Eg: 

```json
{
  "metadata":{
    "CREATE_GROUP_MESSAGE":":adminName created group",
    "ADD_MEMBER_MESSAGE":":userName joined group",
    "GROUP_USER_ROLE_UPDATED_MESSAGE":":userName is :role now"
  }
}
```



**Example:1**

If want to displayed messages in chat message list but don't want explicit notification.

Use below sample:
```json
{
  "groupName" : "GroupName",
  "groupMemberList" : ["user1","user2"],
  "metadata":{
    "CREATE_GROUP_MESSAGE":"",
    "ADD_MEMBER_MESSAGE":"",
    "GROUP_NAME_CHANGE_MESSAGE" : "",
  }
   
}
```
**Note** 

1.If Alert metadata is configured to false no explicit notification send to iOS devices.

2.) For Android device messages in message list will come with metadata having key **show** with value **false** so android explicit notification can be handled.


**Example:2**

1.)If having any customize message for different metadata and want to add those messages in chat messages list but don't want explicit notification.

2.)Basically  messages will add to device silently:

Use below sample:
```json
{
  "groupName" : "GroupName",
  "groupMemberList" : ["user1","user2"],
  "metadata":{
    "CREATE_GROUP_MESSAGE":"Message in different language",
    "ADD_MEMBER_MESSAGE":" :adminName Ne Group :groupName me add Kiya :)",
    "GROUP_NAME_CHANGE_MESSAGE" : "Message in different language",
    "ALERT": "false"
  }
   
}
```
**Note** 

1.If Alert metadata is configured to false no explicit notification send to iOS devices.

2.) For Android device messages in message list will come with metadata having key **show** with value **false** so android explicit notification can be handled.


**Example:3**

If want to filter messages not to be displayed in chat message list

Use below sample:
 
```json
{
  "groupName" : "GroupName",
  "groupMemberList" : ["user1","user2"],
  "metadata":{
    "CREATE_GROUP_MESSAGE":"",
    "ADD_MEMBER_MESSAGE":"",
    "GROUP_NAME_CHANGE_MESSAGE" : "",
    "HIDE": "true"
  }
   
}
```

**Note** 

1.) In this case Group create, add and name change message will come with metadata **hide** with value **true** message list API call.

2.)So you can filter out these messages:

#### Create User's Friend/Favourite contacts List

Using this API you can create your group of contacts for individual user and fetch it later. 

Example usage case : You can create your favorite contact list by passing GroupName as favorite, and keep modifying list based on once user marks it as favorite.

**URL**: https://apps.applozic.com/rest/ws/group/{GroupName}/add 

**Method Type**: POST 

**ContentType**: application/json


**Request Body**:   

**Json**  
```
["UserName1","UserName1","UserName1"]
```

**Note** : 

**1)** If group does not exist then it will create group and add the list of users (passed in JSON) add into group.

**2)** If group already exist in your system, then the API will add the passed user into group.

###  Create open Friend/Favourite contacts List 

Using this API you can create group of contacts and any member present in the list can fecth it. 

**GROUP CREATION URL**: https://apps.applozic.com/rest/ws/group/{GroupName}/add/members 

**Method Type**: POST 

**ContentType**: application/json


**Request Body**:   

**Json**  
```
{"type":"9",
"groupMemberList":["user1","user2","user3"]
}
```

**Note** : 

**1)** If group does not exist then it will create group and add the list of users (passed in JSON) add into group.

**2)** If group already exist in your system, then the API will add the passed user into group.



#### Get Friend/Favourite List

Using this API you can get your friends contact list. 

**FRIEND LIST CREATION URL**: https://apps.applozic.com/rest/ws/group/{GroupName}/get

**Method Type**: GET 

**Parameter**:

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupType   | No  |   | groupType required only for open List  |


**Response**:  Json with friend list info with added users :- 


#### Remove user from Friend List

Using this API you can remove user from your friends contact list. 

**FRIEND LIST CREATION URL**: https://apps.applozic.com/rest/ws/group/{GroupName}/remove?userId=userName

**Method Type**: GET 

**Parameter**:

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupType   | No  |   | groupType required only for open List  |


**Response**:  Json with success:- 


#### Delete Friend List

Using this API you can delete friends contact list. 

**FRIEND LIST CREATION URL**: https://apps.applozic.com/rest/ws/group/{GroupName}/delete

**Method Type**: GET 

**Parameter**:

| Parameter  | Required | Default  | Description |
| ------------- | ------------- | ------------- | ------------- |
| groupType   | No  |   | groupType required only for open List  |


**Response**:  Json with success:- 







