## Paths
#### POST /Cards/validate

**Tag**: Card

**Description**: public endpoint Validates card using a card number and pin. A stateCode of the following will be returned: CardNotFound, CardAlreadyRegistered, CardExpiredOrCancelled, or CardInactive.

**Request Parameters**:

| Name      | Description                 | Type    | Data Type     | Mandatory |
| --------- |:---------------------------:|:-------:|:-------------:| -----:|
| cardNumber| Number of the rewards card. | form    | string        | true  |
| pin       | Card pin                    | form    | string        | true  |
| httpCtx   | Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: { `cardNumber`: 'xxxx', `state`: 'xxxx', `stateCode`: 'xxxx' }

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)

**Error Code sample**:  

105 `IncorrectPin` The CardPassword is not correct.  




#### POST /Customers/addresses/add

**Tag**: Customer

**Description**: Add an address for a customer.

**Request Body**:  
Uses default content-types: *application/json*  
Request Body: `CustomerAddress`  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id|Customer id| header| string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `CustomerAddress`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.


#### GET /Customers/addresses/list

**Tag**: Customer

**Description**: List all customer's addresses.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id|Customer id| header| string | true |
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: ITEMS `CustomerAddress`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.



#### POST /Customers/addresses/update/{addressId}

**Tag**: Customer

**Description**: Update customer's address.

**Request Body**:  
Uses default content-types: *application/json*  
Request Body: `CustomerAddress`  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id|Customer id                  | header| string        | true  |
| httpCtx      | Do not implement in clients.| formData | string (JSON) | false |
| addressId    | Address id                  | path  | string        | true  |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `CustomerAddress`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
3005 `InvalidAddressId` The address for the AddressId is not exist.  


#### POST /Customers/cards/add

**Tag**: Customer

**Description**: Attach a new card to a Customer.
                 The `makeLive` param will set the card to be active after adding.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id|Customer id                  | header| string        | true  |
| httpCtx      | Do not implement in clients.| formData | string (JSON) | false |
| cardNumber   | Rewards card number         | form  | string        | true  |
| pin          | Card pin number             | form  | string        | true  |
| makeLive     | Make this card live after it's added. Only Y or N. Default is N | form  | string        | false  |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `Card`  # # ## ### 

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
106 `CardAlreadyRegistered` The card has been registered.  
104 `CardNotFound` The card is not found.  
105 `IncorrectPin` The CardPassword is not correct.  
108 `CardNotActive` The card status is not Active.  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
3008 `CardExpired` The card is Active, but end date is greater than today.  
3010 `MemberNotActive` The member status of card is not Active.  



#### POST /Customers/cards/delete

**Tag**: Customer

**Description**: Remove a customer's card.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id|Customer id                  | header| string        | true  |
| httpCtx      | Do not implement in clients.| formData | string (JSON) | false |
| cardNumber   | Rewards card number         | form  | string        | true  |
| reason       | Reason for removing the card. | form  | string        | true |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
103 `CardRegisteredWithAnotherCustomer` The card has been registered with another member.  
104 `CardNotFound` The card is not found.  
113 `CardNotDormant` The card status is not Dormant  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  



#### GET /Customers/cards/list

**Tag**: Customer

**Description**: List all the cards for a customer.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id|Customer id                  | header| string        | true  |
| httpCtx      | Do not implement in clients.| query | string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: ITEMS `Card`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  



#### POST /Customers/cards/lost

**Tag**: Customer

**Description**: Report a customer's card as lost or stolen.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id|Customer id                  | header| string        | true  |
| httpCtx      | Do not implement in clients.| formData | string (JSON) | false |
| cardNumber   | Rewards card number         | form  | string        | true  |
| reasonCode   | Mark the card as being `Lost`, `Stolen`, or `Damaged`. | form  | string        | true  |
| sendReplacement | Should a replacement card be sent? | form  | string        | false  |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `Card`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
102 `CardAlreadyLostOrStolen` Te card is already flagged as Lost or Stolen (Status is Obsolete).  
103 `CardRegisteredWithAnotherCustomer` The card has been registered with another member.  
104 `CardNotFound` The card is not found.  
111 `CardInTransit` The card status is InTransit.  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
3012 `CardNotRegisteredOrDormant` The card status is not Registered or Dormant  


