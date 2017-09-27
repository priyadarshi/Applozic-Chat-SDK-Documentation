Explore Platform API's as per Application Admin or as per Application User.

# HEADERS

#####Application Admin

For Application Admin send following authentication headers with each API call to explore platform API's. Request should contain these headers:

| Header | Description  |
| ------ | ----------- |
| Apz-AppId | application key got in admin dashboard for which admin want to call api. |
| Apz-Token | Authorization Code. Authentication is done using BASIC authentication. Authorization Code is combination of  base64 value of email & password of  application admin. Basic Base64Encode of "email:password". |
| Content-Type |  application/json  |
| OfUserId |  On behalf of Application Admin want to call the API |

**Note** : Pass **OfUserId** header only where it is required, it is specified in the API details.

**Example**- 
If the email of the admin(Logged in Applozic Dashboard) is  **jack@gmail.com** and password is **adminLoggedInApplozicDashboard** then header will be:

| Header | Description  |
| ------ | ----------- |
| Apz-AppId | 21040368s3869d9b2b7b2f953ae28cf |
| Apz-Token | Basic amFja0BnbWFpbC5jb206YWRtaW5Mb2dnZWRJbkFwcGxvemljRGFzaGJvYXJk |
| Content-Type |  application/json  |

#####Application User

All request from Device must contain following headers:

| Key | Values  |
| ------------- | ------ |
| Application-Key | Your Application Key |
| Authorization | Authentication is done using BASIC authentication.Basic Base64Encode of userId:deviceKey |
| Device-Key | DeviceKey is received when application user does registration using register/client API. Use Device-Key to create Authorization Code and send Device-Key also in request header.  |


**Example**- 
If the userId is **robert** and deviceKey is **09c5d869-6d38-4d6b-9ebf-9de16cdab176**, then the authorization code will be:

| Key | Values  |
| ------------- | ------ |
| Application-Key | TestApp |
| Authorization | Basic cm9iZXJ0OjA5YzVkODY5LTZkMzgtNGQ2Yi05ZWJmLTlkZTE2Y2RhYjE3Ng== |
| Device-Key | 09c5d869-6d38-4d6b-9ebf-9de16cdab176 |
| UserId-Enabled | true |

**Note** : Additional header **Access-Token**  is also required if user password is set in Applozic.

| Key | Values  |
| ------------- | ------ |
| Access-Token | user password |

**Note** : Headers are required in each API call except user registration .ie register/client API.
