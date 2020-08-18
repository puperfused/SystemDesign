# **Client Server Model - Communications & Events**
- There are different communication protocols available in client server model like HTTP request, HTTP Polling, Long Polling, WebSockets and Server Sent Events(SSE). While building a real-time web application where we need to send our data from the server to the client and vice-versa, it becomes necessary to analyse the various options available for communication for better performance and efficiency. Lets understand how a standard HTTP web request looks like and works.

## **HTTP Request**
---
- To make a request to the server for the data, client first needs to establish a connection (by handshaking). A connection is opened and server do some processing and returns the response to the client on the same opened connection, and then closes the connection. 
- Example: Fetching profile information on facebook.



## **HTTP Polling**
---
- The client can make a request to the server for the data using the http request, and keeps on knocking the door of the server at regular interval (say after every 3 sec) for a response. The server will only return useful response once its processing is completed otherwise it will keep sending empty responses at the time of knock.
- This method has several disadvantages like, getting lots of empty responses increasing the number of network calls which in itself is considered as expensive task. Also it increases the header overhead, consider you have requested for 1kb of data but you are attaching a JWT token of 16kb(assume, as it can be this large in size), in every network calls.
- Consider whatsapp application, if we are using HTTP Polling, it will keep on polling for the data, but most of the times it will get empty response, and hence drains the batter of the mobile.
- There might be some delay in delivering of message(mostly the interval duration, 3 sec in our case), as we are continously polling after every 3 sec, but this can be a better fit for a usecase where we ask or poll for the location update of the delivery guy, there having some delay will not cause us any harm, although not recommended.

<br><br><br><br><br><br><br><br><br><br><br>

## **HTTP Long Polling**
---
![Long Polling]("C:\Users\abhi9\Pictures\longPolling.jpeg")
- To better understand this scenario, consider you are riding a car, there is a child in the back seat. He keeps on asking you, are we there? are we there? Irritating, right? (HTTP Polling) So you tell him, to count the number of cross, we will reach our destination after 50 crosses. So he asks you again after 50 crosses, are we there ? 
- Similar thing happens in Long polling, after a client ask or request for data, you tell the client to wait for certain amount of time(like counting 50 crosses), and after that it comes again asking for the data, and server may or may not reply with the data if the processing is still incomplete.
- Client waits for the response from server, by keeping the connection open, hence long polling.
- After the response, client can make another request, in the similar manner.
- Each request has a timeout, the client needs to reconnect periodically after the connection is closed due to timeouts.
- Consider whatsapp, if we want to use long polling, messaging would be rather better as compared to normal HTTP Polling, as there be no or almost no empty response, although timeout and reconnection might cause issue.
- There are various disadavantages, like Header Overhead, Maximal Latency, Connection establishment, Performance degradation, timeouts, but we can have a better solution than long polling.


<br><br><br><br><br><br><br><br><br><br><br><br>

## **WebSockets**
---
![WebSockets]("C:\Users\abhi9\Pictures\websocket.jpeg")
- Its opposite of Long Polling, websocket is persitent connection between the client and the server and you are constantly transmitting the data in this connection. Best thing is, its a duplex connection, meaning the client and server both can send data at any time, hence providing full-duplex communication over *single TCP connection*.
- Client send request (using handshaking) to the server, and then a TCP connection gets established between the server and client through websocket.
- It will further reduce the overhead of handshaking again and again as we are doing handshaking only once, that too at the beginning.
- Again take the example of whatsapp, if we are implementing websockets here, we can easily send and receive messages in realtime to and from the server. It can be considered as much better solution so far.
- There can be unlimited number of connections possible with websockets, as long as your hardware is able to handle that many number of connections.

<br><br><br>

## **Server Sent Events**
---
![Server Sent Event]("C:\\Users\\abhi9\\Pictures\\sse.jpeg")
- SSE is unidirectional, you establish the connection once(which stays for long) and then the server sends the data to you proactively. So its a server push technology, enabling a client to receive automatic updates from a server, but you can no longer talk to the server. After establishing the connection you can no longer request for anything from the server, the clients subscribes and the server starts pushing data to the client.
- If you want to send anything to the server, for that you will have to use normal HTTP Request.
- Best usecase for such kind of connection is realtime data of stock market, as we will be getting updates from the server continously, and we dont do any updates on it or send any update request (which is managed by other process).


> *Abhishek*<br>
> *07 June, 2020*