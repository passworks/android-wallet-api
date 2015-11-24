# Passworks Android API

This document describes how to use the [Passworks Android Wallet](https://play.google.com/store/apps/details?id=io.passworks.wallet) API for regitering devices and sending push notification to the Passworks Wallet App.

# Getting started

Before using the Wallet API you need to contact Passworks Support via [api@passworks.io](mailto:api@passworks.io?subject=Android+Wallet+API+Key) asking for a API access key before staring using the API.


## Registering a Device to Receive Push Notifications for a Pass

Passworks Wallet follows Apple's Wallet oficial API for registering a device for receiveing push notifications as stated in the following document

[https://developer.apple.com/library/ios/documentation/PassKit/Reference/PassKit_WebService/WebService.html#//apple_ref/doc/uid/TP40011988-CH0-SW2](https://developer.apple.com/library/ios/documentation/PassKit/Reference/PassKit_WebService/WebService.html#//apple_ref/doc/uid/TP40011988-CH0-SW2) 

The major difference is that the Passworks Wallet App sends a [custom HTTP  header](http://tools.ietf.org/html/rfc6648) called `X-Pass-Client` with each request with the value `Passworks`.

If your system already implements the Apple Wallet (or Passbook) API you only need to take in account the new header flaging the registering device as and Android device using Passworks Wallet.

## Sending Push notifications

### Authentication

For authentication simply send the  HTTP `Authorization` header with the Wallet API Key provided by Passworks support.

```
Authorization: <Wallet App Key>
```

### The push notification request

Sending push notifications to Passworks Wallet API consists in sending a `POST` with a specific payload to the following Wallet App endpoint with the content type `"application/json"`.

```
POST https://wallet.passworks.io
```

Payload

```
{
	"passTypeIdentifier": "pass.io.passworks.public.generic",
	"pushTokens":[
	  "538156984fb963f2eccc92664f85876d72000923ea226e6befb8" , 
	  "7d633f073fa7c73750c62e6b0236423c99bb841527512fa6c0f0"
	]
}
```


|Name                | Type             | Required | Description                       |
|--------------------|------------------|----------|-------------------------|
| __passTypeIdentifier__ |  String          | Yes | The `passTypeIdentifier ` eg: *"pass.io.passworks.public.generic"*  |                
| __pushTokens__    |  Array of String | Yes | Example: ["538156984fb963f2eccc92664f85876d72000923ea226e6befb8", "7d633f073fa7c73750c62e6b0236423c99bb841527512fa6c0f0"] 


# Help us make it better

Please tell us how we can make the Passworks Wallet API better. If you have a specific feature request or if you found a bug, please use GitHub [issues](https://github.com/passworks/android-wallet-api/issues). Fork these docs and send a pull request with improvements.

To talk with us and other developers about the API open a support ticket or mail us at [api@passworks.io](mailto:api@passworks.io) if you need to talk to us.


