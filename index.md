---
title: Pinch.ai API definition file v0.0.1
language_tabs:
  - java: Java
  - python: Python
language_clients:
  - java: ""
  - python: ""
toc_footers: []
includes: []
search: false
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="pinch-ai-api-definition-file">Pinch.ai API definition file v0.0.1</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

< Provides the definition of API endpoints for accessing Pinch.ai functionality during return processing. Three operations are currently supported&#58; (a) create a new return from a prior order; (b) update the status of a return as it is processed (including closing the return when completed; and (c) querying the status of a return.

Base URLs:

* <a href="https://api.pinch.ai/v1">https://api.pinch.ai/v1</a>

* <a href="https://staging-api.pinch.ai/v1">https://staging-api.pinch.ai/v1</a>

<h1 id="pinch-ai-api-definition-file-default">Default</h1>

## < Used to provide information about a shopping cart during the sales process, prior to checkout. This operations determines which policies (return, shipping, etc) can be applied to each of the items in the cart; it also allows Pinch to build behavioral information about the customer interactions with the site.

<a id="opIdanalyzeCart"></a>

> Code samples

```java
URL obj = new URL("https://api.pinch.ai/v1/cart/analyze");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-merchant-id': 'string'
}

r = requests.post('https://api.pinch.ai/v1/cart/analyze', headers = headers)

print(r.json())

```

`POST /cart/analyze`

> Body parameter

```json
{
  "merchantCartID": "string",
  "previousCartId": "string",
  "totalCartCost": {
    "currencyCode": 840,
    "amount": 0.1
  },
  "cart": [
    {
      "product": {
        "identifierType": "UPC",
        "identifier": "string",
        "category": "Fashion"
      },
      "count": 1,
      "perItemPrice": {
        "currencyCode": 840,
        "amount": 0.1
      }
    }
  ],
  "customer": {
    "name": "string",
    "deviceFingerprints": [
      {
        "algorithm": "string",
        "fingerPrint": "string"
      }
    ],
    "contactInformation": [
      {
        "contactType": "ContactAddress",
        "address": {
          "line1": "string",
          "line2": "string",
          "line3": "string",
          "line4": "string",
          "city": "string",
          "state": "string",
          "postalCode": "string",
          "country": "string",
          "geoCode": {
            "longitude": -180,
            "latitude": -90
          }
        },
        "addressType": "Billing"
      }
    ]
  },
  "merchant": {
    "locationID": "string"
  },
  "customData": {
    "property1": {},
    "property2": {}
  },
  "timestamp": 0
}
```

