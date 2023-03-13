

**API Specification Doc**

**(_Chilly Recipes App_)**


<table>
  <tr>
   <td><strong>Version</strong>
   </td>
   <td><strong>Date</strong>
   </td>
   <td><strong>Author</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>1.0
   </td>
   <td>05-Oct-2012
   </td>
   <td>Saurabh (rebugged.com)
   </td>
   <td>Initial draft
   </td>
  </tr>
  <tr>
   <td>1.1
   </td>
   <td>17-Nov-2012
   </td>
   <td>Saurabh (rebugged.com)
   </td>
   <td>Added version number in response
   </td>
  </tr>
</table>



## <span style="text-decoration:underline;">NOTE:</span> Please don’t request edit access to this demo document. Instead, click the “USE TEMPLATE” button if it is present on the right top corner of the page, or click [here](https://docs.google.com/document/d/1HSQ3Fe77hnthw8hizqvXJU-qGEPHavMkctvCCadkVbY/template/preview?usp=drive_web) to make a copy of this template for your use. Thank you!


## 


## <p style="text-align: right">
Index</p>



[TOC]



## 


## <p style="text-align: right">
Methods</p>



## 1. login {#1-login}

Authenticate the user with the system and obtain the auth_token


## Request {#request}


<table>
  <tr>
   <td><strong>Method</strong>
   </td>
   <td><strong>URL            </strong>
   </td>
  </tr>
  <tr>
   <td><strong><code>POST</code></strong>
   </td>
   <td><code>api/login/</code>
   </td>
  </tr>
</table>



<table>
  <tr>
   <td><strong>Type</strong>
   </td>
   <td><strong>Params</strong>
   </td>
   <td><strong>Values</strong>
   </td>
  </tr>
  <tr>
   <td><code>HEAD</code>
<p>
<code>POST</code>
<p>
<code>POST</code>
   </td>
   <td><code>api_key</code>
<p>
<code>username</code>
<p>
<code>password</code>
   </td>
   <td><code>string</code>
<p>
<code>string</code>
<p>
<code>string</code>
   </td>
  </tr>
</table>



```
api_key
```


 `api_key`  must be sent with all client requests. The api_key helps the server to validate the request source.


## Response {#response}


<table>
  <tr>
   <td><strong>Status</strong>
   </td>
   <td><strong>Response</strong>
   </td>
  </tr>
  <tr>
   <td><code>200</code>
   </td>
   <td><code>{</code>
<p>
<code>    "auth_key": &lt;auth_key></code>
<p>
<code>}</code>
<p>
<code>auth_key (<strong>string</strong>)</code> - all further API calls must have this key in header
   </td>
  </tr>
  <tr>
   <td><code>403</code>
   </td>
   <td><code>{"error":"API key is missing."}</code>
   </td>
  </tr>
  <tr>
   <td><code>400</code>
   </td>
   <td><code>{"error":"Please provide username."}</code>
   </td>
  </tr>
  <tr>
   <td><code>400</code>
   </td>
   <td><code>{"error":"Please provide password."}</code>
   </td>
  </tr>
  <tr>
   <td><code>401</code>
   </td>
   <td><code>{"error":"Invalid API key."}</code>
   </td>
  </tr>
  <tr>
   <td><code>401</code>
   </td>
   <td><code>{"error":"Incorrect username or password."}</code>
   </td>
  </tr>
  <tr>
   <td><code>500</code>
   </td>
   <td><code>{"error":"Something went wrong. Please try again later."}</code>
   </td>
  </tr>
</table>



## 2. get itineraries

Get the new updates


## Request {#request}


<table>
  <tr>
   <td><strong>Method</strong>
   </td>
   <td><strong>URL            </strong>
   </td>
  </tr>
  <tr>
   <td><strong><code>GET</code></strong>
   </td>
   <td><code>itineraries</code>
   </td>
  </tr>
</table>



<table>
  <tr>
   <td><strong>Type</strong>
   </td>
   <td><strong>Params</strong>
   </td>
   <td><strong>Values</strong>
   </td>
  </tr>
  <tr>
   <td><code>HEAD</code>
<p>
<code>POST</code>
   </td>
   <td><code>auth_key</code>
<p>
<code>version</code>
   </td>
   <td><code>string</code>
<p>
<code>number</code>
   </td>
  </tr>
</table>



```
auth_key
```


The ` auth_key ` that was given in response to `/api/login`


```
version
```


The current version of internal recipe database. Each time when updates are pulled from the server through the web service, the internal database version is incremented.


## Response {#response}


