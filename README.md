# Difference between HTTP 1 and HTTP 2 :

## HTTP/1.0 – Building extensibility

HTTP/0.9 was very limited and both browsers and servers quickly extended it to be more versatile:

Versioning information is now sent within each request (HTTP/1.0 is appended to the GET line)
A status code line is also sent at the beginning of the response, allowing the browser itself to understand the success or failure of the request and to adapt its behavior in consequence (like in updating or using its local cache in a specific way)
The notion of HTTP headers has been introduced, both for the requests and the responses, allowing metadata to be transmitted and making the protocol extremely flexible and extensible.
With the help of the new HTTP headers, the ability to transmit other documents than plain HTML files has been added (thanks to the Content-Type header).

Request -

GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html
<HTML>
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
  
Response -

GET /myimage.gif HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:32 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/gif
(image content)
  
## HTTP/1.1 – The standardized protocol

In parallel to the somewhat chaotic use of the diverse implementations of HTTP/1.0, and since 1995, well before the publication of HTTP/1.0 document the next year, proper standardization was in progress. The first standardized version of HTTP, HTTP/1.1 was published in early 1997, only a few months after HTTP/1.0.

HTTP/1.1 clarified ambiguities and introduced numerous improvements:

A connection can be reused, saving the time to reopen it numerous times to display the resources embedded into the single original document retrieved.
Pipelining has been added, allowing to send a second request before the answer for the first one is fully transmitted, lowering the latency of the communication.
Chunked responses are now also supported.
Additional cache control mechanisms have been introduced.
Content negotiation, including language, encoding, or type, has been introduced, and allows a client and a server to agree on the most adequate content to exchange.
Thanks to the Host header, the ability to host different domains at the same IP address now allows server colocation.

## More than 15 years of extensions

Thanks to its extensibility – creating new headers or methods is easy – and even if the HTTP/1.1 protocol was refined over two revisions, RFC 2616 published in June 1999 and the series of RFC 7230-RFC 7235 published in June 2014 in prevision of the release of HTTP/2, this protocol has been extremely stable over more than 15 years.

### Using HTTP for secure transmissions

The largest change that happened to HTTP was done as early as end of 1994. Instead of sending HTTP over a basic TCP/IP stack, Netscape Communications created an additional encrypted transmission layer on top of it: SSL. SSL 1.0 was never released outside the company, but SSL 2.0 and its successor SSL 3.0 allowed for the creation of e-commerce Web sites by encrypting and guaranteeing the authenticity of the messages exchanged between the server and client. SSL was put on the standards track and eventually became TLS, with versions 1.0, 1.1, 1.2, and 1.3 appearing successfully to close vulnerabilities.

During the same time, the need for an encrypted transport layer raised: the Web left the relative trustiness of a mostly academic network, to a jungle where advertisers, random individuals or criminals compete to get as much private information about people, try to impersonate them or even to replace data transmitted by altered ones. As the applications built over HTTP became more and more powerful, having access to more and more private information like address books, e-mail, or the geographic position of the user, the need to have TLS became ubiquitous even outside the e-commerce use case.

### Using HTTP for complex applications

The original vision of Tim Berners-Lee for the Web wasn't a read-only medium. He envisioned a Web where people can add and move documents remotely, a kind of distributed file system. Around 1996, HTTP has been extended to allow authoring, and a standard called WebDAV was created. It has been further extended for specific applications like CardDAV to handle address book entries and CalDAV to deal with calendars. But all these *DAV extensions had a flaw: they had to be implemented by the servers to be used, which was quite complex. Their use on Web realms stayed confidential.

In 2000, a new pattern for using HTTP was designed: representational state transfer (or REST). The actions induced by the API were no more conveyed by new HTTP methods, but only by accessing specific URIs with basic HTTP/1.1 methods. This allowed any Web application to provide an API to allow retrieval and modification of its data without having to update the browsers or the servers: all what is needed was embedded in the files served by the Web sites through standard HTTP/1.1. The drawback of the REST model resides in the fact that each website defines its own non-standard RESTful API and has total control on it; unlike the *DAV extensions where clients and servers are interoperable. RESTful APIs became very common in the 2010s.

Since 2005, the set of APIs available to Web pages greatly increased and several of these APIs created extensions, mostly new specific HTTP headers, to the HTTP protocol for specific purposes:

Server-sent events, where the server can push occasional messages to the browser.
WebSocket, a new protocol that can be set up by upgrading an existing HTTP connection.

### Relaxing the security-model of the Web

HTTP is independent of the security model of the Web, the same-origin policy. In fact, the current Web security model has been developed after the creation of HTTP! Over the years, it has proved useful to be able to be more lenient, by allowing under certain constraints to lift some of the restriction of this policy. How much and when such restrictions are lifted is transmitted by the server to the client using a new bunch of HTTP headers. These are defined in specifications like Cross-Origin Resource Sharing (CORS) or the Content Security Policy (CSP).

In addition to these large extensions, numerous other headers have been added, sometimes experimentally only. Notable headers are Do Not Track (DNT) header to control privacy, X-Frame-Options, or Upgrade-Insecure-Requests but many more exist.

## HTTP/2 – A protocol for greater performance

