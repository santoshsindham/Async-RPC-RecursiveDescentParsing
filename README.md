# Async-RPC-RecursiveDescentParsing

Remote Procedure Call or RPC is when we need to run a function on a remote computer and wait for the result.

In this project we're going to use RabbitMQ to build an async RPC system: a client and a scalable RPC server.

We will create a RPC Client class that accepts the input from the user and will remotely call a 
service on the RPC Server using RabbitMQ as  the message bus. The service on the RPC Server will
accept the input string and parse it using the Recursive Descent Parser(RDP).

```
Assuming Grammar for RDP:
	E -> x + T
	T -> (E)
	T -> x
```

#### Steps to execute:   
 - RabbitMQ is required, install it by following the instructions in the [link](https://www.rabbitmq.com/download.html)
 - For Macbook install RabbitMQ via [Homebrew](https://www.rabbitmq.com/install-homebrew.html)
 - The server can then be started with `rabbitmq-server`
 - Assuming that the RabbitMQ is running on `localhost` and port `5672`
 - This example is dependant on 
    - [amqp-client-5.7.1.jar](https://repo1.maven.org/maven2/com/rabbitmq/amqp-client/5.7.1/amqp-client-5.7.1.jar) 
    - [slf4j-api-1.7.26.jar](https://repo1.maven.org/maven2/org/slf4j/slf4j-api/1.7.26/slf4j-api-1.7.26.jar)
    - [slf4j-simple-1.7.26.jar](https://repo1.maven.org/maven2/org/slf4j/slf4j-simple/1.7.26/slf4j-simple-1.7.26.jar)
    
 - All the above three jars need to be downloaded and configured on classpath, alternately
 these jars are available in the lib directory of this project.
 - Import the project into an IDE of your choice.
 - Build the project.
 - Right click on the `RPCServer.java` and select `Run`
    - it will print `[x] Awaiting RPC requests`
 - Right click on the `RPCClient.java` and select `Run`
    - it will print `Enter the input string:`
 - Type any string and click Enter.
  
###### Sample
```
Enter the input string:
santosh
 [x] Requesting parsing of String = santosh
 [.] Got 'The input string is invalid.'

```
 
```
Enter the input string:
x+(x+(x+x))
 [x] Requesting parsing of String = x+(x+(x+x))
 [.] Got 'The input string is valid.'
``` 
 
 - As can be seen in the examples above the input string `santosh` cannot be parsed 
 with the assumed grammar above, however `x+(x+(x+x))` we were able to parse.


##### Sample Inputs for Parsing:
```
	- xxx: invalid
	- x+x+x: invalid
	- x+(x+x): valid
	- x+(x+(x+x)): valid
	- xxx: invalid
	- x+(x+x)+x: invalid 
```
  
 