<table>
  <tr>
   <td><strong>Status</strong>
   </td>
   <td><strong>Response</strong>
   </td>
  </tr>
  <tr>
   <td><code>200</code>
   </td>
   <td><strong>Response will be an object containing the list of recipes (array) </strong>
<p>
<strong>as well as the updated recipe database. Each item in the recipe array has the following structure.</strong>
<p>
<code>{</code>
<p>
<code>    "recipe_id": 10,</code>
<p>
<code>    "title": "Green Chilly Salad",</code>
<p>
<code>    "category": 1,</code>
<p>
<code>    "ingredients": {</code>
<p>
<code>        "Green Chilly": "1 kg",</code>
<p>
<code>        "Salt": "0.5 tbsp"</code>
<p>
<code>    },</code>
<p>
<code>    "steps": [</code>
<p>
<code>        "First clean and cut the chillies",</code>
<p>
<code>        "Now you can eat."</code>
<p>
<code>    ],</code>
<p>
<code>    "remarks": "serves 2 people"</code>
<p>
<code>}</code>
<p>
<strong>An example response is:-</strong>
<p>
<code>{</code>
<p>
<code>    "recipes": [</code>
<p>
<code>        {</code>
<p>
<code>            "recipe_id": 10,</code>
<p>
<code>            "title": "Green Leaf Curry",</code>
<p>
<code>            "category": 1,</code>
<p>
<code>            "ingredients": {</code>
<p>
<code>                "Green leaf": "1 kg",</code>
<p>
<code>                "Salt": "0.5 tbsp"</code>
<p>
<code>            },</code>
<p>
<code>            "steps": [</code>
<p>
<code>                "First clean and cut the leaves",</code>
<p>
<code>                "Now you can eat."</code>
<p>
<code>            ],</code>
<p>
<code>            "remarks": "serves 2 people"</code>
<p>
<code>        }</code>
<p>
<code>    ],</code>
<p>
<code>    "version": "4"</code>
<p>
<code>}</code>
   </td>
  </tr>
  <tr>
   <td><code>400</code>
   </td>
   <td><code>{"error":"Please specify database version."}</code>
   </td>
  </tr>
  <tr>
   <td><code>400</code>
   </td>
   <td><code>{"error":"Invalid database version."}</code>
   </td>
  </tr>
  <tr>
   <td><code>401</code>
   </td>
   <td><code>{"error":"Invalid API key."}</code>
   </td>
  </tr>
  <tr>
   <td><code>500</code>
   </td>
   <td><code>{"error":"Something went wrong. Please try again later."}</code>
   </td>
  </tr>
</table>



## 3. deletions {#3-deletions}

Get the recipes that were deleted from the web interface, so that they can be deleted from the internal database also.


## Request {#request}


<table>
  <tr>
   <td><strong>Method</strong>
   </td>
   <td><strong>URL            </strong>
   </td>
  </tr>
  <tr>
   <td><strong><code>POST</code></strong>
   </td>
   <td><code>api/deletions/</code>
   </td>
  </tr>
</table>



<table>
  <tr>
   <td><strong>Type</strong>
   </td>
   <td><strong>Params</strong>
   </td>
   <td><strong>Values</strong>
   </td>
  </tr>
  <tr>
   <td><code>HEAD</code>
<p>
<code>POST</code>
   </td>
   <td><code>auth_key</code>
<p>
<code>version</code>
   </td>
   <td><code>string</code>
<p>
<code>number</code>
   </td>
  </tr>
</table>



```
version
```


The current version of internal database. Each time when updates are pulled from the API, the internal database version increases.


## Response {#response}


<table>
  <tr>
   <td><strong>Status</strong>
   </td>
   <td><strong>Response</strong>
   </td>
  </tr>
  <tr>
   <td><code>200</code>
   </td>
   <td><strong>An array containing the ID’s of recipes to delete is given</strong>
<p>
<code>Example response:-</code>
<p>
<code>{"deletions":[10,11,40], "version":"5"}</code>
   </td>
  </tr>
  <tr>
   <td><code>400</code>
   </td>
   <td><code>{"error":"Please specify database version."}</code>
   </td>
  </tr>
  <tr>
   <td><code>400</code>
   </td>
   <td><code>{"error":"Invalid database version."}</code>
   </td>
  </tr>
  <tr>
   <td><code>401</code>
   </td>
   <td><code>{"error":"Invalid Auth key."}</code>
   </td>
  </tr>
  <tr>
   <td><code>500</code>
   </td>
   <td><code>{"error":"Something went wrong. Please try again later."}</code>
   </td>
  </tr>
</table>



## 4. get recipe image {#4-get-recipe-image}

Get more information on a particular recipe


## Request {#request}


