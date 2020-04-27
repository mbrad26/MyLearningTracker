### How the web works

#### Computers connected to the web are called **clients** and **servers**. 

  * **Clients** are the typical web user's internet-connected devices and web-accessing software available on those devices.

  * **Servers** are computers that store webpages, sites, or apps. 
  
  When a client device wants to access a webpage, a copy of the webpage is downloaded from the server onto the client machine to be displayed in the user's web browser.

In addition to the client and the server:

  * Your **internet connection**: Allows you to send and receive data on the web. 

  * **TCP/IP**: Transmission Control Protocol and Internet Protocol are communication protocols that define how data should travel across the web. 

  * **DNS**: Domain Name Servers are like an address book for websites. When you type a web address in your browser, the browser looks at the DNS to find the website's real address before it can retrieve the website. The browser needs to find out which server the website lives on, so it can send HTTP messages to the right place.

  * **HTTP**: Hypertext Transfer Protocol is an application protocol that defines a language for clients and servers to speak to each other. 

  * **Component files**: A website is made up of many different files:

     * **Code files**: Websites are built primarily from HTML, CSS, and JavaScript.
     * **Assets**: This is a collective name for all the other stuff that makes up a website, such as images, music, video, Word documents, and PDFs.

#### When you type a web address into your browser:

The browser goes to the DNS server, and finds the real address of the server that the website lives on.

The browser sends an **HTTP request** message to the server, asking it to send a copy of the website to the client. This message, and all other data sent between the client and the server, is sent across your internet connection using TCP/IP.

If the server approves the client's request, the server sends the client a "200 OK" message and then starts sending the website's files to the browser as a series of small chunks called data **packets**.

The browser assembles the small chunks into a complete website and displays it to you.

#### DNS explained

Real web addresses are special numbers that look like this: 63.245.215.20.

This is called an **IP address**, and it represents a unique location on the web. **DNS** are special servers that match up a web address you type into your browser to the website's real (IP) address.

Websites can be reached directly via their **IP addresses**. You can find the IP address of a website by typing its domain into a tool like IP Checker.

#### Packets explained

When data is sent across the web, it is sent as thousands of small chunks, so that many different web users can download the same website at the same time. If websites were sent as single big chunks, only one user could download one at a time.