# Table of contents
1. [I. Proxy](#proxy)
2. [II. Lab](#lab)
3. [III. Basic markdown](#basic-markdown)
4. [IV. CICD](#cicd)

<a name="proxy"></a>
# I. Proxy

- A **proxy server** is a system or router that provides a **gateway between users and the internet** - acting as a middleman between your device and the web.
- Proxies are intermediaries between a user and a web server
- It helps **prevent cyber attackers** from entering a private network. It is a server, referred to as an “intermediary” because it goes between end-users and the web pages they visit online.
- Proxies provide a valuable layer of security for your computer. They can be set up as web filters or firewalls, protecting your computer from internet threats like malware.
- S proxy server has its **own IP address**.
- There are hardware and software versions:
  - Hardware connections sit between your network and the internet, where they get, send, and forward data from the web.
  - Software proxies are typically hosted by a provider or reside in the cloud. You download and install an application on your computer that facilitates interaction with the proxy.
- 

## 1. Forward Proxy

- This proxy sits in front of a user and acts as a mediator between users and the web servers they access. It means that the user’s request goes through the forward proxy first and then reaches the web page.
- Once the data from the internet is retrieved, it is sent to the proxy server, redirecting it back to the requester.
- From the perspective of the internet server, the request is made by the proxy server itself and not the user.
- A forward proxy can also cache information and use it to process future requests.

## 2. Reverse Proxy

- A reverse proxy server resides in front of backend servers and transfers client requests to these servers
- A reverse proxy gets the request from a client, passes it on to another server, and then forwards it back to the client, making it appear as if the initial proxy server processed it.
- These proxies make sure that users don’t reach the origin server directly

<a name="cache"></a>
# II. Cache

- Caching is the process of storing copies of files in a cache, or temporary storage location, so that they can be accessed more quickly
- Web browsers cache HTML files, JavaScript, and images in order to load websites more quickly, while DNS servers cache DNS records for faster lookups and CDN servers cache content to reduce latency.
- To shorten page load times, browsers cache most of the content that appears on the webpage, saving a copy of the webpage's content on the device’s hard drive. This way, the next time the user loads the page, most of the content is already stored locally and the page will load much more quickly.
- Browsers store these files until their **time to live (TTL)** expires or until the hard drive cache is full. (TTL is an indication of how long content should be cached.)

## 1. CDN - Content Delivery Network

- A CDN, or content delivery network, caches content (such as images, videos, or webpages) in proxy servers that are located closer to end users than origin servers.

<a name="firewall"></a>
# III. Firewall

- Firewalls have existed since the late 1980’s and started out as packet filters, which were networks set up to examine packets, or bytes, transferred between computers.

<a name="basic-markdown"></a>
# III. Basic markdown

<a name="note"></a>
> [!NOTE]
> - Markdown basic: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
> - Application Recovery Controller (ARC)