#### POST /Customers/cards/wake

**Tag**: Customer

**Description**: Wake a card.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id|Customer id                  | header| string        | true  |
| httpCtx      | Do not implement in clients.| formData | string (JSON) | false |
| cardNumber   | Rewards card number         | form  | string        | true  |

**Response**  
Uses default content-types: *application/json*  

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
104 `CardNotFound` The card is not found.  
113 `CardNotDormant` The card status is not Dormant  


#### POST /Customers/create

**Tag**: Customer WeChat

**Description**: Create a new customer.

**Request Body**:  
Uses default content-types: *application/json*  
Request Body: `CustomerCreate`  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| data| Model instance data| form| Object([CustomerCreate](#user-content-CustomerCreate)) | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

###<span id = "user-content-CustomerCreate">CustomerCreate</span>

`userName`: {type: 'string', required: true},

`password`: {type: 'string', required: true},

`cardNumber`: {type: 'string', required: true},

`cardPassword`: {type: 'string', required: true, description: 'Otherwise known as the card\'s `pin`'},

`email`: {type: 'string', required: true},

`firstName`: {type: 'string', required: true},

`lastName`: {type: 'string', required: true },

`gender`: {type: 'string', description: 'Only `Male` or `Female` are allowed'},

`birthday`: {type: 'string', required: true, description: 'Must have format of `MM/DD/YYYY`'},

`primaryCountry`: String,

`primaryState`: String,

`primaryCity`: String,

`primaryZip`: String,

`primaryAddress`: String,

`hobbies`: {type: 'string'},

`language`: {
    type: 'string',
    description: 'Only `CHS` or `ENU` are allowed',
    required: true
  },

  `notes`: {
    type: 'string'
  },

  `favouriteProduct`: {
    type: 'string'
  },

  `favouriteProductAlternate`: {
    type: 'string'
  },

  `cellPhone`: {
    type: 'string',
    description: 'Must have format of `/^((1[34578][0-9]))[0-9]{8}$/`',
    required: true
  },

  `homePhone`: {
    type: 'string'
  },

  `workPhone`: {
    type: 'string'
  },

  `fax`: {
    type: 'string'
  },

  `SourceCode`:{
    type:'string'
  },

  `optOut`: {
    type: 'number',
    description: '`0` - yes , `1` - no, `2` - don\'t allow third parties to send notifications'
  },

  `cellPhoneValidFlag`: {
    type: 'string'
  }


**Response**  
Uses default content-types: *application/json*  

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
104 `CardNotFound` The card is not found.  
105 `IncorrectPin` The card password incorrect  
108 `CardNotActive` The card status is not Active.  
201 `EmailRegisteredActive` Email is in use by a registered customer.  
202 `EmailRegisteredInactive`  Email is in use by an Closed customer.  
204 `EmailInUse` Email in use by another member.  
301 `InvalidStore` The store is not exist or the status of the store is closed.  
3008 `CardExpired` The card status is Active, but the end date of card is greater than today  
3009 `MemberNotOpen` The member status of card is not Open  
3011 `UserNameInUse` UserName use by another member  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
10005 `WrongCaptcha` Captcha may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20005 `MissingCaptcha` Captcha is missing.  
20009 `FrequentVerify` Verify too frequent.    

Http Status code: 423  
Response Body: [SMSRequestError](abc.com)  

**Error Code sample**:  
20006 `CaptchaRequired` Captcha is required.  





#### GET /Customers/detail

**Tag**: Customer

**Description**: Find a customer by id.

**Request Body**:  
Uses default content-types: *application/json*  
Request Body: `CustomerCreate`  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id | Customer id| header | string | true |
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*  

**Success response**  
Http Status code: 200 OK  
Response Body: `Customer`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  



#### POST /Customers/disable

**Tag**: Customer

**Description**: Disables a customer.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id | Customer id| header | string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |
| reason | Reason for disabling.| formData| string | true |

**Response**  
Uses default content-types: *application/json*  

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  



#### POST /Customers/login

**Tag**: Customer

**Description**:  
> public endpoint NOTE: password hashing algorithms may change and reset your password. You will need to create a new user, or reset your password.  

**Request Parameters**:  
> 
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| user  |   Username or email.   | formData | string | true |
| password  | Password. | formData | string | true |
| httpCtx  | Do not implement in clients.| formData | string(json) | false |

**Success response**  
> 
Http Status code: 200 OK  
Response Body: CustomerId 


**Failure response**  
> 
Http Status code: 400  
Response Body:  [SiebelRequestError](abc.com) 


**Error Code sample**:  
>
403 `InvalidEmailAndPassword` The UserName/Email or Password is invalid.  
3016 ` NeedEmailActiveMember` The Member Need Active Use Email.  
3099 ` RefuseLoginDueUnverifiedMobile` Refuse Login due to cell phone is not verified.  



#### GET /Customers/orders/list

**Tag**: Customer

**Description**: List all the orders for a customer.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id | Customer id| header | string | true |
| pageNum | The page number to fetch.| query | number(double) | true |
| pageSize | Number of items to return per page.| query | number(double)(default:"50") | false |
| startDate | Date to start querying items for. Format must be MM/DD/YYYY.| query | string | false |
| endDate | Date to stop querying items for. Format must be MM/DD/YYYY.| query | string | false |
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*  

**Success response**  
Http Status code: 200 OK  
Response Body: `Order`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  



#### POST /Customers/resetPassword

**Tag**: Customer

**Description**: Reset a customer's password.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id | Customer id| header | string | true |
| password | Customer's current password.| form | string | true |
| newPassword | New password to set.| form | string | true |
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
3013 `EmailNotFound` Email not found.  
3014 `IncorrectUserPassword` The UserPassword is Incorrect.  



#### POST /Customers/resetPasswordToken

**Tag**: Customer

**Description**: Reset a customer's password when passed a valid reset token. `public endpoint` 

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| token |               | form | string | true |
| newPassword | New password to set.| form | string | true |
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
-400 `TOKEN_ALREADY_USED`  
-401 `TOKEN_INVALID`  
-5 `EMAILS_DONT_MATCH`  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
3013 `EmailNotFound Email` not found.  
3014 `IncorrectUserPassword` The UserPassword is Incorrect.   



#### GET /Customers/rewards

**Tag**: Customer

**Description**: List all customer rewards.  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id | Customer id | header | string | true |
| status | Filter rewards by status either `All`, `Unused`, or `Used`. Default is `All`| query | string | false |
| pageNum | The page number to fetch.| query | number(double) | true |
| pageSize | Number of items to return per page.| query | number(double)(default:"50") | false |
| startDate | Date to start querying items for. Format must be MM/DD/YYYY.| query | string | false |
| endDate | Date to stop querying items for. Format must be MM/DD/YYYY.| query | string | false |
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: ITEMS `Reward`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  



#### POST /Customers/sendResetPasswordEmail

**Tag**: Customer

**Description**: Sends and email to Customer with an expiring password reset link. `public endpoint` Will always return success, regardless if the email was found or not. 

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| email |       | form | string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  



#### POST /Customers/sms/send （to be replaced by below two new APIs)

**Tag**: Customer

**Description**: Send SMS to customer.  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| phoneNumber |       | form | string | true |
| template | SMS text template key (Available value is `captcha`, `create`, `update`, `create-cn`, `create-en`, `update-cn`, `update-en`) | form | string | false |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)  

**Error Code sample**:  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20004 `MissingMsg` Message text is missing.  


#### POST /Customers/sms/sendRegisterPin

**Tag**: Customer

**Description**:  
> Send Register PIN to customer mobile. (This is a public API).  

**Request Parameters**:  
> 
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| phoneNumber |   phone number cannot be NULL    | form | string | true |
| template | SMS text template key (Available value is create-cn, create-en) | form | string | true |
| cardNumber | card number cannot be NULL |  form | string | true |
| cardPassword | card password cannot be NULL |  form | string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
> 
Uses default content-types: *application/json*

**Success response**  
> 
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
> 
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)  

