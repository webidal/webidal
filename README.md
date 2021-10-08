# Webidal v1 API documents

Webidal API `Endpoint:` ```http://127.0.0.1:8000/api/v1```

## Account API

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>User Registration</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/user/register/</code></p> 
        <p style="margin-bottom: 5px;">Add new user</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
    var data = JSON.stringify({
    "account_type": "Personal",
    "email": "********",
    "firstname": "john",
    "lastname": "Doe",
    "password": "********",
    "cnf-password": "********"
    });

    var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/user/register/',
    headers: { 
        'Content-Type': 'application/json'
    },
    data : data
    };

    axios(config)
    .then(function (response) {
    console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
    console.log(error);
    });
```




### Successful Response
```JSON
  {
    "status": true
    }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Email already exist"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| account_type         | True    | User account type (ie 'Personal' or 'Organization') `default Personal`   | String      |
| email         | True    | User valid email address   | String      |
| firstname         | True    | User first name or business name for Organization   | String      |
| lastname         | True    | User last name. `Not required for Organization account`   | String      |
| country_code         | False    | User country code  `default +234`    | String      |
| phone         | False    | User phone number   | string      |
| password         | True    | User password   | String      |
| cnf-password         | True    | User password confirmation   | String      |
| verification_type         | True    | User account verification type `Organization account only` `default Certificate of Incorporation`   | String      |
| location_state         | True    | Organization state `Organization account only`   | String      |
| location_city         | True    | Organization city `Organization account only`   | String      |
| streetaddress         | True    | Organization street address `Organization account only`   | String      |
| businesscac         | True    | Organization business registration proof `Organization account only`   | Image file      |

</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>User Login</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/user-token/</code></p> 
        <p style="margin-bottom: 5px;">Login to user account</p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
    var data = JSON.stringify({
    "email": "****@***.****",
    "password": "*******"
    });

    var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/user-token/',
    headers: { 
        'Content-Type': 'application/json'
    },
    data : data
    };

    axios(config)
    .then(function (response) {
    console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
    console.log(error);
    });

```




### Successful Response
```JSON
  {
    "refresh": "******",
    "access": "******",
    }
```

### Error Response
```JSON
  {
    "detail": "No active account found with the given credentials"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| email         | True    | User valid email address   | String      |
| password         | True    | User password   | String      |
</details>



<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Forgot Password</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/user/reset-password/</code></p> 
        <p style="margin-bottom: 5px;">Reset user password</p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
    var data = JSON.stringify({
    "forgot-email": "****@***.****"
    });

    var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/user/reset-password/',
    headers: { 
        'Content-Type': 'application/json'
    },
    data : data
    };

    axios(config)
    .then(function (response) {
    console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
    console.log(error);
    });

```

### Successful Response
```JSON
  {
    "status": true,
    "message": "Please check your email and follow the instructions to verify your account"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "User doesn't exists in our record"
  }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| forgot-email         | True    | User valid email address   | String      |
</details>


<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Edit Profile</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/user/edit-profile/</code></p> 
        <p style="margin-bottom: 5px;">Change user profile settings</p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
    var data = JSON.stringify({
    "current-password": "******",
    "password": "**********",
    "cnf-password": "**********"
    });

    var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/user/edit-profile/',
    headers: { 
        'Authorization': 'Bearer token-string', 
        'Content-Type': 'application/json'
    },
    data : data
    };

    axios(config)
    .then(function (response) {
    console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
    console.log(error);
    });

```

### Successful Response
```JSON
  {
    "status": true,
    "message": "Password changed"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Invalid current password"
  }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| email         | False    | if user wants to change email address   | String      |
