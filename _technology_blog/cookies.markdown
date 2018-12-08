---
layout: post
title: Because everyone loves Cookies!
date:  2018-12-08 16:00:00
categories: main
banner_image: "because-everyone-loves-cookies.jpg"
---
"Http is a stateless protocol" we have heard this multiple times, but what does it mean? It means that server cannot figure out that two requests are coming from the same browser. 

![HTTP is a stateless protocol]({{ "/assets/images/cookies/without_cookies.png" }})

Cookies are the answer to this problem. 

![Let's add cookies]({{ "/assets/images/cookies/idea.png" }})

Cookies are a used to exchange information between server and browser in order to determine if the request comes from a client that already made a request before. Cookies are plain text that is sent back and forth between the client and the server with every Http request and response.

When a web page is requested, server sets a cookie while responding back using `Set-Cookie` key.
Browser stores these cookies and whenever a request is made by the same client, sends it back till the cookie is expired. 

![Server sets a cookie while responding to the client. Cookie is sent back and forth between server and client]({{ "/assets/images/cookies/with_cookies.png" }})

Syntax for `Set-Cookie` is as follows:

 `Set-Cookie: <cookie-name>=<cookie-value>; Expires=<date>; Domain=<domain-value>; Path=<path-value>; Secure;`

Let us take a deep dive into the options provided in `Set-Cookie`.
1. `<cookie-name>=<cookie-value>` :  This is a string of format `key=value`. This is how cookie name and cookie values are set. This value is sent to the server whenever a request is made. The `value` is stored in the  HTTP header under `Cookie` without any options. 
	`Cookie: value`

2. `Expires=<date>` : This options  determines when the cookie is to be deleted by the browser. If this option is omitted, by default cookie expires when the browser is closed. 

3.  `Domain=<domain-value>` : This option determines the domain for which cookie should be sent. By default, host name of the page setting the cookie is set as a domain, so the cookie value is sent whenever a request is made to the same host name.

4. `Path=<path-value>` : Cookie is assigned to a specific path and sent to the server only if the URL path matches. 

5.  `Secure`:  This option is a flag, which allows the cookie to be transported over SSL and HTTPS  protocols only. By default connection is automatically set to secure.

This was all about setting the cookie, but what about updating a cookie?
A cookie can be updated by sending the same `cookie_name`, `domain`, `path` and `secure`.

Example, <br/>
Existing Cookie: <br/>
 `Set-Cookie: name=Sam; Domain=soumyathinks.com; Path=/blog;`  <br/>
Updated Cookie: <br/>
 `Set-Cookie: name=Soumya; Domain=soumyathinks.com; Path=/blog;`


The response header will look something like this:
 `Cookie: name=Soumya`

This will update the existing cookie, because we have sent all the other details as it is and just changed the name from _Sam_ to _Soumya_. But what if we change one of the other options in the cookie? In that case it will create a whole new cookie.

Example, <br/>
Existing Cookie: <br/>
  `Set-Cookie: name=Sam; Domain=soumyathinks.com; Path=/blog;` <br/>
Updated Cookie: <br/>
  `Set-Cookie: name=Soumya; Domain=soumyathinks.com; Path=/;`

Note that I am setting a different path.
In this case a whole new cookie is created with two cookies with key as "name" and the header looks like this: <br/>
 `Cookie: name=Sam; name=Soumya;`

If you want to delete the cookie, just unset its value and pass an expiration date in the past. As discussed above, the cookies are deleted automatically when browser is closed, if expiration date is not set. 

Cookies have important applications in real world like allowing user to add products to their shopping carts. They are an elegant way to customize a user session and for servers to recognize a user. This is barely scratching the surface of cookies. It is a very deep topic to learn and understand. But this is where I stop today because in my next blog I will be discussing about how cookies are used in Rails. Till then keep coding!   