Over the years, Web pages have become much more complex, even becoming applications in their own right. The amount of visual media displayed, the volume and size of scripts adding interactivity, has also increased: much more data is transmitted over significantly more HTTP requests. HTTP/1.1 connections need requests sent in the correct order. Theoretically, several parallel connections could be used (typically between 5 and 8), bringing considerable overhead and complexity. For example, HTTP pipelining has emerged as a resource burden in Web development.

In the first half of the 2010s, Google demonstrated an alternative way of exchanging data between client and server, by implementing an experimental protocol SPDY. This amassed interest from developers working on both browsers and servers. Defining an increase in responsiveness, and solving the problem of duplication of data transmitted, SPDY served as the foundations of the HTTP/2 protocol.

### The HTTP/2 protocol has several prime differences from the HTTP/1.1 version:

It is a binary protocol rather than text. It can no longer be read and created manually. Despite this hurdle, improved optimization techniques can now be implemented.
It is a multiplexed protocol. Parallel requests can be handled over the same connection, removing the order and blocking constraints of the HTTP/1.x protocol.
It compresses headers. As these are often similar among a set of requests, this removes duplication and overhead of data transmitted.
It allows a server to populate data in a client cache, in advance of it being required, through a mechanism called the server push.
Officially standardized, in May 2015, HTTP/2 has had much success. By July 2016, 8.7% of all Web sites were already using it (see these stats), representing more than 68% of all requests (see these statistics). High-traffic Web sites showed the most rapid adoption, saving considerably on data transfer overheads and subsequent budgets.

This rapid adoption rate was likely as HTTP/2 does not require adaptation of Web sites and applications: using HTTP/1.1 or HTTP/2 is transparent for them. Having an up-to-date server communicating with a recent browser is enough to enable its use: only a limited set of groups were needed to trigger adoption, and as legacy browser and server versions are renewed, usage has naturally increased, without further Web developer efforts.

## Post-HTTP/2 evolution

HTTP didn't stop evolving upon the release of HTTP/2. Like with HTTP/1.x previously, HTTP's extensibility is still being used to add new features. Notably, we can cite new extensions of the HTTP protocol appearing in 2016:

Support of Alt-Svc allows the dissociation of the identification and the location of a given resource, allowing for a smarter CDN caching mechanism.
The introduction of Client-Hints allows the browser, or client, to proactively communicate information about its requirements, or hardware constraints, to the server.
The introduction of security-related prefixes in the Cookie header, now helps guarantee a secure cookie has not been altered.
This evolution of HTTP proves its extensibility and simplicity, liberating creation of many applications and compelling the adoption of the protocol. The environment in which HTTP is used today is quite different from that seen in the early 1990s. HTTP's original design proved to be a masterpiece, allowing the Web to evolve over a quarter of a century, without the need of a mutiny. By healing flaws, yet retaining the flexibility and extensibility which made HTTP such a success, the adoption of HTTP/2 hints at a bright future for the protocol.


# Objects and its Internal representation in Javascript :
  
Objects and its Internal Representation in Javascript. Objects are the representation of real-world entities in any language representing things by defining its properties along with their values. In Javascript, objects may be defined as an unordered collection of related data, of primitive or reference types, in the form of “key: value” pairs.
  
  An object is a collection of properties, and a property is an association between a name (or key) and a value. A property’s value can be a function, in which case the property is known as a method.
  
A JavaScript object has properties associated with it. A property of an object can be explained as a variable that is attached to the object. Object properties are basically the same as ordinary JavaScript variables, except for the attachment to objects. The properties of an object define the characteristics of the object. We can access the properties of an object with a simple dot-notation:
  
### objectName.propertyName :
  
Like all JavaScript variables, both the object name (which could be a normal variable) and property name are case sensitive. You can define a property by assigning it a value. For example, let’s create an object named myCar and give it properties named make, model, and year as follows:
  
var myCar = new Object();
  
myCar.make = ‘Ford’;
  
myCar.model = ‘Mustang’;
  
myCar.year = 1969;
  
The above example could also be written using an object initializer, which is a comma-delimited list of zero or more pairs of property names and associated values of an object, enclosed in curly braces ({}):
  
var myCar = {
  
make: ‘Ford’,
  
model: ‘Mustang’,
  
year: 1969
  
};
  
## JavaScript’s internal representation of Objects:
A simple diagram is probably the best way to give a quick overview of the object representation in Javascript.

Most objects contain all their properties in a single block of memory (‘a’ and ‘b’). All blocks of memory have a pointer to a map, which describes their structure.
Named properties that don’t fit in an object are usually stored in an overflow array (‘c’ and ‘d’).
Numbered properties are stored separately, usually in a contiguous array.
The JavaScript standard allows developers to define objects in a very flexible way, and it is hard to come up with an efficient representation that works for everything. An object is essentially a collection of properties: basically key-value pairs. We can access properties using two different kinds of expressions:
obj.prop
obj[“prop”]
According to the spec, property names are always strings. If we use a name that is not a string, it is implicitly converted to a string. This may be a little surprising: if we use a number as a property name, it gets converted to a string as well. So a JavaScript object is basically a map from strings to values.
