# Counting Red5 Conenctions
---


## About
---

This example demonstrates how to count the total number of connections in a Red5 Pro application. Red5 pro supports `RTMP`, `RTSP` (Android/IOS sdk) and `WebRTC` (Red5pro HTML5 SDK) type connections. All of these connection types are counted when you use the [getClientConnections](http://red5.org/javadoc/red5-server-common/org/red5/server/api/scope/IScope.html#getClientConnections--) method of the [IScope](http://red5.org/javadoc/red5-server-common/org/red5/server/api/scope/IScope.html#getClientConnections--) interface. Thsi gives you total connections in that `scope`

Similarly to look up connectiosn in a room (sub-scope) you can use the [getClientConnections](http://red5.org/javadoc/red5-server-common/org/red5/server/api/scope/IScope.html#getClientConnections--) method on the `ROOM` type scope.


## Build & Deploy
---


To deploy the war to red5 / red5 pro server :

1. Stop server if it is running.

2. Extract the content of the `war file` to directory by war name. 

> The java war file is simply a `archive file` similar to `zip` format. you can extract it using a archive tool such as [7zip](#http://www.7-zip.org/), [Winrar trial](#http://www.rarlab.com/download.htm) etc

3. Copy the folder into `RED5_HOME/webapps/` directory.

4. Start server.



## How To Use Example
---

In this example we call the method `getTotalConnections` whenever a client connects or disconnects from the application scope and/or a sub scope. The method logs the current conenctions count on the `IScope` object passed to it. To see the example in action properly you need to connect atleast 2 clients to the application one after the other sequentially. Once they are all conencted, disconenct each client in a similar fashion one after the other.

When the first client connects the `appConnect` is triggered which calls the `getTotalConnections` method. But at this point the total count will be zero because the client has not completed connection to the scope. 

```

[INFO] [NioProcessor-2] org.red5.connection.examples.totalconnections.Application - Client connect RTMPMinaConnection from 127.0.0.1 (in: 3483 out: 3073) session: 2KBUO1LL0M9FU state: connected
[INFO] [NioProcessor-2] org.red5.connection.examples.totalconnections.Application - Total connections currently in scope /default = 0

```

The `appConnect` is a callback indicating a client is attempting to conenct. When the second connection connects, the `getTotalConnections` method will log total count as 1 because it counts the the previously conencted client but not the current one.


```

[INFO] [NioProcessor-3] org.red5.connection.examples.totalconnections.Application - Client connect RTMPMinaConnection from 127.0.0.1 (in: 3483 out: 3073) session: OI2X1IAOUBNTR state: connected
[INFO] [NioProcessor-3] org.red5.connection.examples.totalconnections.Application - Total connections currently in scope /default = 1

```

## Notes
---

Alternative ways to call the `getTotalConnections` method include:

1. Add a java scheduled job to call the `getTotalConnections` method periodically
2. Invoke the `getTotalConnections` method from client as through a `RMI` (remote method invocation) call.

> Calling application adapter methods from clients as RMI is discussed in a different example.