| firstname         | False    | if user wants to change first name or business name for Organization   | String      |
| lastname         | False    | if user wants to change last name. `Not required for Organization account`   | String      |
| country_code         | False    | if user wants to change country code  `default +234`    | String      |
| phone         | False    | if user wants to change phone number   | string      |
| current-password         | False    | only required if user wants change password   | String      |
| password         | False    | User new password  | String      |
| cnf-password         | False    | User new password confirmation   | String      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>User Addres</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/user/change-address/{action_type}/</code></p> 
        <p style="margin-bottom: 5px;">Change user profile settings</p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
    var data = JSON.stringify({
    "address_id": 0,
    "location_state": "*******",
    "location_locality": "******",
    "streetaddress": "*****"
    });

    var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/user/change-address/{action_type}/',
    headers: { 
        'Authorization': 'Bearer token-string', 
        'Content-Type': 'application/json'
    },
    data : data
    };

    axios(config)
    .then(function (response) {
    console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
    console.log(error);
    });

```

### Successful Response
```JSON
  {
    "message": "Address saved",
    "status": true
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Unable to process your request at the moment"
  }
```
### Url Parameter
| parameter      | Values | Description |
| -------------- | -------- | ----------- |
| action_type         | newaddress    | Add new user address   |
|          | change    | Edit user address   | 
|          | setdefault    | Set user address as default   |
|          | deleteaddress    | Delete user address    |

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| address_id         | True    | User address Id. `Not required when using newaddress action_type`   | Integer      |
| location_state         | True    | User address state. `Not required when using setdefault & deleteaddress action_type`  | String      |
| location_locality         | True    | User address locality. `Not required when using setdefault & deleteaddress action_type`  | String      |
| streetaddress         | True    | User street address. `Not required when using setdefault & deleteaddress action_type`  | String      |
| set_as_default         | False    | Set user address as default. `Not applicable when using deleteaddress action_type`   | String      |
</details>



## Notification API

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Notification</strong></p>
        <p style="margin-bottom: 5px;"><strong>GET</strong> <code>/dashboard/notification/</code></p> 
        <p style="margin-bottom: 5px;">Get all notifications for authenticated user</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = '';

var config = {
  method: 'get',
  url: 'http://127.0.0.1:8000/api/v1/dashboard/notification/',
  headers: { 
    'Authorization': 'Bearer bearer-token', 
    'Content-Type': 'application/json'
  },
  data : data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});
```


### Successful Response
```JSON
  {
    "status": true,
    "unread": 16,
    "notifications": [
      {
          "id": 93,
          "message": "Auction PID:E3XA81 has started",
          "type": "Auction",
          "url": "/bidroom/E3XA81/",
          "status": "unread",
          "datetime": "2021-07-28 08:40:23.076052+00:00"
      }
    ]
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Unable to fetch notification"
    }
```
</details>