<table>
  <tr>
   <td><strong>Method</strong>
   </td>
   <td><strong>URL            </strong>
   </td>
  </tr>
  <tr>
   <td><strong><code>GET</code></strong>
   </td>
   <td><code>api/image/&lt;recipe_id>/</code>
   </td>
  </tr>
</table>



<table>
  <tr>
   <td><strong>Type</strong>
   </td>
   <td><strong>Params</strong>
   </td>
   <td><strong>Values</strong>
   </td>
  </tr>
  <tr>
   <td><code>HEAD</code>
<p>
<code>URL_PARAM</code>
   </td>
   <td><code>auth_key</code>
<p>
<code>&lt;recipe_id></code>
   </td>
   <td><code>string</code>
<p>
<code>number</code>
   </td>
  </tr>
</table>



```
recipe_id
```


Id of the recipe you want the image of.


## Response {#response}


<table>
  <tr>
   <td><strong>Status</strong>
   </td>
   <td><strong>Response</strong>
   </td>
  </tr>
  <tr>
   <td><code>200</code>
   </td>
   <td><strong>An array containing the ID’s of recipes to delete is given</strong>
<p>
<code>Example response:-</code>
<p>
<code>{"image":"http:\/\/example.com\/recipe-5-image.jpg"}</code>
   </td>
  </tr>
  <tr>
   <td><code>400</code>
   </td>
   <td><code>{"error":"Please provide recipe_id."}</code>
   </td>
  </tr>
  <tr>
   <td><code>400</code>
   </td>
   <td><code>{"error":"Invalid recipe_id."}</code>
   </td>
  </tr>
  <tr>
   <td><code>401</code>
   </td>
   <td><code>{"error":"Invalid Auth key."}</code>
   </td>
  </tr>
  <tr>
   <td><code>500</code>
   </td>
   <td><code>{"error":"Something went wrong. Please try again later."}</code>
   </td>
  </tr>
</table>



## <p style="text-align: right">
</p>



## <p style="text-align: right">
Glossary</p>



## Conventions {#conventions}



* **Client** - Client application.
* **Status** - HTTP status code of response.
* All the possible responses are listed under ‘Responses’ for each method. Only one of them is issued per request server.
* All response are in JSON format.
* All request parameters are mandatory unless explicitly marked as `[optional]`
* The type of values accepted for a _request_ parameter are shown the the values column like this <code>[<strong>10</strong>|&lt;any number>]</code> .The <code>|</code> symbol means <em>OR</em>. If the parameter is <code>[optional]</code>, the default value is shown in blue bold text, as <strong><code>10</code></strong> is written in <code>[<strong>10</strong>|&lt;any number>]</code>.


## Status Codes {#status-codes}

All status codes are standard HTTP status codes. The below ones are used in this API.

`2XX - `Success of some kind

`4XX - `Error occurred in client’s part

`5XX - `Error occurred in server’s part


<table>
  <tr>
   <td><strong>Status Code</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td><code>200</code>
   </td>
   <td><code>OK</code>
   </td>
  </tr>
  <tr>
   <td><code>201</code>
   </td>
   <td><code>Created</code>
   </td>
  </tr>
  <tr>
   <td><code>202</code>
   </td>
   <td><code>Accepted (Request accepted, and queued for execution)</code>
   </td>
  </tr>
  <tr>
   <td><code>400</code>
   </td>
   <td><code>Bad request</code>
   </td>
  </tr>
  <tr>
   <td><code>401</code>
   </td>
   <td><code>Authentication failure</code>
   </td>
  </tr>
  <tr>
   <td><code>403</code>
   </td>
   <td><code>Forbidden</code>
   </td>
  </tr>
  <tr>
   <td><code>404</code>
   </td>
   <td><code>Resource not found</code>
   </td>
  </tr>
  <tr>
   <td><code>405</code>
   </td>
   <td><code>Method Not Allowed</code>
   </td>
  </tr>
  <tr>
   <td><code>409</code>
   </td>
   <td><code>Conflict</code>
   </td>
  </tr>
  <tr>
   <td><code>412</code>
   </td>
   <td><code>Precondition Failed</code>
   </td>
  </tr>
  <tr>
   <td><code>413</code>
   </td>
   <td><code>Request Entity Too Large</code>
   </td>
  </tr>
  <tr>
   <td><code>500</code>
   </td>
   <td><code>Internal Server Error</code>
   </td>
  </tr>
  <tr>
   <td><code>501</code>
   </td>
   <td><code>Not Implemented</code>
   </td>
  </tr>
  <tr>
   <td><code>503</code>
   </td>
   <td><code>Service Unavailable</code>
   </td>
  </tr>
</table>

