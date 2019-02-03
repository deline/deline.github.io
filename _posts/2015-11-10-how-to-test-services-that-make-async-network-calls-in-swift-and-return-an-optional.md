---
id: 1479
title: How to test services that make async network calls in Swift and return an Optional
date: 2015-11-10T23:09:57+00:00
author: deline
layout: post
guid: http://delineneo.com/?p=1479
permalink: /2015/11/how-to-test-services-that-make-async-network-calls-in-swift-and-return-an-optional/
categories:
  - Programming
  - Technology
tags:
  - ios
  - swift
---
One of the things that threw me the first time I did iOS development was the fact network calls were done asynchronously by default. From an implementation side this was nice, I didn&#8217;t have to worry about blocking my main thread. But from a testing side&#8230; well that was something new.

Since then Apple&#8217;s come out with Swift. And with Swift comes the need to learn new ways to do things.  A couple of things I wanted to work out how to do nicely was:  how can I stub out my network layer as I don&#8217;t want my test to have to run against a dummy backend, and secondly how can I assert the Optional value I get back is set.

Turns out it wasn&#8217;t too tricky. The optional var was set as a result of an async call, so the easiest way to check the value is to first wait till the var has a non nil value.

And stubbing out the network layer was easily achieved by using [OHHTTPStubs](https://github.com/AliSoftware/OHHTTPStubs).

My final test ended up looking like:

<pre class="lang:swift decode:true">func testSubmitsAndProcessesResultFromRemoteService() {
    let service = CoinEntryService()
    let expectedResponse: JSON =  ["amountEnteredSoFar":NSDecimalNumber(double: 2.50), "enoughFundsEntered":false]

    stub(isHost("localhost")) {
        _ in
        return OHHTTPStubsResponse(JSONObject: expectedResponse.rawValue, statusCode: 200, headers: nil)
    }

    var coinEnteredResult: CoinEnteredResult?
    service.coinEntered(NSDecimalNumber.one()) {
        result in
        coinEnteredResult = result
    }

    expect(coinEnteredResult).toEventuallyNot(beNil())
    expect(coinEnteredResult?.amountEnteredSoFar).to(equal(NSDecimalNumber(double: 2.5)))

}</pre>

&nbsp;
