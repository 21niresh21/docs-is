# Request user information

User information is encoded inside the ID token returned along with the access token. In addition to that, OpenID Connect provides the userinfo endpoint <!-- [userinfo endpoint](https://openid.net/specs/openid-connect-core-1_0.html#UserInfo)--> to obtain user
information as a payload. The application should send a request with the access token to invoke the userinfo endpoint.

**Userinfo endpoint**

``` 
https://api.asgardeo.io/t/<organization_name>/oauth2/userinfo
```

**Sample request**

<CodeGroup>
<CodeGroupItem title="cURL" active>

```bash
curl --location --request GET 'https://api.asgardeo.io/t/{organization}/oauth2/userinfo' \
--header 'Authorization: Bearer {your_access_token}'
```

</CodeGroupItem>

<CodeGroupItem title="JavaScript - jQuery">

```js
var settings = {
    "url": "https://api.asgardeo.io/t/{organization}/oauth2/userinfo",
    "method": "GET",
    "timeout": 0,
    "headers": {
        "Authorization": "Bearer {your_access_token}"
    },
};

$.ajax(settings).done(function (response) {
    console.log(response);
});
```

</CodeGroupItem>

<CodeGroupItem title="Nodejs - Axios">

```js
var axios = require('axios');

var config = {
    method: 'get',
    url: 'https://api.asgardeo.io/t/{organization}/oauth2/userinfo',
    headers: {
        'Authorization': 'Bearer {your_access_token}'
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

</CodeGroupItem>
</CodeGroup>

**Default sample response**  
{{ product_name }} returns only the `sub` claim if there are no user attributes shared with the application.

```json
{
  "sub": "user1@bifrost.com"
}
```

You can customize the user information in the response by [configuring user attributes](../../guides/authentication/user-attributes/enable-attributes-for-oidc-app/) on the registered application.
<br>