**Error Code sample**:  
> 
104 `CardNotFound` The card is not found.  
105 `IncorrectPin` The CardPassword is not correct.  
106 `CardAlreadyRegistered` The card has been registered.  
3006 `CardInactive` The card status is Inactive.  
3008 `CardExpired` The card is Active, but end date is greater than today.  
3015 `CardReturnedOrAbolished` The card status is Returned or Abolished  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20004 `MissingMsg` Message text is missing.  
40001 `RegisterSMSTooFrenquently` Too frequently for sending message to the same card or mobile    



#### POST /Customers/sms/sendOldPhonePin

**Tag**: Customer

**Description**:  
> Send Update PIN to customer. (This is a private API, need login first)  

**Request Parameters**:  
> 
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| template | SMS text template key (Available value is update-cn, update-en) | form | string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
> 
Uses default content-types: *application/json*

**Success response**  
> 
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
> 
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)  

**Error Code sample**:  
> 
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20004 `MissingMsg` Message text is missing.  
40001 `RegisterSMSTooFrenquently` Too frequently for sending update SMS to the same mobile  
-11   `MEMBER_NOT_FOUND_ERROR` Member not found with email or customerId.  

#### POST /Customers/sms/verifyForToken

**Tag**: Customer

**Description**:  
> Verify customer input captcha for Token.  

