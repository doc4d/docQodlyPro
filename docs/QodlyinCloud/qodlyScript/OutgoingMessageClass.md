---
id: OutgoingMessageClass
title: OutgoingMessage
---


The `4D.OutgoingMessage` class allows you to build messages to be returned by your application functions in response to [REST requests](../../Integrations/api/overview.md). If the response is of type `4D.OutgoingMessage`, the REST server does not return an object but the object instance of the `OutgoingMessage` class.

Typically, this class can be used in functions declared with the [`onHttpGet`](../qodlyScript/guides/data-model.md#onhttpget-keyword) keyword and designed to handle HTTP GET requests. Such requests are used, for example, to implement features such as download file, generate and download picture as well as receiving any content-type via a browser. 

An instance of this class is built on the Qodly server and can be sent to the browser by the [REST Server](../../Integrations/api/overview.md) only. This class allows to use other technologies than HTTP (e.g. mobile).



### Example

In this example, a `getFile()` function is implemented in the [Datastore class](../qodlyScript/guides/data-model.md#dataclass-class) and [can be called](../qodlyScript/guides/data-model.md#onhttpget-keyword) by a REST request. The purpose is to return a **testFile.pdf** file as a response to the request:

```qs
extends DataStoreImplementation

exposed onHTTPGet function getFile() : 4D.OutgoingMessage
	
	var result = 4D.OutgoingMessage.new()
	var vfile = file("/SOURCES/Shared/testFile.pdf")
	
	result.setBody(vfile.getContent())  
	result.setHeader("Content-Type", "application/pdf")
	return result
```

### OutgoingMessage Object


4D.OutgoingMessage objects provide the following properties and functions:

||
|---|
|[<!-- INCLUDE #OutgoingMessageClass.body.Syntax -->](#body)<br/><!-- INCLUDE #OutgoingMessageClass.body.Summary -->|
|[<!-- INCLUDE #OutgoingMessageClass.headers.Syntax -->](#headers)<br/><!-- INCLUDE #OutgoingMessageClass.headers.Summary -->|
|[<!-- INCLUDE #OutgoingMessageClass.setBody().Syntax -->](#setbody)<br/><!-- INCLUDE #OutgoingMessageClass.setBody().Summary -->|
|[<!-- INCLUDE #OutgoingMessageClass.setHeader().Syntax -->](#setheader)<br/><!-- INCLUDE #OutgoingMessageClass.setHeader().Summary -->|
|[<!-- INCLUDE #OutgoingMessageClass.setStatus().Syntax -->](#setstatus)<br/><!-- INCLUDE #OutgoingMessageClass.setStatus().Summary -->|
|[<!-- INCLUDE #OutgoingMessageClass.status.Syntax -->](#status)<br/><!-- INCLUDE #OutgoingMessageClass.status.Summary -->|

:::note

A 4D.OutgoingMessage object is a [non-sharable](../qodlyScript/basics/lang-shared.md) object.

:::





<!-- REF #OutgoingMessageClass.body.Desc -->
## .body

<!-- REF #OutgoingMessageClass.body.Syntax -->**body** : any<!-- END REF -->

#### Description

The `.body` property contains <!-- REF #OutgoingMessageClass.body.Summary -->the outgoing message body<!-- END REF -->. The following data types are supported in the `.body` property:

- text
- blob
- object
- image

The `.body` property is read-write.

You can also set the `.body` property using the [`setBody()`](#setbody) function, in which case the `content-type` header is automatically set. 

<!-- END REF -->


<!-- REF #OutgoingMessageClass.headers.Desc -->
## .headers

<!-- REF #OutgoingMessageClass.headers.Syntax -->**headers** : object<!-- END REF -->

#### Description

The `.headers` property contains <!-- REF #OutgoingMessageClass.headers.Summary -->the current headers of the outgoing message as key/value pairs<!-- END REF -->. 

The `.headers` property is read-only. To set a header, use the [`setHeader()`](#setheader) function. 

<!-- END REF -->


<!-- REF #OutgoingMessageClass.setBody().Desc -->
## .setBody()

<!-- REF #OutgoingMessageClass.setBody().Syntax -->**.setBody**( *body* : any )<!-- END REF -->


<!-- REF #OutgoingMessageClass.setBody().Params -->
|Parameter|Type||Description|
|---|--- |---|------|
|body|any |&#8594;|Body of the outgoing message|
<!-- END REF -->

#### Description

The `.setBody()` function <!-- REF #OutgoingMessageClass.setBody().Summary -->sets the outgoing message *body*<!-- END REF -->.

 The following data types are supported in the *body*:

- text
- blob
- object
- image

When this function is used, the content-type header is automatically set depending on the *body* type:

- Content-Type:text/plain if the body is a text
- Content-Type:application/octet-stream if body is a blob
- Content-Type:application/json if body is an object
- Content-Type:image/jpeg, image/gif... if body is an image

If *body* is not of a supported value type, an error is returned.

<!-- END REF -->


<!-- REF #OutgoingMessageClass.setHeader().Desc -->
## .setHeader()

<!-- REF #OutgoingMessageClass.setHeader().Syntax -->**.setHeader**( *key* : string , *value* : string )<!-- END REF -->


<!-- REF #OutgoingMessageClass.setHeader().Params -->
|Parameter|Type||Description|
|---|--- |---|------|
|key|string|&#8594;|Header property to set|
|value|string|&#8594;|Value of the header property|
<!-- END REF -->

#### Description

The `.setHeader()` function <!-- REF #OutgoingMessageClass.setHeader().Summary -->sets the outgoing message header *key* with the provided *value*<!-- END REF -->. If both parameters are not Text values, an error is raised.

When returning a 4D.OutgoingMessage object instance, 4D automatically sets some headers (e.g. `Set-Cookie` with `WASID4D=...` and `4DSID__ProjectName_=....`). 

:::note

If you set a *value* for the "Content-Type" header *key*, make sure you call this function after the call to [`setBody()`](#setbody), because `setBody()` automatically fills this header.  

:::


<!-- END REF -->

<!-- REF #OutgoingMessageClass.setStatus().Desc -->
## .setStatus()

<!-- REF #OutgoingMessageClass.setStatus().Syntax -->**.setStatus**( *status* : integer )<!-- END REF -->


<!-- REF #OutgoingMessageClass.setStatus().Params -->
|Parameter|Type||Description|
|---|--- |---|------|
|status|integer|&#8594;|Status to set|
<!-- END REF -->

#### Description

The `.setStatus()` function <!-- REF #OutgoingMessageClass.setStatus().Summary -->sets the `status` property with the given *status*<!-- END REF -->.

If *status* is not an integer value, an error is raised.

For a list of HTTP status codes, please refer the [HTTP status code list on Wikipedia](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes).  


<!-- END REF -->



<!-- REF #OutgoingMessageClass.status.Desc -->
## .status

<!-- REF #OutgoingMessageClass.status.Syntax -->**status** : integer<!-- END REF -->

#### Description

The `.status` property contains <!-- REF #OutgoingMessageClass.status.Summary -->the current status of the outgoing message<!-- END REF -->. This property can be set using the [`setStatus()`](#setstatus) function.

<!-- END REF -->
