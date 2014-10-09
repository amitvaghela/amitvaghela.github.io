---
layout: post
title: "Server trust evaluation has failed"
date: 2014-10-09 23:36:15 +1100
comments: true
categories:
---
While working iOS app I faced an issue when app was making a connection to API endpoint. After investigation I found that it was happening because of server trust evaluation failure.

{% codeblock %}
Error I was getting,
Domain=NSURLErrorDomain Code=-1202 "The certificate for this server is invalid. You might be connecting to a server that is pretending to be “example.com” which could put your confidential information at risk." UserInfo=0x14a730 {NSErrorFailingURLStringKey=https://example.com/, NSLocalizedRecoverySuggestion=Would you like to connect to the server anyway?, NSErrorFailingURLKey=https://example.com/, NSLocalizedDescription=The certificate for this server is invalid. You might be connecting to a server that is pretending to be “example.com” which could put your confidential information at risk., NSUnderlyingError=0x14a6c0 "The certificate for this server is invalid. You might be connecting to a server that is pretending to be “example.com” which could put your confidential information at risk.", NSURLErrorFailingURLPeerTrustErrorKey=<SecTrustRef: 0x14ec00>}
{% endcodeblock %}

Apple have really good [technical note](https://developer.apple.com/library/ios/technotes/tn2232/_index.html) on this matter.

### NSURLSession

Here is how I fixed it using NSURLSession delegates,

{% codeblock lang:objc %}
- (void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task didReceiveChallenge:(NSURLAuthenticationChallenge *)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential *credential))completionHandler
{
    completionHandler(NSURLSessionAuthChallengeUseCredential, [NSURLCredential credentialForTrust:challenge.protectionSpace.serverTrust]);
}
{% endcodeblock %}