**Request Parameters**:  
> 
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| captcha  | This field can not be null | form | string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
> 
Uses default content-types: *application/json*

**Success response**  
> 
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
> 
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)  

**Error Code sample**:  
> 
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
10005 `WrongCaptcha` Captcha may be wrong.  
20005 `MissingCaptcha` Captcha is missing.  
20009 `FrequentVerify` Verify too frequent.  
-11   `MEMBER_NOT_FOUND_ERROR` Member not found with email or customerId.  

#### POST /Customers/sendEmailPin

**Tag**: Customer

**Description**:  
> Send an email to Customer with a Pin Code.  


*private endpoint*  
Will always return success, regardless if the email was found or not.
  

**Request Parameters**:  
> 
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
> 
Uses default content-types: *application/json*

**Success response**  
> 
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
> 
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
> 
40001 `Too frequently for sending message for the same mobile`    

#### POST /Customers/verifyEmailPin

**Tag**: Customer

**Description**:  
> Verify a customer's Email Pin Code.  
private endpoint  

**Request Parameters**:  
> 
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| pinCode   |  | form | string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
> 
Uses default content-types: *application/json*

**Success response**  
> 
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
> 
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
> 
105 `Incorrect pin`  
40001 `Too frequently for sending message for the same mobile`    
-11   `MEMBER_NOT_FOUND_ERROR` Member not found with email or customerId.  


#### POST /Customers/sms/sendUpdatePin

**Tag**: Customer

**Description**:  
> Send Update PIN to customer. (This is a private API, need login first)   

**Request Parameters**:  
> 
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| phoneNumber   | This field can not be null | form | string | true |  
| template    | SMS text template key (Available value is update-cn, update-en) | form | string | true |  
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
> 
Uses default content-types: *application/json*

**Success response**  
> 
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
> 
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)  

**Error Code sample**:  
> 
-6 `PhoneNotValid` Phone number Not Valid.  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20004 `MissingMsg` Message text is missing.  
40001 `RegisterSMSTooFrenquently` Too frequently for sending update SMS to the same mobile



#### POST /Customers/sms/sendMobilePin

**Tag**: Customer

**Description**:  
> Send verify mobile PIN to customer mobile. (This is a public API).  

