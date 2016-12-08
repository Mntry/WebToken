# Getting started with Monetary WebToken

###Include the client on your page
##### Add the secure, hosted JavaScript client in the `<head>` of your page:
```html
<script src="https://token.monetary.co/v1/client"></script>
```

### Define the required form and controls

#####Give your payment form an ID:
```html
<form id="payment_form">
```

##### Add the following 4 payment information input controls to your form:
```html
<input type="text" data-token="card_number" />
<input type="text" data-token="exp_month" />
<input type="text" data-token="exp_year" />
<input type="text" data-token="cvv" />
```
**_Note:_** The payment info input controls must not have ID or Name attributes.

##### Define an input control to insert the token into:
```html
<input type="hidden" id="token" />
```

### Define required JavaScript
##### Define a JavaScript callback method for token events:
```javascript
var tokenCallback = function(response) {
  if (response.Error)
  {
    alert("Token error: " + response.Error);
  }
  else
  {
    var token = response.Token;
    document.getElementById("token").value = token;
  }
}
```

### Request a token!
##### Call `requestToken` with your public authenticator, payment form name, and token callback method:

```javascript
MonetaryWebToken.requestToken("[Public Key Goes Here]", "payment_form", tokenCallback);
```

##### The response object received by your callback method looks like this:
###### On Success
```javascript
{
  Token: "otu_ABCDEFGHIJ",
  Brand: "Visa",
  ExpirationMonth: "12",
  ExpirationYear: "2020",
  Last4: "1111"
}
```

###### On Failure
```javascript
{
  Error: "Failed to create token"
}
```

### Validation Helper Methods!
The Monetary WebToken client provides a few methods to help integrators validate their input fields, for card number, expiration date, and CVV that return `bool` values indicating input validity.

##### Validate Credit Card Number
```javascript
var validCard = MonetaryWebToken.validateCardNumber("4242424242424242");
```

##### Validate Expiration Date
```javascript
var validExpirationDate = MonetaryWebToken.validateExpirationDate("06", "2020");
```

##### Validate CVV
```javascript
var validCVV = MonetaryWebToken.validateCVV("123");
```

### Use your tokens!
Now that you've got fresh tokens in your payment form, you can submit the form and process token payments on Monetary's payment platform!

###Report bugs
If you encounter any bugs or issues with the latest version of WebToken, please report them to us by opening a [GitHub Issue](https://github.com/Mntry/WebToken/issues)!
