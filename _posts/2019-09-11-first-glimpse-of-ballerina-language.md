---
layout: post
title:  "First glimpse of Ballerina language: Language of Integration"
author: dhanushka
categories: [ Programming ]
image: //miro.medium.com/max/4396/1*2MsLyXWTedL53FxjViFYPg.jpeg
---
Ballerina is the latest programming language released on September 10th of this year. There are more than a thousand programming languages out there. Why do you need another programming language? Ballerina language intended to simplify the particular programming domain known as integration. You may be a developer who develops different kinds of web services and intends to interconnect those services. Then the Ballerina language will be your next programming companion.

This post is intended to give you an introduction to Ballerina, a flexible, powerful and beautiful programming language that helps you implement any sort of integration requirements. You can download and install Ballerina from the official [Ballerinalang](https://ballerina.io/downloads/) website.

## What does it look like?
When I said that this is a programming language, the first concern that comes to your mind is how it looks. Ballerina language syntax takes shape based on programming languages such as Java, Go and JavaScript. Ballerina is a static typed language. For example, if you need to define an integer, the syntax would be the following.

```int total = 99;```

Same as the other languages, Ballerina has the main method, which is the primary program entry point. You can write a simple "hello world" as shown below.

```
import ballerina/io;

public function main() {
    io:println("Hello, World!");
}
```

Apart from regular primitive data types, Ballerina provides various non-primitive data types, such as Arrays, Tuples, Maps, Tables, Union, etc. Ballerina represent nil as bracket "()"

Another special type of variable is that "anydata" data type. This type is a union  of the `()|boolean|int|float|decimal|string|(anydata|error)[]|map<anydata|error>|xml|table` data types. anydata variables can be used in places where you expect pure values.

Since Ballerina specifically designed to construct apps operating on networks, it natively supports JSON and XML.  You can easily define a JSON variables as the following in JavaScript. 

```
json user = {
         fname: "Peter",
         lname: "Stallone",
         "age": age,
         address: {
             line: "20 Palm Grove",
             city: "Colombo 03",
             country: "Sri Lanka"
         }
    };
io:println(user.address.country);
```
Same way you can define XML object as well.
```
xml x1 = xml `<book>The Lost World</book>`;
io:println(x1);
```

Ballerina offers built-in libraries for the implementation of different kinds of functionalities. In Ballerina, this is called modules. Modules are working the same as Java packages. You can import built-in modules or your own modules into your application. Ballerina has built-in logging, math, encoding, string, caching, time, file processing, and many more modules.

Flow control of the syntax is the same as other languages. It provides support for the syntax "if else," "while" and "foreach." Foreach syntax provides iteration support over arrays and maps. If you are looking for an appealing way to verify the null, then Ballerina will give the to Elvis operator to verify whether the specified variable is null or not. Syntax would be as 'expression?: expressionIfNil' and, below, an example to verify whether variable x is null or not.
```
string elvisOutput = x ?: "value is nil";
```


## Object Oriented Programming with Ballerina
Ballerina does provide assistance for object-oriented programming. The Ballerina OOP syntax seems closer to the Python OOP syntax. Here is an example for defining objects with a constructors.

```
type Person object {
    public int age;
    public string firstName;
    public string lastName;

    function __init(int age, string firstName, string lastName) {
        self.age = age;
        self.firstName = firstName;
        self.lastName = lastName;
    }

    function getFullName() returns string {
        return self.firstName + " " + self.lastName;
    }

    function checkAndModifyAge(int condition, int a);
};

function Person.checkAndModifyAge(int condition, int a) {

    if (self.age < condition) {
        self.age = a;
    }
}
```

Instantiating object is simple and straight forward as "Person p1 = new(5, "John", "Doe");". Object can be access with dot(".") operator which is same as other languages. 
```
p1.getFullName()
```

Ballerina is providing assistance for Encapsulation. Here you can define variables within an object with the appropriate access level. Ballerina supports the following access modifiers.

- public — visible everywhere
- private — visible only within the same object
- no modifier — visible only within same package.

You can also use abstraction concepts with Ballerina. Abstraction is a powerful OOP concept that is essential in the design of big modular software. You can define and reuse abstract objects in ballerina. You can convert an object to an abstract object by using an abstract keyword.  Example abstract Person object would be as follows.

```
type Person abstract object {
    public int age;
    public string firstName;
    public string lastName;

    function getFullName() returns string;

    function checkAndModifyAge(int condition, int a);
};
```
You can reuse the Person object as follows to reuse the variables and methods in the Person objects

```
type Employee abstract object {

    *Person;    
    public float salary;

    function __init(int age, string firstName, string lastName) {
        self.age = age;
        self.firstName = firstName;
        self.lastName = lastName;
    }
    function getSalary() returns float;

};
```

There is one more remaining concept of OOP known as Polymorphism to finish OOP concepts in the Ballerina languages. Polymorphism can also be implemented in the Ballerina language as follows in previous code segments. Here, a person object can have many types, as it is an abstract class.

```
Person p = new Employee(5, "John", "Doe");
``` 

## Integration with Ballerina language
As I mentioned earlier on the introduction, Ballerina was specially designed to solve integration problems. We live in a globe where thousands of web servers are running and interacting with each other. Early developers had problems of connecting these services with each other. Enterprise Integration Bus emerges as a solution to the problems of integration. The ESB model offers an elegant way to interconnect distinct kinds of services with each other. The common issue with these ESB products is that it is difficult to configure and less flexible.

Compared to ESB, Ballerina is more user-friendly so that developers can design the system by coding. Ballerina offers built-in libraries to solve all kinds of integration problems.

The general requirement of integration is to read, forward and transform messages between distinct protocols. Ballerina provides built-in assistance for HTTP, HTTPS, HTTP2, Websockets, GRPC, TCP, UDP, etc transports.

Ballerina can function as both a client and a server. Sending a request to another endpoint is simple, as it requires only three lines of code. You can easily call the REST API backend by setting the request headers as needed. Since Ballerina supports JSON natively, you can directly manipulate JSON content within the software without importing modules from third parties.

```
import ballerina/http;
http:Client clientEndpoint = new("https://postman-echo.com");
public function main() {
    var response = clientEndpoint->get("/get?test=123");
}
```

On the other hand, you can create an HTTP server with a ballerina language. You can use built-in security features to secure your HTTPS link.

```	
import ballerina/http;
import ballerina/log;
http:ServiceEndpointConfiguration helloWorldEPConfig = {
    secureSocket: {
        keyStore: {
            path: "${ballerina.home}/bre/security/ballerinaKeystore.p12",
            password: "ballerina"
        }
    }
};

listener http:Listener helloWorldEP = new(9095, config = helloWorldEPConfig);

@http:ServiceConfig {
    basePath: "/hello"
}
service helloWorld on helloWorldEP {
    @http:ResourceConfig {
        methods: ["GET"],
        path: "/"
    }
    resource function sayHello(http:Caller caller, http:Request req) {
        var result = caller->respond("Hello World!");
        if (result is error) {
            log:printError("Error in responding ", err = result);
        }
    }
}
```
Ballerina also provides support for streaming through the HTTP interface. Building GRPC and web socket based servers is straight forward and easy as building HTTP servers.

Message brokers are one of the most important aspects of integration when it comes to reliable messaging. If you need to send messages reliably, you can use the Message Broker along with the Ballerina Integrator. Ballerina provides assistance for famous Message Brokers such as ActiveMQ, RabbitMQ and NATS. You can generate messages and receive messages with only a few lines of Ballerina codes that make it the best language to use with all integration requirements.

## Conclusion
In this article, I attempted to explain the capabilities of Ballerina as a generic programming language as well as a specialized programming language for integration. There are a lot more features like threading, streaming, security, and native support for microservices that I haven't addressed here. I'm going to clarify these features to you in detail in another article. 

You can learn more about Ballerina language from their [official site](https://ballerina.io). There you can find example implementation for each use cases. You can follow me in [twitter]() to know more about tech stuff. Go to the Ballerina [download](https://ballerina.io/downloads/) page and try it now. As its name suggests, it is flexible, powerful and beautiful.