**Request Parameters**:  
> 
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| phoneNumber |   phone number cannot be NULL    | form | string | true |
| template | SMS text template key (Available value is verify-cn, verify-en) | form | string | true |
| user  | Username or email |  form | string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
> 
Uses default content-types: *application/json*

**Success response**  
> 
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
> 
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)

**Error Code sample**:  
> 
-6 `PhoneNotValid` Phone number Not Valid.  
-7 `TemplateNotValid` Template Not Valid.  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
20001 `FrequentSend`Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20004 `MissingMsg` Message text is missing.  
40001 `RegisterSMSTooFrenquently` Too frequently for sending message to the same card or mobile.   
40003 `NeedLoginFirstBeforeVerifyMobile` Need user login first before verify mobile or send mobile.



#### POST /Customers/sms/verifyMobile

**Tag**: Customer

**Description**:  
>
 verify  MobilePIN is correct or wrong. (This is a public API). 

**Request Parameters**:
>
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| phoneNumber |  phone number cannot be NULL     | form | string | true |
| cellPhoneValidFlag  |  cell phone pin code cannot be NULL         | form | string | true |  
| user | Username or email | form| string  | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
>
Uses default content-types: *application/json*

**Success response**  
>
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
>
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com) 

**Error Code sample**:  
>
-6 `PhoneNotValid` Phone number Not Valid.  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
10005 `WrongCaptcha` Captcha may be wrong.  
20003 `MissingNo` Phone number is missing.  
20005 `MissingCaptcha` Captcha is missing.  
20009 `FrequentVerify` Verify too frequent.   
40003 `NeedLoginFirstBeforeVerifyMobile` Need user login first before verify mobile or send mobile. (**This force user to login first before trying to verify his mobile. In order to enhance the security level, as this public API can help change user mobile.**)
  
**Failure response**  
>
Http Status code: 423  
Response Body: [SMSRequestError](abc.com) 

**Error Code sample**:  
>
20006 `CaptchaRequired` Captcha is required.


#### POST /Customers/sms/verify

**Tag**: Customer

**Description**: Verify customer input captcha.  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| phoneNumber |       | form | string | true |
| captcha |           | form | string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)  

**Error Code sample**:  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
10005 `WrongCaptcha` Captcha may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20005 `MissingCaptcha` Captcha is missing.  
20006 `FrequentVerify` Verify too frequent.  



#### POST /Customers/sms/sendPasswordPin

**Tag**: Customer

**Description**:
>
Send Find password PIN to customer mobile. (This is a public API).
 

**Request Parameters**:
>
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| phoneNumber |  phone number cannot be NULL     | form | string | true |
| template   |  SMS text template key (Available value is password-cn, password-en)        | form | string | true |  
| user | Username or email | form| string  | false |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
>
Uses default content-types: *application/json*

**Success response**  
>
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
>
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)

**Error Code sample**:  
>
-6 `PhoneNotValid` Phone number Not Valid.  
-7 `TemplateNotValid` Template Not Valid.  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20004 `MissingMsg` Message text is missing.  
40001 `RegisterSMSTooFrenquently` Too frequently for sending message to the same card or mobile.  
40002 `MultiAccountBoundToOnePhone` More than one customer accounts bound to one phone.   

#### POST /Customers/sms/verifyPasswordPin

**Tag**: Customer

**Description**:
>
verify password PIN is correct or wrong. (This is a public API).
 

**Request Parameters**:
>
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| phoneNumber |  phone number cannot be NULL     | form | string | true |
| cellPhoneValidFlag  | cell phone pin code cannot be NULL        | form | string | true |  
| user | Username or email | form| string  | false |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |
 
**Response**  
>
Uses default content-types: *application/json*

**Success response**  
>
Http Status code: 200 OK   
**Response Body：**  
PROPERTIES  
arg: *x-customer-id*  
type: *string*  
description: *Customer id*  
required: *x-any*  
http: *x-any*

**Failure response**  
>
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)

