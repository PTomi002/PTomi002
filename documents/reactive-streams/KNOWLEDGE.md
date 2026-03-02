## Reactive Streams

### Tips and Tricks

#### Server Stops Long Running Process Without Errors

It can easily happen that the Server runs a long-running process and 
there is a firewall / reverse proxy between the Server and the Client.

If the firewall / reverse proxy times out during executing of the long-running
process ➡️ WebFlux (because of the dropped Connection) creates a Cancellation signal 
to Subscription.

This may cause the following symptoms:
- the execution just stops / froze
- there are missing logs
- the workflows look unfinished