## Location API

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Find Location</strong></p>
        <p style="margin-bottom: 5px;"><strong>GET</strong> <code>/dashboard/location/find/</code></p> 
        <p style="margin-bottom: 5px;">Get all locations containing the given parameters</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var param = {
    "location": "lagos",
  };

  var config = {
    method: 'get',
    url: 'http://127.0.0.1:8000/api/v1/dashboard/location/find/',
    headers: { 
    },
  data : data
};

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "location": [
        "1004, Victoria Island, Lagos, Nigeria",
        "2nd Avenue Extension, Ikoyi, Lagos, Nigeria",
        "Abacha Estate, Ikoyi, Lagos, Nigeria",
        "Abaranje, Ikotun/Igando, Lagos, Nigeria"
    ]
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "unable to find location"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| location         | True    | text used for finding locations   | String      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Search Location</strong></p>
        <p style="margin-bottom: 5px;"><strong>GET</strong> <code>/dashboard/location/search/</code></p> 
        <p style="margin-bottom: 5px;">Get location data</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = {
    "country": "Nigeria",
  };

  var config = {
    method: 'get',
    url: 'http://127.0.0.1:8000/api/v1/dashboard/location/search/',
    headers: { },
    params : data
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "search_type": "state",
    "data": [
        "Abia",
        "Abuja",
        "Adamawa",
        "Akwa Ibom",
        "Anambra",
        "Bauchi",
    ]
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "no content found"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| country         | True    | country to search for locations   | String      |
| state         | False    | state within a selected country to search   | String      |
| city         | False    | city within a selected state to search `ensure state is not empty`   | String      |
</details>



## Transaction API

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Transaction History</strong></p>
        <p style="margin-bottom: 5px;"><strong>GET</strong> <code>/transaction/history/</code></p> 
        <p style="margin-bottom: 5px;">Get all transaction history</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = '';

  var config = {
    method: 'get',
    url: 'http://127.0.0.1:8000/api/v1/transaction/history/',
    headers: { 
      'Authorization': 'Bearer bearer-token',
      'Content-Type': 'application/json'
    },
    params : data
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "transactions": [
        {
            "id": 57,
            "trxid": "webidal-subscription-2b97fa27-833c-4357-94c4-9f5d173801e5",
            "type": "Subscription",
            "status": "Approved",
            "description": "You purchased Standard subscription",
            "amount": 10000.0,
            "datetime": "2021-07-14 22:38:30.314125+00:00"
        }
    ]
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "No content"
    }
```

</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Deposit</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/transaction/make/deposit/</code></p> 
        <p style="margin-bottom: 5px;">Get account deposit with flutterwave</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = JSON.stringify({
    "payment_amount": 2500.89,
    "payment_type": "Card"
  });

  var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/transaction/make/deposit/',
    headers: { 
      "Authorization": "Bearer brearer-token",
      "Content-Type": "application/json"
    },
    data : data
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```

### Successful Response
```JSON
  {
    "status": true,
    "public_key": "FLWPUBK_TEST-788e55961a4024f186aa9999dfb54f1e-X",
    "ref": "webidal-deposit-d92749ee-c297-4f1c-89c7-57f60aad4216",
    "amount": 2500.89,
    "payment_type": "card",
    "email": "dane1@qa.team",
    "phone": "08146089071",
    "name": "Dane Daniel"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Payment method not supported"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| payment_amount         | True    | Amount to be deposited   | Float      |
| payment_type         | True    | how payment will be made `options: 'Bank Transfer', 'Card'`   | String      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Withdraw request</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/transaction/make/withdraw/</code></p> 
        <p style="margin-bottom: 5px;">Place withdrawal request</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = JSON.stringify({
    "payment_amount": 2500.89
  });

  var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/transaction/make/withdraw/',
    headers: { 
      "Authorization": "Bearer brearer-token",
      "Content-Type": "application/json"
    },
    data : data
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```

### Successful Response
```JSON
  {
    "status": true,
    "withdraw_amount": 2500.89,
    "withdraw_fee": 25.0089,
    "amount_payable": 2475.8811,
    "message": "Withdraw request has been placed"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Insufficient balance"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| payment_amount         | True    | Amount to withdraw   | Float      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Token Purchase</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/transaction/token/purchase/</code></p> 
        <p style="margin-bottom: 5px;">Purchase token</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = JSON.stringify({
    "token_amount": 2
  });

  var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/transaction/token/purchase/',
    headers: { 
      "Authorization": "Bearer brearer-token",
      "Content-Type": "application/json"
    },
    data : data
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```

### Successful Response
```JSON
  {
    "status": true,
    "message": "2 token(s) purchased for 6000.00"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Insufficient balance"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| token_amount         | True    | Number of tokens to purchase   | Integer      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Subscription Purchase</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/transaction/subscription/purchase/</code></p> 
        <p style="margin-bottom: 5px;">Purchase subscription package</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = JSON.stringify({
    "subscription_type": "Standard",
    "auto_renew": true
  });

  var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/transaction/subscription/purchase/',
    headers: { 
      "Authorization": "Bearer brearer-token",
      "Content-Type": "application/json"
    },
    data : data
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```

### Successful Response
```JSON
  {
    "status": true,
    "message": "Standard Subscription purchase was successful"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Insufficient balance"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| subscription_type         | True    | Type of subscription package `options: 'Standard', 'Premium`   | String      |
| auto_renew         | True    | If user wants subscription package to automatically renew after expiry `default: true`   | Boolean      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Change Subscription Auto Renewal</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/transaction/subscription/renew/change/</code></p> 
        <p style="margin-bottom: 5px;">change auto renewal status for user subcription package</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = JSON.stringify({
    "auto_renew": false
  });

  var config = {
    method: 'post',
    url: 'http://127.0.0.1:8000/api/v1/transaction/subscription/renew/change/',
    headers: { 
      "Authorization": "Bearer brearer-token",
      "Content-Type": "application/json"
    },
    data : data
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```

### Successful Response
```JSON
  {
    "status": true,
    "message": "Subscription auto renewal has been set to False "
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Unable to process your request at the moment"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| auto_renew         | True    | If user wants subscription package to automatically renew after expiry   | Boolean      |
</details>



## Auction API

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Explore Auction</strong></p>
        <p style="margin-bottom: 5px;"><strong>GET</strong> <code>/auction/explore/{type}/</code></p> 
        <p style="margin-bottom: 5px;">Get all published auctions</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = '';

  var config = {
    method: 'get',
    url: 'http://127.0.0.1:8000/api/v1/auction/explore/{type}/',
    headers: { 
      'Authorization': 'Bearer bearer-token' - `optional`
    },
    params : data
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "auction": [
      {
          "id": 23,
          "auction_id": "A017B9",
          "category": "Real Estate",
          "subcategory": "Land",
          "title": "2 Acres FOR SALE",
          "description": "Table Land On Orchid Hotel Road, Directly Opposite The Popular Coop-Lag Gardens",
          "display_image": "https://res.cloudinary.com/do7imvim7/image/upload/v1624559975/webidal/auctions/A017B9/displayimage/ekfravlbqej64i8fule0.jpg",
          "status": "Live",
          "type": "Down Offer",
          "start_date": "2021-07-13T18:38:49Z",
          "end_date": "2021-07-29T08:31:11Z",
          "base_price": 103050000,
          "current_price": 103140000.0,
          "bidders_count": 2,
          "auctioneer_verified": false,
          "auctioneer_name": "James",
          "is_favourite": true,
          "sale_type": "For Sale",
          "location_city": "Isolo",
          "location_state": "Lagos",
          "location_country": "Nigeria",
          "land_type": "Plots",
          "land_qty": 2.0
      }
    ]
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "No content"
    }
```
### Url Parameter
| parameter      | Values | Description |
| -------------- | -------- | ----------- |
| type         | all    | displays all auction   |
|          | search    | search for specific autions with queries parameters provided   |

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| auction_type         | False    | The type of auction you like to search for   | String      |
| sales_type         | False    | Search for auction by the sales type  | String      |
| subcategory         | False    | Search for auction by subcategory  | String      |
| location         | False    | Search for auction by location  | String      |
| land_type         | False    | Search for auction by land_type `used when subcategory is set as Land`   | String      |
| land_qty         | False    | Search for auction by land_qty `used when subcategory is set as Land and land_type is provided`   | String      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Create Auction</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/auction/create/{type}/</code></p> 
        <p style="margin-bottom: 5px;">Create real estate auctions</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = new FormData();
  data.append('saletype', 'For Sale');
  data.append('property_id', 'AXOP87');
  data.append('property_title', '10 plots of land for sale in magodo');
  data.append('property_description', '10 plots of land with a lake side view in jason estate');
  data.append('auction_type', 'Classic Auction');
  data.append('property_type', 'Land');
  data.append('location_country', 'Nigeria');
  data.append('location_state', 'Lagos');
  data.append('location_locality', 'Magodo');
  data.append('property_street', '2 opan street');
  data.append('property_inspection', '3 Days');
  data.append('auction_start_date_time', '2021-10-9T20:50:23.808Z');
  data.append('auction_duration', '3 hours');
  data.append('inspection_end_date_time', '2021-10-08T20:54:18.222Z');
  data.append('auction_base_Price', '3000000.59');
  data.append('landtype', 'Plots');
  data.append('land_qty', '10');
  data.append('property_image_obj', image_file);
  data.append('condition_Virgin_Land', 'on');
  data.append('condition_Water_Log', 'on');
  data.append('features_fenced', 'on');
  data.append('features_lake', 'on');
  data.append('document_c_of_o', 'on');
  data.append('document_survey', 'on');
  data.append('documents_upload_c_of_o', document_file);
  data.append('documents_upload_survey', document_file);
  data.append('images_view1', image_file);
  data.append('images_interior', image_file);

  var config = {
    method: 'POST',
    url: 'http://127.0.0.1:8000/api/v1/auction/create/{type}/',
    headers: { 
      'Authorization': 'Bearer bearer-token',
      'Content-Type': 'multipart/formdata'
    },
    data : data
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "message": "Auction PID:AXOP87 Created successfully and Publish",
    "redirect_url": "/bidroom/AXOP87/"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "You don't have the permissions to create an auction"
    }
```
### Url Parameter
| parameter      | Values | Description |
| -------------- | -------- | ----------- |
| type         | publish    | Publish auction to public listing after creation or modification   |
|          | draft    | Save auction as draft accessible to auction author only   |

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| saletype         | True    | Auction type of sale `options: 'For Sale', 'For Rent', 'For Lease', 'For Shortlet'`  | String      |
| property_id         | True    | Generated auction ID  | String      |
| property_title         | True    | Auction short title  | String      |
| property_description         | True    | Description about the auction `not required if url parameter {type} is draft`  | String      |
| auction_type         | True    | Type of webidal auction `options: 'Classic Auction', 'Down Offer'`   | String      |
| property_type         | True    | Real Estate property type `currently only Land option is available`   | String      |
| location_country         | True    | Auction property location country   | String      |
| location_state         | True    | Auction property location state   | String      |
| location_locality         | True    | Auction property location locality   | String      |
| property_street         | False    | Auction property street address   | String      |
| property_inspection         | True    | Inspection duration in days `options: '3 Days', '5 Days', '10 Days', '12 Days', '14 Days'`   | String      |
| auction_start_date_time         | True    | Auction start datetime `default 1 day after the inspection end date`   | Datetime `isoString`      |
| auction_duration         | True    | Auction duration from auction start datetime `default '1 hour'`   | String      |
| inspection_end_date_time         | True    | Inpection end datetime from the inpection duration    | Datetime `isoString`      |
| auction_base_Price         | True    | Auction starting price `not required if url parameter {type} is draft`   | Float      |
| landtype         | True    | Auction property unit measurement `options: 'Plots', 'Acres', 'Hectares'. default Plots`   | String      |
| land_qty         | True    | Amount of the land measurement `not required if url parameter {type} is draft`   | String      |
| property_image_obj         | True    | Auction public display image `not required if url parameter {type} is draft`   | Image File      |
| condition_*         | True    | Dynamic auction property conditions, `prefix with condition_` `not required if url parameter {type} is draft`   | String      |
| features_*         | True    | Dynamic auction property features `prefix with features_` `not required if url parameter {type} is draft`   | String      |
| documents_*         | True    | Dynamic auction property document name `prefix with documents_` `not required if url parameter {type} is draft`   | String      |
| documents_upload_*         | True    | Dynamic auction property document file with the corresponding document name `prefix with document_` `not required if url parameter {type} is draft`   | Files      |
| images_*         | True    | Dynamic auction property images `prefix with images_` `not required if url parameter {type} is draft`   | Image File      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Generate Auction ID</strong></p>
        <p style="margin-bottom: 5px;"><strong>GET</strong> <code>/auction/generate_id/</code></p> 
        <p style="margin-bottom: 5px;">Generate auction id for creating auction</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');

  var config = {
    method: 'GEt',
    url: 'http://127.0.0.1:8000/api/v1/auction/generate_id/',
    headers: { 
      'Authorization': 'Bearer bearer-token',
      'Content-Type': 'application/json'
    }
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "auction_id": "252327"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "You don't have the permissions to perform this action"
    }
```
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Auction Draft List</strong></p>
        <p style="margin-bottom: 5px;"><strong>GET</strong> <code>/auction/draft/list/</code></p> 
        <p style="margin-bottom: 5px;">Get the total auctions saved as draft from an authenticated business account</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');

  var config = {
    method: 'GEt',
    url: 'http://127.0.0.1:8000/api/v1/auction/auction/draft/list/',
    headers: { 
      'Authorization': 'Bearer bearer-token',
      'Content-Type': 'application/json'
    }
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "count": 3,
    "auctions": [
      {
          "id": 24,
          "auction_id": "658579",
          "title": "10 plosts of land for sale",
          "description": "fdffdffffffffffffffffffffffffffffffffffffffffffff",
          "created_at": "2021-07-05T11:36:03Z"
      },
      {
          "id": 25,
          "auction_id": "081501",
          "title": "Eren's house for lease",
          "description": "",
          "created_at": "2021-07-05T11:37:02.715776Z"
      },
      {
          "id": 26,
          "auction_id": "13X25E",
          "title": "fgfgfddd",
          "description": "",
          "created_at": "2021-07-05T11:39:12.111278Z"
      }
    ]
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "You don't have the permissions to perform this action"
    }
```
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Auction Draft Edit</strong></p>
        <p style="margin-bottom: 5px;"><strong>GET</strong> <code>/auction/draft/edit/</code></p> 
        <p style="margin-bottom: 5px;">Get the auctions details for editting</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = JSON.stringify({
  "draft_auction": [
    "658579"
  ]
});
  var config = {
    method: 'GET',
    url: 'http://127.0.0.1:8000/api/v1/auction/auction/draft/edit/',
    headers: { 
      'Authorization': 'Bearer bearer-token',
      'Content-Type': 'application/json'
    }
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "auctions": [
      {
          "id": 25,
          "auction_id": "081501",
          "title": "Eren's house for lease",
          "description": "",
          "auction_type": "Classic Auction",
          "property_type": "Land",
          "property_image_url": "",
          "auction_start_date": "2021-07-09T11:36:15Z",
          "auction_end_date": "2021-07-09T12:36:15Z",
          "auction_base_price": 0.0,
          "auction_down_price": 0.0,
          "sales_type": "For Lease",
          "land_type": "Plots",
          "land_qty": 0.0,
          "location": {
              "location_country": "Nigeria",
              "location_state": "Abia",
              "location_locality": "Aba",
              "location_street": ""
          },
          "inspections_dates": {
              "count": "3 Days",
              "dates": [
                  "2021-07-07T23:00:00Z",
                  "2021-07-06T23:00:00Z",
                  "2021-07-05T23:00:00Z"
              ]
          }
      }
    ]
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "You don't have the permissions to perform this action"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| draft_auction         | True    | List of selected auctions for editting by auctions id  | List      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Auction Draft Delete</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/auction/draft/delete/</code></p> 
        <p style="margin-bottom: 5px;">Get the auctions details for deletion</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  var data = JSON.stringify({
  "draft_auction": [
    "658579"
  ]
});
  var config = {
    method: 'POST',
    url: 'http://127.0.0.1:8000/api/v1/auction/auction/draft/delete/',
    headers: { 
      'Authorization': 'Bearer bearer-token',
      'Content-Type': 'application/json'
    }
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "message": "Auctions ['658579'] have been deleted"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "You don't have the permissions to perform this action"
    }
```

### Query Parameter
| parameter      | Required | Description | Data Type |
| -------------- | -------- | ----------- | ----------|
| draft_auction         | True    | List of selected auctions for deletion by auctions id  | List      |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Cancel Auction</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/auction/cancel/{auction_id}/</code></p> 
        <p style="margin-bottom: 5px;">To cancel an auction when in Scheduled or Live stage</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  
  var config = {
    method: 'POST',
    url: 'http://127.0.0.1:8000/api/v1/auction/auction/cancel/AXOP84/',
    headers: { 
      'Authorization': 'Bearer bearer-token',
      'Content-Type': 'application/json'
    }
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "message": "Auction successfully cancelled"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "Auction is already cancelled"
  }
```

### Url Parameter
| parameter      | Description |
| -------------- | ----------- |
| auction_id     | the auction id for auction to be cancelled  |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Favourite Auction</strong></p>
        <p style="margin-bottom: 5px;"><strong>POST</strong> <code>/auction/favourite/{auction id}/</code></p> 
        <p style="margin-bottom: 5px;">To favourite and unfavourite an auction</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  
  var config = {
    method: 'POST',
    url: 'http://127.0.0.1:8000/api/v1/auction/auction/favourite/35/',
    headers: { 
      'Authorization': 'Bearer bearer-token',
      'Content-Type': 'application/json'
    }
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "type": "add"
  }
```
```JSON
  {
    "status": true,
    "type": "remove"
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "unable to perform action at the moment"
  }
```

### Url Parameter
| parameter      | Description |
| -------------- | ----------- |
| auction id     | the auction id for auction to change favourite status `id should be the valid id assigned to the property`  |
</details>

<details style="border-bottom: 1px solid var(--color-border-secondary);">
    <summary>
        <p style="margin-bottom: 5px;"><strong>Recently Viewed Auction</strong></p>
        <p style="margin-bottom: 5px;"><strong>GET</strong> <code>/auction/recentlyviewed/</code></p> 
        <p style="margin-bottom: 5px;">Get all viewed auctions with in the last 14 days</code></p> 
    </summary>

### Sample Call `axios`
```javascript
  var axios = require('axios');
  
  var config = {
    method: 'POST',
    url: 'http://127.0.0.1:8000/api/v1/auction/auction/recentlyviewed/',
    headers: { 
      'Authorization': 'Bearer bearer-token',
      'Content-Type': 'application/json'
    }
  };

  axios(config)
  .then(function (response) {
    console.log(JSON.stringify(response.data));
  })
  .catch(function (error) {
    console.log(error);
  });
```




### Successful Response
```JSON
  {
    "status": true,
    "count": 1,
    "auctions": [
      {
          "id": 23,
          "auction_id": "A017B9",
          "title": "2 Acres FOR SALE",
          "description": "Table Land On Orchid Hotel Road, Directly Opposite The Popular Coop-Lag Gardens",
          "property_image_url": "https://res.cloudinary.com/do7imvim7/image/upload/v1624559975/webidal/auctions/A017B9/displayimage/ekfravlbqej64i8fule0.jpg",
          "auction_type": "Down Offer",
          "auction_status": "Live",
          "images_count": 4,
          "is_favourite": true,
          "location": {
              "location_country": "Nigeria",
              "location_state": "Lagos",
              "location_locality": "Isolo"
          },
          "sales_type": "For Sale",
          "property_type": "Land",
          "auction_price": 103050000.0,
          "current_best_offer": 103140000.0,
          "total_bidders": 2,
          "auction_end_datetime": "2021-07-29T08:31:11Z",
          "key_features": {
              "Fenced": true,
              "Street Light": false
          }
      }
    ]
  }
```

### Error Response
```JSON
  {
    "status": false,
    "message": "You haven't viewed any auction in the last 14 days."
  }
```
</details>