**Error Code sample**:  
>
-6 `PhoneNotValid` Phone number Not Valid.  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
10005 `WrongCaptcha` Captcha may be wrong.  
20003 `MissingNo` Phone number is missing.  
20005 `MissingCaptcha` Captcha is missing.  
20009 `FrequentVerify` Verify too frequent.  
40002 `MultiAccountBoundToOnePhone` More than one customer accounts bound to one phone.   

#### POST /Customers/sms/resetPasswordByPhoneToken

**Tag**:Customer

**Description**:
>
Reset password with token. (This is a public API).
 

**Request Parameters**:
>
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| token  | Token for retrieving password by SMS.    | form | string | true |
| newPassword   | New password to set.        | form | string | true |  
| httpCtx| Do not implement in clients.| formData| string (JSON) | false | 

**Response**  
>
Uses default content-types: *application/json*

**Success response**  
>
Http Status code: 200 OK   
**Response Body：**  
PROPERTIES  
arg: *x-customer-id*  
type: *string*  
description: *Customer id*  
required: *x-any*  
http: *x-any*  

**Failure response**
>  
Http Status code: 400  
Response Body: [SMSRequestError](abc.com)

**Error Code sample**: 
> 
`-400` `TOKEN_ALREADY_USED` Token has already been used.  
`-401` `TOKEN_INVALID` Token is invalid or expired.  
`-5` `EMAILS_DONT_MATCH` Emails do not match.  
`-4` `PASSWORD_NOT_STRONG` Password not strong enough.  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
3013 `EmailNotFound` Email not found.  
3014 `IncorrectUserPassword` The UserPassword is Incorrect.


#### POST /Customers/update

**Tag**: Customer

**Description**: Updates a Customer.  

**Request Body**:  
Uses default content-types: *application/json*  
Request Body: `CustomerUpdate`  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id | Customer id | header | string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
204 `EmailInUse` Emai is use by another member.  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
3011 `UserNameInUse` UserName is use by another member.  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
10005 `WrongCaptcha` Captcha may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20005 `MissingCaptcha` Captcha is missing.  
20009 `FrequentVerify` Verify too frequent.  

**Failure response**  
Http Status code: 423  
Response Body: [SMSRequestError](abc.com)  

**Error Code sample**:  
20006 `CaptchaRequired` Captcha is required.  



#### POST /Customers/update/patch

**Tag**: Customer

**Description**:  
> Updates a Customer with a patch like approach.

**Request body**  
> 
Uses default content-types: *application/json*  
Pass any fields from CustomerUpdatePatch which you want to be replaced/updated.  
CustomerUpdatePatch

**Request Parameters**:  
> 
| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id    | Customer id | header | string | true |   
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
> 
Uses default content-types: *application/json*

**Success response**  
> 
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
> 
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
> 
204 `EmailInUse` Email is use by another member.  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
3011 `UserNameInUse` UserName is use by another member.  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
10005 `WrongCaptcha` Captcha may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20005 `MissingCaptcha` Captcha is missing.  
20009 `FrequentVerify` Verify too frequent.  
-402 `ValidationNotMatch` Validation not matched for email or Phone token.  
422 `ValidationError` The `CustomerUpdatePatch` instance is not valid.  
5000 'UnexpectedError' Email Format Error.  

**Failure response**  
> 
Http Status code: 423  
Response Body:[SMSRequestError](abc.com)  

**Error Code sample**:  
> 
20006 `CaptchaRequired` Captcha is required.


#### POST /Customers/updateOpt

**Tag**: Customer

**Description**: Update a customer's Opt.    

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| x-customer-id | Customer id | header | string | true |
| communicationType| Customer's communication type(0-allow, 1-not allow, 2-not allow third party).| form| string | false |
| reason| Customer's update reason.| form| string | false |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  
 


#### POST /Customers/userAvailable

**Tag**: Customer

**Description**: Check if a username or email is already being used.    

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| user| Username or email.| formData| string | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
201 `EmailRegisteredActive` Email is in use by a registered customer.  
202 `EmailRegisteredInactive` Email is in use by an Closed customer.  


#### GET /Orders/forcegc