<h3 id="<-used-to-provide-information-about-a-shopping-cart-during-the-sales-process,-prior-to-checkout.-this-operations-determines-which-policies-(return,-shipping,-etc)-can-be-applied-to-each-of-the-items-in-the-cart;-it-also-allows-pinch-to-build-behavioral-information-about-the-customer-interactions-with-the-site.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-merchant-id|header|string|true|Merchant Id from auth-service|
|body|body|[AnalyzeRequestPayload](#schemaanalyzerequestpayload)|true|none|

> Example responses

> 200 Response

```json
{
  "pinchCartID": "string",
  "merchantCartID": "string",
  "productPolicies": [
    {
      "product": {
        "identifierType": "UPC",
        "identifier": "string",
        "category": "Fashion"
      },
      "count": 0,
      "policies": [
        {
          "policyID": "string",
          "policyName": "string",
          "policyTerms": "string",
          "policyType": "Type1"
        }
      ]
    }
  ],
  "cartPolicies": [
    {
      "policyID": "string",
      "policyName": "string",
      "policyTerms": "string",
      "policyType": "Type1"
    }
  ]
}
```

<h3 id="<-used-to-provide-information-about-a-shopping-cart-during-the-sales-process,-prior-to-checkout.-this-operations-determines-which-policies-(return,-shipping,-etc)-can-be-applied-to-each-of-the-items-in-the-cart;-it-also-allows-pinch-to-build-behavioral-information-about-the-customer-interactions-with-the-site.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[AnalyzeResultPayload](#schemaanalyzeresultpayload)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad Request|None|

<aside class="success">
This operation does not require authentication
</aside>

## < Called to denote that a user has purchased a cart, and which policies were selected for each item. The purchased or applied policies are denoted by the unique policy reference number that was supplied during the analyze cart operation; this policy reference number is unique to the instance of the policy as applied to the item and therefore should be the exact reference number for the item (not the reference number for the same policy applied to a different item).

<a id="opIdpurchaseCart"></a>

> Code samples

```java
URL obj = new URL("https://api.pinch.ai/v1/cart/purchase");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-merchant-id': 'string'
}

r = requests.post('https://api.pinch.ai/v1/cart/purchase', headers = headers)

print(r.json())

```

`POST /cart/purchase`

> Body parameter

```json
{
  "cartID": "string",
  "merchantCartID": "string",
  "merchantOrderID": "string",
  "orderStatus": "Pending",
  "paymentInfo": [
    {
      "amount": {
        "currencyCode": 840,
        "amount": 0.1
      },
      "instrument": null,
      "last4": "string",
      "BIN": "string",
      "postalCode": "string",
      "method": "NotPresent",
      "auth": "string",
      "AID": "string"
    }
  ],
  "purchasedPolicies": [
    "string"
  ],
  "timestamp": 0
}
```

<h3 id="<-called-to-denote-that-a-user-has-purchased-a-cart,-and-which-policies-were-selected-for-each-item.-the-purchased-or-applied-policies-are-denoted-by-the-unique-policy-reference-number-that-was-supplied-during-the-analyze-cart-operation;-this-policy-reference-number-is-unique-to-the-instance-of-the-policy-as-applied-to-the-item-and-therefore-should-be-the-exact-reference-number-for-the-item-(not-the-reference-number-for-the-same-policy-applied-to-a-different-item).-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-merchant-id|header|string|true|Merchant Id from auth-service|
|body|body|[PurchaseRequestPayload](#schemapurchaserequestpayload)|true|none|

> Example responses

> 200 Response

```json
{
  "orderID": "string"
}
```

<h3 id="<-called-to-denote-that-a-user-has-purchased-a-cart,-and-which-policies-were-selected-for-each-item.-the-purchased-or-applied-policies-are-denoted-by-the-unique-policy-reference-number-that-was-supplied-during-the-analyze-cart-operation;-this-policy-reference-number-is-unique-to-the-instance-of-the-policy-as-applied-to-the-item-and-therefore-should-be-the-exact-reference-number-for-the-item-(not-the-reference-number-for-the-same-policy-applied-to-a-different-item).-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[PurchaseResultPayload](#schemapurchaseresultpayload)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The cart ID specified was not found|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|The card ID was already purchased or abandoned|None|

<aside class="success">
This operation does not require authentication
</aside>

## < Called to explicitly abandon a shopping cart. Optional operation as the shopping cart will time out if it is not explicitly marked as purchased. This will most commonly be used if the user empties their cart or takes a similar abandonment action. Note that if the user adjusts their cart (adds / removes items) there is no need to abandon the cart. Rather, provide the previously Pinch assigned cart ID as the previousCartID on the new analyze call.

<a id="opIdabandonCart"></a>

> Code samples

```java
URL obj = new URL("https://api.pinch.ai/v1/cart/abandon");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-merchant-id': 'string'
}

r = requests.post('https://api.pinch.ai/v1/cart/abandon', headers = headers)

print(r.json())

```

`POST /cart/abandon`

> Body parameter

```json
{
  "cartID": "string"
}
```

<h3 id="<-called-to-explicitly-abandon-a-shopping-cart.-optional-operation-as-the-shopping-cart-will-time-out-if-it-is-not-explicitly-marked-as-purchased.-this-will-most-commonly-be-used-if-the-user-empties-their-cart-or-takes-a-similar-abandonment-action.-note-that-if-the-user-adjusts-their-cart-(adds-/-removes-items)-there-is-no-need-to-abandon-the-cart.-rather,-provide-the-previously-pinch-assigned-cart-id-as-the-previouscartid-on-the-new-analyze-call.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-merchant-id|header|string|true|Merchant Id from auth-service|
|body|body|[AbandonRequestPayload](#schemaabandonrequestpayload)|true|none|

> Example responses

> 200 Response

```json
"string"
```

<h3 id="<-called-to-explicitly-abandon-a-shopping-cart.-optional-operation-as-the-shopping-cart-will-time-out-if-it-is-not-explicitly-marked-as-purchased.-this-will-most-commonly-be-used-if-the-user-empties-their-cart-or-takes-a-similar-abandonment-action.-note-that-if-the-user-adjusts-their-cart-(adds-/-removes-items)-there-is-no-need-to-abandon-the-cart.-rather,-provide-the-previously-pinch-assigned-cart-id-as-the-previouscartid-on-the-new-analyze-call.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|string|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The cart ID specified was not found|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|The card ID was already purchased or abandoned|None|

<aside class="success">
This operation does not require authentication
</aside>

## < Initiates the return of one or more items from a previously ordered cart. The cart MUST have been purchased with the cart API; the orderID returned by that call is used to find the cart in question. Furthermore, that order has to have been marked as delivered.

<a id="opIdreturnItems"></a>

> Code samples

```java
URL obj = new URL("https://api.pinch.ai/v1/return");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-merchant-id': 'string'
}

r = requests.post('https://api.pinch.ai/v1/return', headers = headers)

print(r.json())

```

`POST /return`

> Body parameter

```json
{
  "orderID": "string",
  "merchantOrderID": "string",
  "returnedItems": [
    {
      "product": {
        "identifierType": "UPC",
        "identifier": "string",
        "category": "Fashion"
      },
      "count": 1,
      "policyID": "string",
      "reason": "string"
    }
  ],
  "customer": {
    "name": "string",
    "deviceFingerprints": [
      {
        "algorithm": "string",
        "fingerPrint": "string"
      }
    ],
    "contactInformation": [
      {
        "contactType": "ContactAddress",
        "address": {
          "line1": "string",
          "line2": "string",
          "line3": "string",
          "line4": "string",
          "city": "string",
          "state": "string",
          "postalCode": "string",
          "country": "string",
          "geoCode": {
            "longitude": -180,
            "latitude": -90
          }
        },
        "addressType": "Billing"
      }
    ]
  },
  "reason": "string",
  "timestamp": 0
}
```

<h3 id="<-initiates-the-return-of-one-or-more-items-from-a-previously-ordered-cart.-the-cart-must-have-been-purchased-with-the-cart-api;-the-orderid-returned-by-that-call-is-used-to-find-the-cart-in-question.-furthermore,-that-order-has-to-have-been-marked-as-delivered.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-merchant-id|header|string|true|Merchant Id from auth-service|
|body|body|[ReturnRequestPayload](#schemareturnrequestpayload)|true|none|

> Example responses

> 200 Response

```json
{
  "items": [
    {
      "product": {
        "identifierType": "UPC",
        "identifier": "string",
        "category": "Fashion"
      },
      "returnID": "string",
      "status": "ALLOW",
      "reason": "string"
    }
  ]
}
```

<h3 id="<-initiates-the-return-of-one-or-more-items-from-a-previously-ordered-cart.-the-cart-must-have-been-purchased-with-the-cart-api;-the-orderid-returned-by-that-call-is-used-to-find-the-cart-in-question.-furthermore,-that-order-has-to-have-been-marked-as-delivered.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[ReturnResponsePayload](#schemareturnresponsepayload)|

<aside class="success">
This operation does not require authentication
</aside>

## < Called to update the status of a previously created return. This call will be used to denote that a return label was generated, the return item was received, the refund was generated, etc.

<a id="opIdupdateReturnStatus"></a>

> Code samples

```java
URL obj = new URL("https://api.pinch.ai/v1/return/{returnID}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PATCH");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-merchant-id': 'string'
}

r = requests.patch('https://api.pinch.ai/v1/return/{returnID}', headers = headers)

print(r.json())

```

`PATCH /return/{returnID}`

> Body parameter

```json
{
  "updateType": "string",
  "newStatus": "Opened",
  "comment": "string",
  "timestamp": 0
}
```

<h3 id="<-called-to-update-the-status-of-a-previously-created-return.-this-call-will-be-used-to-denote-that-a-return-label-was-generated,-the-return-item-was-received,-the-refund-was-generated,-etc.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|returnID|path|string|true|ID of the return to update|
|x-merchant-id|header|string|true|Merchant Id from the auth-service|
|body|body|[ReturnUpdateRequestPayload](#schemareturnupdaterequestpayload)|true|none|

> Example responses

> 200 Response

```json
"string"
```

<h3 id="<-called-to-update-the-status-of-a-previously-created-return.-this-call-will-be-used-to-denote-that-a-return-label-was-generated,-the-return-item-was-received,-the-refund-was-generated,-etc.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|string|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The caller did not have permission to access that return|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The return ID specified was not found|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|The return ID was already closed|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|The requested update could not be performed|string|

<aside class="success">
This operation does not require authentication
</aside>

## < Called to get the current status of the return. This operation allows merchants and their business partners to query on the status of a return.

<a id="opIdgetReturnStatus"></a>

> Code samples

```java
URL obj = new URL("https://api.pinch.ai/v1/return/{returnID}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-merchant-id': 'string'
}

r = requests.get('https://api.pinch.ai/v1/return/{returnID}', headers = headers)

print(r.json())

```

`GET /return/{returnID}`

<h3 id="<-called-to-get-the-current-status-of-the-return.-this-operation-allows-merchants-and-their-business-partners-to-query-on-the-status-of-a-return.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|returnID|path|string|true|ID of the return to update|
|x-merchant-id|header|string|true|Merchant Id from auth-service|

> Example responses

> 200 Response

```json
{
  "state": "Opened",
  "shippingLabel": {
    "carrier": "string",
    "carrierCode": "USPS",
    "trackingNumber": "string",
    "state": "Created"
  },
  "historyMap": {
    "property1": [
      {
        "timestamp": "string",
        "oldState": "string",
        "newState": "string",
        "comment": "string"
      }
    ],
    "property2": [
      {
        "timestamp": "string",
        "oldState": "string",
        "newState": "string",
        "comment": "string"
      }
    ]
  },
  "coveredItems": [
    {
      "identifierType": "UPC",
      "identifier": "string",
      "category": "Fashion"
    }
  ]
}
```

<h3 id="<-called-to-get-the-current-status-of-the-return.-this-operation-allows-merchants-and-their-business-partners-to-query-on-the-status-of-a-return.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|[ReturnStatusResultPayload](#schemareturnstatusresultpayload)|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The caller did not have permission to access that return|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|The return ID specified was not found|None|

<aside class="success">
This operation does not require authentication
</aside>

## < Called to update the disposition outcome of previously returned item.

<a id="opIddispositionReturn"></a>

> Code samples

```java
URL obj = new URL("https://api.pinch.ai/v1/return/disposition/{returnID}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'x-merchant-id': 'string'
}

r = requests.post('https://api.pinch.ai/v1/return/disposition/{returnID}', headers = headers)

print(r.json())

```

`POST /return/disposition/{returnID}`

> Body parameter

```json
[
  {
    "itemID": "string",
    "inspectionNotes": "string",
    "returnedItemCondition": "NEW",
    "dispositionOutcome": "RESTOCK",
    "returnMode": "IN_STORE",
    "refundMethod": "ORIGINAL_TENDER",
    "warehouseId": "string",
    "storeId": "string",
    "images": [
      "string"
    ],
    "abuseType": "STOLEN_MERCHANDISE",
    "timestamp": 0
  }
]
```

<h3 id="<-called-to-update-the-disposition-outcome-of-previously-returned-item.-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|returnID|path|string|true|ID of the return to update|
|x-merchant-id|header|string|true|Merchant Id from the auth-service|
|body|body|[DispositionRequestPayload](#schemadispositionrequestpayload)|true|none|

> Example responses

> 200 Response

```json
"string"
```

<h3 id="<-called-to-update-the-disposition-outcome-of-previously-returned-item.-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Success|string|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|The caller did not have permission to access that return|None|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|return_id was not found|None|
|409|[Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)|The disposition for the item against the return with return ID was already closed|None|
|422|[Unprocessable Entity](https://tools.ietf.org/html/rfc2518#section-10.3)|The requested disposition cannot be created|None|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocS_AbandonRequestPayload">AbandonRequestPayload</h2>
<!-- backwards compatibility -->
<a id="schemaabandonrequestpayload"></a>
<a id="schema_AbandonRequestPayload"></a>
<a id="tocSabandonrequestpayload"></a>
<a id="tocsabandonrequestpayload"></a>

```json
{
  "cartID": "string"
}

```

The payload for an abandon cart operations

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|cartID|string|true|none|The (Pinch generated) cart ID supplied when analyzing the cart|

<h2 id="tocS_AnalyzeRequestPayload">AnalyzeRequestPayload</h2>
<!-- backwards compatibility -->
<a id="schemaanalyzerequestpayload"></a>
<a id="schema_AnalyzeRequestPayload"></a>
<a id="tocSanalyzerequestpayload"></a>
<a id="tocsanalyzerequestpayload"></a>

```json
{
  "merchantCartID": "string",
  "previousCartId": "string",
  "totalCartCost": {
    "currencyCode": 840,
    "amount": 0.1
  },
  "cart": [
    {
      "product": {
        "identifierType": "UPC",
        "identifier": "string",
        "category": "Fashion"
      },
      "count": 1,
      "perItemPrice": {
        "currencyCode": 840,
        "amount": 0.1
      }
    }
  ],
  "customer": {
    "name": "string",
    "deviceFingerprints": [
      {
        "algorithm": "string",
        "fingerPrint": "string"
      }
    ],
    "contactInformation": [
      {
        "contactType": "ContactAddress",
        "address": {
          "line1": "string",
          "line2": "string",
          "line3": "string",
          "line4": "string",
          "city": "string",
          "state": "string",
          "postalCode": "string",
          "country": "string",
          "geoCode": {
            "longitude": -180,
            "latitude": -90
          }
        },
        "addressType": "Billing"
      }
    ]
  },
  "merchant": {
    "locationID": "string"
  },
  "customData": {
    "property1": {},
    "property2": {}
  },
  "timestamp": 0
}

```

< The payload for an analyze cart operation. This payload contains information about the merchant, the consumer, and the items being purchased.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|merchantCartID|string|true|none|The merchant-generated unique identifier for this cart|
|previousCartId|string|false|none|The previous (Pinch generated) cart ID, if this replaces a previously supplied cart|
|totalCartCost|[Monetary](#schemamonetary)|true|none|Describes a monetary value, including currency.|
|cart|[[CartEntry](#schemacartentry)]|true|none|Description of the cart|
|customer|[Customer](#schemacustomer)|true|none|Information about a customer|
|merchant|[Merchant](#schemamerchant)|true|none|< Information about a merchant. Note that the merchant will be identified based on the certificate used to access the Pinch APIs; this schema element is intended to provide additional information about the merchant|
|customData|object|false|none|none|
|» **additionalProperties**|object|false|none|none|
|timestamp|integer(int64)|false|none|The epoch time (in milliseconds) when request is happening. This optional field is useful for loading historical data|

<h2 id="tocS_CartEntry">CartEntry</h2>
<!-- backwards compatibility -->
<a id="schemacartentry"></a>
<a id="schema_CartEntry"></a>
<a id="tocScartentry"></a>
<a id="tocscartentry"></a>

```json
{
  "product": {
    "identifierType": "UPC",
    "identifier": "string",
    "category": "Fashion"
  },
  "count": 1,
  "perItemPrice": {
    "currencyCode": 840,
    "amount": 0.1
  }
}

```

< Describes one entry in a cart. This entry will have the product code, count (optionally, defaults to one), and perItemPrice for each item in the cart

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|product|[Product](#schemaproduct)|true|none|< Describes a product in the merchant catalog.|
|count|integer|false|none|none|
|perItemPrice|[Monetary](#schemamonetary)|true|none|Describes a monetary value, including currency.|

<h2 id="tocS_AnalyzeResultPayload">AnalyzeResultPayload</h2>
<!-- backwards compatibility -->
<a id="schemaanalyzeresultpayload"></a>
<a id="schema_AnalyzeResultPayload"></a>
<a id="tocSanalyzeresultpayload"></a>
<a id="tocsanalyzeresultpayload"></a>

```json
{
  "pinchCartID": "string",
  "merchantCartID": "string",
  "productPolicies": [
    {
      "product": {
        "identifierType": "UPC",
        "identifier": "string",
        "category": "Fashion"
      },
      "count": 0,
      "policies": [
        {
          "policyID": "string",
          "policyName": "string",
          "policyTerms": "string",
          "policyType": "Type1"
        }
      ]
    }
  ],
  "cartPolicies": [
    {
      "policyID": "string",
      "policyName": "string",
      "policyTerms": "string",
      "policyType": "Type1"
    }
  ]
}

```

< The result of successfully analyzing the shopping cart. This will return an array of policies, each of which optionally will have a set of items by identifier (UPC, EAN, JAN, SKU, etc.) associated with them. If the policy does not have any identifiers associated with it, that policy can be applied to any item in the cart. If, however, the policy does have one or more items associated with it, that policy can only be applied to the specified items.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|pinchCartID|string|false|none|The Pinch generated cart identifier for use with the sale endpoints|
|merchantCartID|string|false|none|The merchant supplied cart identifier (from the input)|
|productPolicies|[[ProductPolicy](#schemaproductpolicy)]|false|none|< Describes all the that can be offered for the items in the cart. The offers will be organized by item, with the list of policies offered for each item included|
|cartPolicies|[[Policy](#schemapolicy)]|false|none|[< Describes a policy that can be applied to an item in a cart. The policyID describes the policy and is unique for all policies that apply to the merchant. The name and description are human readable information about the policy, but the policyID is authoritative and should be used as the concrete definition of the policy.]|

<h2 id="tocS_ProductPolicy">ProductPolicy</h2>
<!-- backwards compatibility -->
<a id="schemaproductpolicy"></a>
<a id="schema_ProductPolicy"></a>
<a id="tocSproductpolicy"></a>
<a id="tocsproductpolicy"></a>

```json
{
  "product": {
    "identifierType": "UPC",
    "identifier": "string",
    "category": "Fashion"
  },
  "count": 0,
  "policies": [
    {
      "policyID": "string",
      "policyName": "string",
      "policyTerms": "string",
      "policyType": "Type1"
    }
  ]
}

```

< Defines the policies that can be applied to a product. The number of items of that product that can have the policy is included if there is a limit; if there is no limit then the count field will be omitted. Note that it is possible for a product to have multiple Offers, if there are limits on the number of items per Offer.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|product|[Product](#schemaproduct)|true|none|< Describes a product in the merchant catalog.|
|count|integer|false|none|none|
|policies|[[Policy](#schemapolicy)]|true|none|[< Describes a policy that can be applied to an item in a cart. The policyID describes the policy and is unique for all policies that apply to the merchant. The name and description are human readable information about the policy, but the policyID is authoritative and should be used as the concrete definition of the policy.]|

<h2 id="tocS_AddShippingLabel">AddShippingLabel</h2>
<!-- backwards compatibility -->
<a id="schemaaddshippinglabel"></a>
<a id="schema_AddShippingLabel"></a>
<a id="tocSaddshippinglabel"></a>
<a id="tocsaddshippinglabel"></a>

```json
{
  "product": {
    "identifierType": "UPC",
    "identifier": "string",
    "category": "Fashion"
  },
  "updateType": "AddShippingLabel",
  "shippingLabel": {
    "carrier": "string",
    "carrierCode": "USPS",
    "trackingNumber": "string",
    "state": "Created"
  }
}

```

Used to add a shipping label to the return

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|product|[Product](#schemaproduct)|false|none|< Describes a product in the merchant catalog.|
|updateType|string|true|none|none|
|shippingLabel|[ShippingLabel](#schemashippinglabel)|true|none|Information about the shipping label associated with the return|

<h2 id="tocS_CarrierCode">CarrierCode</h2>
<!-- backwards compatibility -->
<a id="schemacarriercode"></a>
<a id="schema_CarrierCode"></a>
<a id="tocScarriercode"></a>
<a id="tocscarriercode"></a>

```json
"USPS"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|USPS|
|*anonymous*|FedEx|
|*anonymous*|UPS|
|*anonymous*|Other|

<h2 id="tocS_ContactAddress">ContactAddress</h2>
<!-- backwards compatibility -->
<a id="schemacontactaddress"></a>
<a id="schema_ContactAddress"></a>
<a id="tocScontactaddress"></a>
<a id="tocscontactaddress"></a>

```json
{
  "contactType": "ContactAddress",
  "address": {
    "line1": "string",
    "line2": "string",
    "line3": "string",
    "line4": "string",
    "city": "string",
    "state": "string",
    "postalCode": "string",
    "country": "string",
    "geoCode": {
      "longitude": -180,
      "latitude": -90
    }
  },
  "addressType": "Billing"
}

```

< An address with associated address type. The address type denotes what type of address it is - a home address, billing address, etc. The contactType element is used to convey that the JSON payload contains contact address information and should always be the constant string "ContactAddress"

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|contactType|string|true|none|none|
|address|[Address](#schemaaddress)|true|none|< Describes an address. While the address structure is intended to be flexible, it is not possible to define an exact address structure for every possible postal standard. Instead, there is a recommended mapping for each country to these fields; see <TBD>|
|addressType|string|true|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|addressType|Billing|
|addressType|Mailing|
|addressType|Work|
|addressType|Home|

<h2 id="tocS_Customer">Customer</h2>
<!-- backwards compatibility -->
<a id="schemacustomer"></a>
<a id="schema_Customer"></a>
<a id="tocScustomer"></a>
<a id="tocscustomer"></a>

```json
{
  "name": "string",
  "deviceFingerprints": [
    {
      "algorithm": "string",
      "fingerPrint": "string"
    }
  ],
  "contactInformation": [
    {
      "contactType": "ContactAddress",
      "address": {
        "line1": "string",
        "line2": "string",
        "line3": "string",
        "line4": "string",
        "city": "string",
        "state": "string",
        "postalCode": "string",
        "country": "string",
        "geoCode": {
          "longitude": -180,
          "latitude": -90
        }
      },
      "addressType": "Billing"
    }
  ]
}

```

Information about a customer

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|The name of the customer|
|deviceFingerprints|[[DeviceFingerprint](#schemadevicefingerprint)]|false|none|[< A unique identifying device fingerprint for the user device. Each fingerprint needs to identify the algorithm used to create the fingerprint]|
|contactInformation|[[CustomerContact](#schemacustomercontact)]|false|none|Contact information for the customer|

<h2 id="tocS_CustomerContact">CustomerContact</h2>
<!-- backwards compatibility -->
<a id="schemacustomercontact"></a>
<a id="schema_CustomerContact"></a>
<a id="tocScustomercontact"></a>
<a id="tocscustomercontact"></a>

```json
{
  "contactType": "ContactAddress",
  "address": {
    "line1": "string",
    "line2": "string",
    "line3": "string",
    "line4": "string",
    "city": "string",
    "state": "string",
    "postalCode": "string",
    "country": "string",
    "geoCode": {
      "longitude": -180,
      "latitude": -90
    }
  },
  "addressType": "Billing"
}

```

A means for contacting a customer

### Properties

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ContactAddress](#schemacontactaddress)|false|none|< An address with associated address type. The address type denotes what type of address it is - a home address, billing address, etc. The contactType element is used to convey that the JSON payload contains contact address information and should always be the constant string "ContactAddress"|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[EMail](#schemaemail)|false|none|< An email address as described in §3.4.1 of RFC 5322. This schema is part of the CustomerContact schema and therefore must supply a contactType (in this case, the constant string "EMail"|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[IPAddress](#schemaipaddress)|false|none|< The IP address for a customer in either ipv4 or ipv6 format. This is a contactType and must supply the contactType property as the hard-code string "IPAddress"|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[Phone](#schemaphone)|false|none|< Phone number of customer|

<h2 id="tocS_DeviceFingerprint">DeviceFingerprint</h2>
<!-- backwards compatibility -->
<a id="schemadevicefingerprint"></a>
<a id="schema_DeviceFingerprint"></a>
<a id="tocSdevicefingerprint"></a>
<a id="tocsdevicefingerprint"></a>

```json
{
  "algorithm": "string",
  "fingerPrint": "string"
}

```

< A unique identifying device fingerprint for the user device. Each fingerprint needs to identify the algorithm used to create the fingerprint

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|algorithm|string|true|none|none|
|fingerPrint|string|true|none|none|

<h2 id="tocS_EMail">EMail</h2>
<!-- backwards compatibility -->
<a id="schemaemail"></a>
<a id="schema_EMail"></a>
<a id="tocSemail"></a>
<a id="tocsemail"></a>

```json
{
  "contactType": "EMail",
  "address": "string"
}

```

< An email address as described in §3.4.1 of RFC 5322. This schema is part of the CustomerContact schema and therefore must supply a contactType (in this case, the constant string "EMail"

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|contactType|string|true|none|none|
|address|string|true|none|none|

<h2 id="tocS_Phone">Phone</h2>
<!-- backwards compatibility -->
<a id="schemaphone"></a>
<a id="schema_Phone"></a>
<a id="tocSphone"></a>
<a id="tocsphone"></a>

```json
{
  "contactType": "Phone",
  "phone": "string"
}

```

< Phone number of customer

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|contactType|string|true|none|none|
|phone|string|true|none|none|

<h2 id="tocS_GeoCode">GeoCode</h2>
<!-- backwards compatibility -->
<a id="schemageocode"></a>
<a id="schema_GeoCode"></a>
<a id="tocSgeocode"></a>
<a id="tocsgeocode"></a>

```json
{
  "longitude": -180,
  "latitude": -90
}

```

Used to describe a location using latitude and longitude values

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|longitude|number(double)|true|none|none|
|latitude|number(double)|true|none|none|

<h2 id="tocS_History">History</h2>
<!-- backwards compatibility -->
<a id="schemahistory"></a>
<a id="schema_History"></a>
<a id="tocShistory"></a>
<a id="tocshistory"></a>

```json
{
  "timestamp": "string",
  "oldState": "string",
  "newState": "string",
  "comment": "string"
}

```

One history record for the return

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|timestamp|string|true|none|The timestamp formatted under ISO 8601-1:2019, e.g. 2007-04-05T14:30|
|oldState|string|false|none|The old state of the return|
|newState|string|true|none|The new state of the return|
|comment|string|true|none|none|

<h2 id="tocS_ReturnResponseItem">ReturnResponseItem</h2>
<!-- backwards compatibility -->
<a id="schemareturnresponseitem"></a>
<a id="schema_ReturnResponseItem"></a>
<a id="tocSreturnresponseitem"></a>
<a id="tocsreturnresponseitem"></a>

```json
{
  "product": {
    "identifierType": "UPC",
    "identifier": "string",
    "category": "Fashion"
  },
  "returnID": "string",
  "status": "ALLOW",
  "reason": "string"
}

```

Item that was requested to be returned

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|product|[Product](#schemaproduct)|true|none|< Describes a product in the merchant catalog.|
|returnID|string|false|none|The return identifier|
|status|string|true|none|none|
|reason|string|true|none|The reason why the item could not be returned|

#### Enumerated Values

|Property|Value|
|---|---|
|status|ALLOW|
|status|DENY|
|status|REVIEW|

<h2 id="tocS_IneligibleReasonCode">IneligibleReasonCode</h2>
<!-- backwards compatibility -->
<a id="schemaineligiblereasoncode"></a>
<a id="schema_IneligibleReasonCode"></a>
<a id="tocSineligiblereasoncode"></a>
<a id="tocsineligiblereasoncode"></a>

```json
"NotInCart"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|NotInCart|
|*anonymous*|AlreadyReturned|
|*anonymous*|NoSuitablePolicy|
|*anonymous*|InvalidItemCount|

<h2 id="tocS_ReturnUpdateType">ReturnUpdateType</h2>
<!-- backwards compatibility -->
<a id="schemareturnupdatetype"></a>
<a id="schema_ReturnUpdateType"></a>
<a id="tocSreturnupdatetype"></a>
<a id="tocsreturnupdatetype"></a>

```json
"AddShippingLabel"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|AddShippingLabel|
|*anonymous*|UpdateShippingLabelState|
|*anonymous*|ReturnUpdateStatus|

<h2 id="tocS_IPAddress">IPAddress</h2>
<!-- backwards compatibility -->
<a id="schemaipaddress"></a>
<a id="schema_IPAddress"></a>
<a id="tocSipaddress"></a>
<a id="tocsipaddress"></a>

```json
{
  "contactType": "IPAddress",
  "address": "string"
}

```

< The IP address for a customer in either ipv4 or ipv6 format. This is a contactType and must supply the contactType property as the hard-code string "IPAddress"

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|contactType|string|true|none|none|
|address|string|true|none|none|

<h2 id="tocS_ProductIdentifierType">ProductIdentifierType</h2>
<!-- backwards compatibility -->
<a id="schemaproductidentifiertype"></a>
<a id="schema_ProductIdentifierType"></a>
<a id="tocSproductidentifiertype"></a>
<a id="tocsproductidentifiertype"></a>

```json
"UPC"

```

The enum of know item identifier types

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|The enum of know item identifier types|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|UPC|
|*anonymous*|EAN|
|*anonymous*|JAN|
|*anonymous*|SKU|
|*anonymous*|Category|
|*anonymous*|Subcategory|

<h2 id="tocS_Product">Product</h2>
<!-- backwards compatibility -->
<a id="schemaproduct"></a>
<a id="schema_Product"></a>
<a id="tocSproduct"></a>
<a id="tocsproduct"></a>

```json
{
  "identifierType": "UPC",
  "identifier": "string",
  "category": "Fashion"
}

```

< Describes a product in the merchant catalog.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|identifierType|[ProductIdentifierType](#schemaproductidentifiertype)|true|none|The enum of know item identifier types|
|identifier|string|true|none|The unique identifier|
|category|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|category|Fashion|
|category|Shoes|
|category|Electronics|
|category|Toys_Hobbies|
|category|Cosmetics_body_care|
|category|Food_beverage|
|category|Furniture_decor|
|category|Health_wellness|
|category|Home_Goods|
|category|Pet_care|
|category|Office_equipment|

<h2 id="tocS_Merchant">Merchant</h2>
<!-- backwards compatibility -->
<a id="schemamerchant"></a>
<a id="schema_Merchant"></a>
<a id="tocSmerchant"></a>
<a id="tocsmerchant"></a>

```json
{
  "locationID": "string"
}

```

< Information about a merchant. Note that the merchant will be identified based on the certificate used to access the Pinch APIs; this schema element is intended to provide additional information about the merchant

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|locationID|string|true|none|The merchant-defined location identifier|

<h2 id="tocS_PaymentInfo">PaymentInfo</h2>
<!-- backwards compatibility -->
<a id="schemapaymentinfo"></a>
<a id="schema_PaymentInfo"></a>
<a id="tocSpaymentinfo"></a>
<a id="tocspaymentinfo"></a>

```json
{
  "amount": {
    "currencyCode": 840,
    "amount": 0.1
  },
  "instrument": null,
  "last4": "string",
  "BIN": "string",
  "postalCode": "string",
  "method": "NotPresent",
  "auth": "string",
  "AID": "string"
}

```

Describes a payment associated with a purchase

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|amount|[Monetary](#schemamonetary)|true|none|Describes a monetary value, including currency.|
|instrument|[./instrument-type.yaml#/Instrument](#schema./instrument-type.yaml#/instrument)|true|none|none|
|last4|string|false|none|For credit and debit cards, the last four digits of the PAN|
|BIN|string|false|none|For credit and debit cards, the BIN / IIN|
|postalCode|string|false|none|For credit and debit cards, the postal code provided|
|method|string|false|none|For credit and debit cards, the way the card was presented|
|auth|string|false|none|For credit and debit cards, the authorization code returned|
|AID|string|false|none|For credit and debit cards where method = Tap or Dip, the AID used|

#### Enumerated Values

|Property|Value|
|---|---|
|method|NotPresent|
|method|Swipe|
|method|Tap|
|method|Dip|

<h2 id="tocS_Policy">Policy</h2>
<!-- backwards compatibility -->
<a id="schemapolicy"></a>
<a id="schema_Policy"></a>
<a id="tocSpolicy"></a>
<a id="tocspolicy"></a>

```json
{
  "policyID": "string",
  "policyName": "string",
  "policyTerms": "string",
  "policyType": "Type1"
}

```

< Describes a policy that can be applied to an item in a cart. The policyID describes the policy and is unique for all policies that apply to the merchant. The name and description are human readable information about the policy, but the policyID is authoritative and should be used as the concrete definition of the policy.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|policyID|string|true|none|The unique identifier for the policy within the defined policies for this merchant|
|policyName|string|true|none|The human-readable name for the policy|
|policyTerms|string|true|none|The human-readable terms and conditions|
|policyType|string|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|policyType|Type1|
|policyType|Type2|
|policyType|Type3|

<h2 id="tocS_ReturnedItem">ReturnedItem</h2>
<!-- backwards compatibility -->
<a id="schemareturneditem"></a>
<a id="schema_ReturnedItem"></a>
<a id="tocSreturneditem"></a>
<a id="tocsreturneditem"></a>

```json
{
  "product": {
    "identifierType": "UPC",
    "identifier": "string",
    "category": "Fashion"
  },
  "count": 1,
  "policyID": "string",
  "reason": "string"
}

```

< A group of identical returned items (same ItemIdentifier), optionally with the requested return policy and reason. The reason provided at this level will override any reason given at the top level

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|product|[Product](#schemaproduct)|true|none|< Describes a product in the merchant catalog.|
|count|integer|true|none|The number of returned items of this type|
|policyID|string|true|none|The policy ID that should be used for this return|
|reason|string|false|none|The customer specified reason for the return|

<h2 id="tocS_ReturnRequestPayload">ReturnRequestPayload</h2>
<!-- backwards compatibility -->
<a id="schemareturnrequestpayload"></a>
<a id="schema_ReturnRequestPayload"></a>
<a id="tocSreturnrequestpayload"></a>
<a id="tocsreturnrequestpayload"></a>

```json
{
  "orderID": "string",
  "merchantOrderID": "string",
  "returnedItems": [
    {
      "product": {
        "identifierType": "UPC",
        "identifier": "string",
        "category": "Fashion"
      },
      "count": 1,
      "policyID": "string",
      "reason": "string"
    }
  ],
  "customer": {
    "name": "string",
    "deviceFingerprints": [
      {
        "algorithm": "string",
        "fingerPrint": "string"
      }
    ],
    "contactInformation": [
      {
        "contactType": "ContactAddress",
        "address": {
          "line1": "string",
          "line2": "string",
          "line3": "string",
          "line4": "string",
          "city": "string",
          "state": "string",
          "postalCode": "string",
          "country": "string",
          "geoCode": {
            "longitude": -180,
            "latitude": -90
          }
        },
        "addressType": "Billing"
      }
    ]
  },
  "reason": "string",
  "timestamp": 0
}

```

< Provides information to initiate a return. The return requires an order ID; furthermore the items in that order that are being returned have to be marked as delivered.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|orderID|string|false|none|The unique order number returned by the cart purchase API|
|merchantOrderID|string|false|none|The merchant-supplied order ID|
|returnedItems|[[ReturnedItem](#schemareturneditem)]|true|none|[< A group of identical returned items (same ItemIdentifier), optionally with the requested return policy and reason. The reason provided at this level will override any reason given at the top level]|
|customer|[Customer](#schemacustomer)|true|none|Information about a customer|
|reason|string|true|none|The customer specified reason for the return|
|timestamp|integer(int64)|false|none|The epoch time (in milliseconds) when request is happening. This optional field is useful for loading historical data|

<h2 id="tocS_ReturnResponsePayload">ReturnResponsePayload</h2>
<!-- backwards compatibility -->
<a id="schemareturnresponsepayload"></a>
<a id="schema_ReturnResponsePayload"></a>
<a id="tocSreturnresponsepayload"></a>
<a id="tocsreturnresponsepayload"></a>

```json
{
  "items": [
    {
      "product": {
        "identifierType": "UPC",
        "identifier": "string",
        "category": "Fashion"
      },
      "returnID": "string",
      "status": "ALLOW",
      "reason": "string"
    }
  ]
}

```

< Denotes the result of attempting to open a new return. This will be an array of newly generated return IDs and the items associated with this returns along with their review status

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|items|[[ReturnResponseItem](#schemareturnresponseitem)]|false|none|[Item that was requested to be returned]|

<h2 id="tocS_ReturnState">ReturnState</h2>
<!-- backwards compatibility -->
<a id="schemareturnstate"></a>
<a id="schema_ReturnState"></a>
<a id="tocSreturnstate"></a>
<a id="tocsreturnstate"></a>

```json
"Opened"

```

The state of the return

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|The state of the return|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Opened|
|*anonymous*|Denied|
|*anonymous*|InProcess|
|*anonymous*|Exception|
|*anonymous*|Cancelled|
|*anonymous*|Closed|

<h2 id="tocS_ReturnStatusResultPayload">ReturnStatusResultPayload</h2>
<!-- backwards compatibility -->
<a id="schemareturnstatusresultpayload"></a>
<a id="schema_ReturnStatusResultPayload"></a>
<a id="tocSreturnstatusresultpayload"></a>
<a id="tocsreturnstatusresultpayload"></a>

```json
{
  "state": "Opened",
  "shippingLabel": {
    "carrier": "string",
    "carrierCode": "USPS",
    "trackingNumber": "string",
    "state": "Created"
  },
  "historyMap": {
    "property1": [
      {
        "timestamp": "string",
        "oldState": "string",
        "newState": "string",
        "comment": "string"
      }
    ],
    "property2": [
      {
        "timestamp": "string",
        "oldState": "string",
        "newState": "string",
        "comment": "string"
      }
    ]
  },
  "coveredItems": [
    {
      "identifierType": "UPC",
      "identifier": "string",
      "category": "Fashion"
    }
  ]
}

```

The state of the return

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|state|[ReturnState](#schemareturnstate)|true|none|The state of the return|
|shippingLabel|[ShippingLabel](#schemashippinglabel)|false|none|Information about the shipping label associated with the return|
|historyMap|object|false|none|none|
|» **additionalProperties**|[[History](#schemahistory)]|false|none|[One history record for the return]|
|coveredItems|[[Product](#schemaproduct)]|true|none|[< Describes a product in the merchant catalog.]|

<h2 id="tocS_ReturnUpdateRequestPayload">ReturnUpdateRequestPayload</h2>
<!-- backwards compatibility -->
<a id="schemareturnupdaterequestpayload"></a>
<a id="schema_ReturnUpdateRequestPayload"></a>
<a id="tocSreturnupdaterequestpayload"></a>
<a id="tocsreturnupdaterequestpayload"></a>

```json
{
  "updateType": "string",
  "newStatus": "Opened",
  "comment": "string",
  "timestamp": 0
}

```

Used to update the state of the return, or one or more fields of the return

### Properties

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[ReturnUpdateStatus](#schemareturnupdatestatus)|false|none|Used to update the status of the return|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[AddShippingLabel](#schemaaddshippinglabel)|false|none|Used to add a shipping label to the return|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[UpdateShippingLabelState](#schemaupdateshippinglabelstate)|false|none|Used to update a shipping label to the return|

<h2 id="tocS_ReturnUpdateStatus">ReturnUpdateStatus</h2>
<!-- backwards compatibility -->
<a id="schemareturnupdatestatus"></a>
<a id="schema_ReturnUpdateStatus"></a>
<a id="tocSreturnupdatestatus"></a>
<a id="tocsreturnupdatestatus"></a>

```json
{
  "updateType": "string",
  "newStatus": "Opened",
  "comment": "string",
  "timestamp": 0
}

```

Used to update the status of the return

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|updateType|string|true|none|UpdateStatus|
|newStatus|[ReturnState](#schemareturnstate)|true|none|The state of the return|
|comment|string|false|none|none|
|timestamp|integer(int64)|false|none|The epoch time (in milliseconds) when request is happening. This optional field is useful for loading historical data|

<h2 id="tocS_ShippingLabel">ShippingLabel</h2>
<!-- backwards compatibility -->
<a id="schemashippinglabel"></a>
<a id="schema_ShippingLabel"></a>
<a id="tocSshippinglabel"></a>
<a id="tocsshippinglabel"></a>

```json
{
  "carrier": "string",
  "carrierCode": "USPS",
  "trackingNumber": "string",
  "state": "Created"
}

```

Information about the shipping label associated with the return

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|carrier|string|false|none|The shipping carrier|
|carrierCode|[CarrierCode](#schemacarriercode)|true|none|none|
|trackingNumber|string|false|none|The tracking number|
|state|[ShippingLabelState](#schemashippinglabelstate)|false|none|The state of the shipping label|

<h2 id="tocS_ShippingLabelState">ShippingLabelState</h2>
<!-- backwards compatibility -->
<a id="schemashippinglabelstate"></a>
<a id="schema_ShippingLabelState"></a>
<a id="tocSshippinglabelstate"></a>
<a id="tocsshippinglabelstate"></a>

```json
"Created"

```

The state of the shipping label

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|The state of the shipping label|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|Created|
|*anonymous*|Shipped|
|*anonymous*|Received|
|*anonymous*|Lost|

<h2 id="tocS_UpdateShippingLabelState">UpdateShippingLabelState</h2>
<!-- backwards compatibility -->
<a id="schemaupdateshippinglabelstate"></a>
<a id="schema_UpdateShippingLabelState"></a>
<a id="tocSupdateshippinglabelstate"></a>
<a id="tocsupdateshippinglabelstate"></a>

```json
{
  "comment": "string",
  "product": {
    "identifierType": "UPC",
    "identifier": "string",
    "category": "Fashion"
  },
  "updateType": "UpdateShippingLabel",
  "shippingLabel": {
    "carrier": "string",
    "carrierCode": "USPS",
    "trackingNumber": "string",
    "state": "Created"
  }
}

```

Used to update a shipping label to the return

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|comment|string|false|none|none|
|product|[Product](#schemaproduct)|false|none|< Describes a product in the merchant catalog.|
|updateType|string|true|none|none|
|shippingLabel|[ShippingLabel](#schemashippinglabel)|true|none|Information about the shipping label associated with the return|

<h2 id="tocS_PurchaseRequestPayload">PurchaseRequestPayload</h2>
<!-- backwards compatibility -->
<a id="schemapurchaserequestpayload"></a>
<a id="schema_PurchaseRequestPayload"></a>
<a id="tocSpurchaserequestpayload"></a>
<a id="tocspurchaserequestpayload"></a>

```json
{
  "cartID": "string",
  "merchantCartID": "string",
  "merchantOrderID": "string",
  "orderStatus": "Pending",
  "paymentInfo": [
    {
      "amount": {
        "currencyCode": 840,
        "amount": 0.1
      },
      "instrument": null,
      "last4": "string",
      "BIN": "string",
      "postalCode": "string",
      "method": "NotPresent",
      "auth": "string",
      "AID": "string"
    }
  ],
  "purchasedPolicies": [
    "string"
  ],
  "timestamp": 0
}

```

< Provided to denote that a consumer has purchased a previously analyzed cart, along with the policies that the user chose to purchase. The policies being selected are denoted by their policyRef, which is unique for the policy applied to the item. The merchant can optionally provide a merchant order ID and order status. If the order status is not provided, the order will be considered Pending until the status is changed with an order status update call (/v1/order/updateStatus)

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|cartID|string|true|none|The cart ID provided by the analysis call|
|merchantCartID|string|false|none|The cart ID provided by the merchant|
|merchantOrderID|string|false|none|The merchant-supplied order ID|
|orderStatus|string|false|none|none|
|paymentInfo|[[PaymentInfo](#schemapaymentinfo)]|true|none|[Describes a payment associated with a purchase]|
|purchasedPolicies|[string]|true|none|none|
|timestamp|integer(int64)|false|none|The epoch time (in milliseconds) when request is happening. This optional field is useful for loading historical data|

#### Enumerated Values

|Property|Value|
|---|---|
|orderStatus|Pending|
|orderStatus|InProgress|
|orderStatus|Shipped|
|orderStatus|Delivered|

<h2 id="tocS_PurchaseResultPayload">PurchaseResultPayload</h2>
<!-- backwards compatibility -->
<a id="schemapurchaseresultpayload"></a>
<a id="schema_PurchaseResultPayload"></a>
<a id="tocSpurchaseresultpayload"></a>
<a id="tocspurchaseresultpayload"></a>

```json
{
  "orderID": "string"
}

```

< Once a cart has been purchased, the purchase request will return an order number. This order number will then be used for subsequent tracking of the state of the order - when it is confirmed, in progress, shipped, delivered, etc. See the /v1/order family of transactions.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|orderID|string|true|none|The Pinch generated order ID used to track the purchase|

<h2 id="tocS_Monetary">Monetary</h2>
<!-- backwards compatibility -->
<a id="schemamonetary"></a>
<a id="schema_Monetary"></a>
<a id="tocSmonetary"></a>
<a id="tocsmonetary"></a>

```json
{
  "currencyCode": 840,
  "amount": 0.1
}

```

Describes a monetary value, including currency.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|currencyCode|string|false|none|The ISO-4217 three-digit currency currency|
|amount|number(float)|true|none|The amount|

<h2 id="tocS_Address">Address</h2>
<!-- backwards compatibility -->
<a id="schemaaddress"></a>
<a id="schema_Address"></a>
<a id="tocSaddress"></a>
<a id="tocsaddress"></a>

```json
{
  "line1": "string",
  "line2": "string",
  "line3": "string",
  "line4": "string",
  "city": "string",
  "state": "string",
  "postalCode": "string",
  "country": "string",
  "geoCode": {
    "longitude": -180,
    "latitude": -90
  }
}

```

< Describes an address. While the address structure is intended to be flexible, it is not possible to define an exact address structure for every possible postal standard. Instead, there is a recommended mapping for each country to these fields; see <TBD>

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|line1|string|true|none|Address line 1|
|line2|string|false|none|Address line 2|
|line3|string|false|none|Address line 3|
|line4|string|false|none|Address line 4|
|city|string|true|none|The city name|
|state|string|false|none|The state name|
|postalCode|string|true|none|The postal code|
|country|string|false|none|The country|
|geoCode|[GeoCode](#schemageocode)|false|none|Used to describe a location using latitude and longitude values|

<h2 id="tocS_DispositionRequestPayload">DispositionRequestPayload</h2>
<!-- backwards compatibility -->
<a id="schemadispositionrequestpayload"></a>
<a id="schema_DispositionRequestPayload"></a>
<a id="tocSdispositionrequestpayload"></a>
<a id="tocsdispositionrequestpayload"></a>

```json
{
  "itemID": "string",
  "inspectionNotes": "string",
  "returnedItemCondition": "NEW",
  "dispositionOutcome": "RESTOCK",
  "returnMode": "IN_STORE",
  "refundMethod": "ORIGINAL_TENDER",
  "warehouseId": "string",
  "storeId": "string",
  "images": [
    "string"
  ],
  "abuseType": "STOLEN_MERCHANDISE",
  "timestamp": 0
}

```

< Denotes the payload to update the disposition of a returned item.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|itemID|string|true|none|The item ID being returned|
|inspectionNotes|string|false|none|Notes from the inspection of the returned item provided by receiver at the time of return|
|returnedItemCondition|[ReturnedItemCondition](#schemareturneditemcondition)|true|none|The condition of the returned item when received|
|dispositionOutcome|[DispositionOutcome](#schemadispositionoutcome)|true|none|Denotes the outcome of the disposition whether to restock, donate etc.|
|returnMode|string|false|none|The mode of return|
|refundMethod|string|false|none|The refund method chosen|
|warehouseId|string|false|none|The ID of warehouse|
|storeId|string|false|none|The ID of the store that returned the unit to the warehouse. Available only in case of in-store returns.|
|images|[string]|false|none|The images of the returned item|
|abuseType|[AbuseType](#schemaabusetype)|false|none|The abuse type of returned item identified by the warehouse worker as part of disposition when item was received|
|timestamp|integer(int64)|false|none|The epoch time (in milliseconds) when request is happening. This optional field is useful for loading historical data|

#### Enumerated Values

|Property|Value|
|---|---|
|returnMode|IN_STORE|
|returnMode|ONLINE|
|refundMethod|ORIGINAL_TENDER|
|refundMethod|STORE_CREDIT|

<h2 id="tocS_ReturnedItemCondition">ReturnedItemCondition</h2>
<!-- backwards compatibility -->
<a id="schemareturneditemcondition"></a>
<a id="schema_ReturnedItemCondition"></a>
<a id="tocSreturneditemcondition"></a>
<a id="tocsreturneditemcondition"></a>

```json
"NEW"

```

The condition of the returned item when received

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|The condition of the returned item when received|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|NEW|
|*anonymous*|OPEN_BOX|
|*anonymous*|LIGHTLY_USED|
|*anonymous*|EMPTY_BOX|
|*anonymous*|COUNTERFEIT_ITEM|
|*anonymous*|DAMAGED_ITEM|
|*anonymous*|LOST_ITEM|

<h2 id="tocS_AbuseType">AbuseType</h2>
<!-- backwards compatibility -->
<a id="schemaabusetype"></a>
<a id="schema_AbuseType"></a>
<a id="tocSabusetype"></a>
<a id="tocsabusetype"></a>

```json
"STOLEN_MERCHANDISE"

```

The abuse type of returned item identified by the warehouse worker as part of disposition when item was received

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|The abuse type of returned item identified by the warehouse worker as part of disposition when item was received|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|STOLEN_MERCHANDISE|
|*anonymous*|STOLEN_PAYMENT_INSTRUMENT|
|*anonymous*|RECEIPT_FRAUD|
|*anonymous*|EMPLOYEE_FRAUD|
|*anonymous*|PRICE_SWITCHING|
|*anonymous*|PRICE_ARBITRAGE|
|*anonymous*|SWITCH_FRAUD|
|*anonymous*|BRICKING|
|*anonymous*|CROSS_RETAIL|
|*anonymous*|OPEN_BOX_FRAUD|
|*anonymous*|EMPTY_BOX_FRAUD|
|*anonymous*|DELIBERATE_FRAUD|
|*anonymous*|WARDROBING|
|*anonymous*|SELLER_SABOTAGE|
|*anonymous*|FREE_SHIPPING_ABUSE|
|*anonymous*|OTHERS|
|*anonymous*|NONE|

<h2 id="tocS_DispositionOutcome">DispositionOutcome</h2>
<!-- backwards compatibility -->
<a id="schemadispositionoutcome"></a>
<a id="schema_DispositionOutcome"></a>
<a id="tocSdispositionoutcome"></a>
<a id="tocsdispositionoutcome"></a>

```json
"RESTOCK"

```

Denotes the outcome of the disposition whether to restock, donate etc.

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string|false|none|Denotes the outcome of the disposition whether to restock, donate etc.|

#### Enumerated Values

|Property|Value|
|---|---|
|*anonymous*|RESTOCK|
|*anonymous*|RECYCLE|
|*anonymous*|REFURBISH|
|*anonymous*|DONATE|
|*anonymous*|LIQUIDATE|
|*anonymous*|REMOVE_OTHERS|
|*anonymous*|REMOVE_SUSPECT_ABUSE|