**Tag**: Order

**Description**: force node V8 execute Garbage Collection.    

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Properties: data: string  


#### GET /Orders/getHeap

**Tag**: Order

**Description**: get current heapdump value.    

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Properties: data: string  



#### GET /Orders/recordHeap

**Tag**: Order

**Description**: write into heap dump.    

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Properties: data: string  


#### GET /Orders/siebelTimeOut/{timeout}

**Tag**: Order

**Description**: test siebel timeout scenario.    

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| timeout| The timeout from siebel server.| path| string | true |
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Properties: data: string  
  

#### GET /Orders/{orderId}/items

**Tag**: Order

**Description**: List all the items sold for an order.    

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| orderId| The order id.| path| string | true |
| httpCtx| Do not implement in clients.| query| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Properties: ITEMS `OrderItem`  


#### POST /PaymentReferences/partner/transaction

**Tag**: PaymentReference

**Description**: Reference for SVC balance and transaction.

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| memIdentityNumber | customer id or MSR Card No to identify the customer | form | string | true |
| partnerCode | 3rd-party consumer code. `AMS` for Account management system| form | string | true |
| externalIdentity | External Identity for the customer. For AMS, should provide SVC Cardno | form | string | false |
| memIdentityType | Indicate using customer-id or MSR Card No. Only accept CRMMemberID or CardNumber| form | string | true |
| typeCode | Only support `Product` now| form | string | true |
| quantity | Number, default 1. For AMS provide 1. | form | string | false |
| receiptNumber | Unique Transaction number indicate.| form | string | true |
| productCode | Product Code. For AMS use `SVC`| form | string | true |
| points | Star amount. Default 0. For AMS provide 0 | form | string | false |
| amount | Transaction amount.Default is 0. For AMS, provide the SVC balance amount for the SVC card. | form | string | false |
| txnDate | Transaction date. Format is MM/DD/YYYY HH24:MI:SS and GMT +8| form | string | true |
| operator | Operator. For AMS provide `AMS` | form | string | false |
| sourceCode | Source System Code. For AMS provide `AMS`| form | string | true |
| storeNumber | Related Store number. For AMS provide null. | form | string | false |
| reserve1 | Reserved field. For AMS, provide null | form | string | false |
| reserve2 | Reserved field. For AMS, provide null | form | string | false |
| reserve3 | Reserved field. For AMS, provide null | form | string | false |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `x-any`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

  

#### GET /Wechats/getCard


**Description**: Fetch A Card from the Card Pool.

**Request Body**:  
Uses default content-types: *application/json*  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: {`msrCard`,`pin`, `customerId`}   

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
4001 `NoCardAvailable` No Card Available.
   
## Register User:

> _/api/Customers/create_ (existing API) `POST`

**Tag**: Customer WeChat

**Description**: Create a new customer.

**Request Body**:  
Uses default content-types: *application/json*  
Request Body: `CustomerCreate`  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| data| Model instance data| form| Object([CustomerCreate](#user-content-CustomerCreate)) | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

###<span id = "user-content-CustomerCreate">CustomerCreate</span>

`userName`: {type: 'string', required: true},

`password`: {type: 'string', required: true},

`cardNumber`: {type: 'string', required: true},

`cardPassword`: {type: 'string', required: true, description: 'Otherwise known as the card\'s `pin`'},

`email`: {type: 'string', required: true},

`firstName`: {type: 'string', required: true},

`lastName`: {type: 'string', required: true },

`gender`: {type: 'string', description: 'Only `Male` or `Female` are allowed'},

`birthday`: {type: 'string', required: true, description: 'Must have format of `MM/DD/YYYY`'},

`primaryCountry`: String,

`primaryState`: String,

`primaryCity`: String,

`primaryZip`: String,

`primaryAddress`: String,

`hobbies`: {type: 'string'},

`language`: {
    type: 'string',
    description: 'Only `CHS` or `ENU` are allowed',
    required: true
  },

  `notes`: {
    type: 'string'
  },

  `favouriteProduct`: {
    type: 'string'
  },

  `favouriteProductAlternate`: {
    type: 'string'
  },

  `cellPhone`: {
    type: 'string',
    description: 'Must have format of `/^((1[34578][0-9]))[0-9]{8}$/`',
    required: true
  },

  `homePhone`: {
    type: 'string'
  },

  `workPhone`: {
    type: 'string'
  },

  `fax`: {
    type: 'string'
  },

  `SourceCode`:{
    type:'string'
  },

  `optOut`: {
    type: 'number',
    description: '`0` - yes , `1` - no, `2` - don\'t allow third parties to send notifications'
  },

  `cellPhoneValidFlag`: {
    type: 'string'
  }


**Response**  
Uses default content-types: *application/json*  

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
104 `CardNotFound` The card is not found.  
105 `IncorrectPin` The card password incorrect  
108 `CardNotActive` The card status is not Active.  
201 `EmailRegisteredActive` Email is in use by a registered customer.  
202 `EmailRegisteredInactive`  Email is in use by an Closed customer.  
204 `EmailInUse` Email in use by another member.  
301 `InvalidStore` The store is not exist or the status of the store is closed.  
3008 `CardExpired` The card status is Active, but the end date of card is greater than today  
3009 `MemberNotOpen` The member status of card is not Open  
3011 `UserNameInUse` UserName use by another member  
402 `InvalidMemberID` The member does not exist or the member is not a registered active member.  
10001 `WrongAccessKey` AccessKey is wrong.  
10002 `MissingParams` Parameters may be missing.  
10003 `WrongSign` Signature is wrong.  
10004 `WrongParams` Parameters may be wrong.  
10005 `WrongCaptcha` Captcha may be wrong.  
20001 `FrequentSend` Send SMS too frequent.  
20002 `SendFailed` Send SMS failed.  
20003 `MissingNo` Phone number is missing.  
20005 `MissingCaptcha` Captcha is missing.  
20009 `FrequentVerify` Verify too frequent.    

Http Status code: 423  
Response Body: [SMSRequestError](abc.com)  

**Error Code sample**:  
20006 `CaptchaRequired` Captcha is required.  


#### POST /Wechats/uploadCard

**Description**: Upload the msrCard & Pin list to specific SFTP by `csv` format file and then store them in the Redis DB pool.

**Request Body**:  
Uses default content-types: *multipart/form-data*  

**Request Parameters**:

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| fileName| csv File name. Default with `cards_pool_data.csv`| form| file (JSON) | false |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

**Response**  
Uses default content-types: *application/json*

**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`  

**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)  

**Error Code sample**:  
4002 `WrongExcelHeader` Wrong Excel header.   
4003 `WrongFileExtension` File Extension incorrect.   
4007 `DirOrFileNotFound` Directory or File Not Found.   

***



> **Obsoleting**

~~Upload Cards Pins~~

~~/api/Wechats/upload `POST`~~

~~**Description**: Upload the msrCard & Pin list by `csv` format file and then store them in the Redis DB pool.~~

~~**Request Body**:~~
~~Uses default content-types: *multipart/form-data*~~

~~**Request Parameters**:~~

| Name   | Description  | Type  | Data Type| Mandatory  |
| ------ |:------------:|:-----:|:--------:| ----------:|
| wechatFile| csv File for upload| form| file (JSON) | true |
| httpCtx| Do not implement in clients.| formData| string (JSON) | false |

~~**Response**  
Uses default content-types: *application/json*~~

~~**Success response**  
Http Status code: 200 OK  
Response Body: `SuccessResponse`~~

~~**Failure response**  
Http Status code: 400  
Response Body: [SiebelRequestError](abc.com)~~

~~**Error Code sample**:  
4002 `WrongFileFormat` File format incorrect.   
4003 `WrongFileExtension` File Extension incorrect.  
4004 `UploadFail` upload is failed due to wrong attachment.  
401 `authorizationError` Authorization Required.  
403 `incorrectDir` wrong upload URL.~~

