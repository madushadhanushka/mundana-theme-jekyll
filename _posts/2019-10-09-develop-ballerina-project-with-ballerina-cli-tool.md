---
layout: post
title:  "Developing Ballerina project with Ballerina CLI tool"
author: dhanushka
categories: [ Programming ]
image: https://hashnode.imgix.net/res/hashnode/image/upload/v1569432967441/9pYP-2Wda.jpeg?w=1600&h=840&fit=crop&crop=entropy&auto=format&q=60
---
Ballerina is the latest programming language release of the 1.0 version in September of this year. Ballerina is a general purpose programming language particularly intended for the implementation of distributed network applications. Ballerina has built-in modules to build a distributed web application with only a few lines of code. Ballerina provides a CLI tool for the maintenance of the Ballerina project. This article is a brief introduction to the Ballerina CLI tool and how it was used.

You can download Ballerina distribution from official [Ballerina website](https://v1-0.ballerina.io/downloads/). You can begin writing Ballerina program once you download and install it. You can check the version of the ballerina installation by executing the following command.

```
ballerina version
```

This command prints the installed version of the ballerina language. You can also check the Ballerina installed folder by running the following command.

```
ballerina home
``` 

## Creating new Ballerina project using CLI

You can use following Ballerina CLI command to create a new Ballerina project.  This command creates a new folder containing the Ballerina.toml file and the src directory. All of your Ballerina descriptions and dependencies are included in this Ballerina.toml file.

```
ballerina new <project-name>
```

Now you can begin working on your project in the freshly created Ballerina project. Following command generates a module to begin writing your own Ballerina code. You should change the current directory to the Ballerina project folder to perform this command.

```
ballerina add <module-name>
```

This command generates the Ballerina folder structure inside the Ballerina module along with the Hello World Code sample in the Ballerina language.`<project_home>/src/<module_name>/main.bal` become the main entry point for your application. Tests for the module should be placed inside the `<project_home>/src/<module_name>/tests/` directory. Hello Wold program in main.bal as follows.

```
import ballerina/io;

public function main() {
    io:println("Hello World!");
}
```

You can build the project together with the test by running the following command. You can prevent running test cases by adding the ' —skip-test ' option at the end of the build command.

```
ballerina build <module-name>
```

Build command build source code and convert it into java program in '<project_home>/target/bin/' folder.If you inspect this folder, you can see a jar file with the name of the module. You can run this jar file on JVM the same way you run the standard java program.

If you need to run a module without building, you can try following command. Here you can run either the module or ballerina file.

```
ballerina run {<bal-file> | <module-name>}
```

Ballerina keep cache inside the Ballerina project. It keeps following caches in-order to speedup the building process. 
- BALO files fetched from Central.
- BIR files generated during the compilation.
- JAR file generated during the compilation

By executing the following command, Ballerina clears the cache inside the ballerina project.

```
ballerina clean
```

You can run tests only with the Ballerina program by running the following command. You can test the whole module by adding the ' -a ' option, or you can only test the particular module by specifying the name of the module.

```
ballerina test <module-name>
```

## Collaborate with others through the Ballerina central


![41505554-ea035ab6-71fa-11e8-80fe-28b495ba9e9e.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1569133593906/37sPDJvDv.png)

Ballerina central is the main place where developers can share their software with other developers. Ballerina Central functions the same way that git works. By pushing the modules, you can upload your modules to the Ballerina central. The same way you can use the module constructed by others by pulling modules. You can browse the available modules on the [Ballerina Central website](https://central.ballerina.io/search).

Following command can be used to search Ballerina module by using CLI instead of searching from Ballerina central website.

```
ballerina search <key-word>
```

Once you list the necessary module, you can pull the module into your project by running the following command.

```
ballerina pull <org-name>/<module-name>[:<version>]
```

Organization name is a logical name used for grouping modules under a common namespace. For instance, you can take the twitter module that can be used to access twitter api by running the following command.

```
ballerina pull wso2/twitter:0.9.26
```

You can use a twitter client to write a simple Ballerina code as follows to send a tweet.

```
import wso2/twitter;

twitter:TwitterConfiguration twitterConfig = {
    clientId: testClientId,
    clientSecret: testClientSecret,
    accessToken: testAccessToken,
    accessTokenSecret: testAccessTokenSecret,
    clientConfig: { secureSocket: {
                        trustStore: {
                            path: "${ballerina.home}/bre/security/ballerinaTruststore.p12",
                            password: "ballerina"
                        }
                    }
                  }
};

public function main() {
twitter:Client twitterClient = new(twitterConfig);

string status = "Twitter endpoint test";
    var result = twitterClient->tweet(status);
    if (result is twitter:Status) {
        // If successful, print the tweet ID and text.
        io:println("Tweet ID: ", result.id);
        io:println("Tweet: ", result.text);
    } else {
        // If unsuccessful, print the error returned.
        io:println("Error: ", result);
    }
}
```

If you need to publish a module in Ballerina Central, you need to create an account in Ballerina Central. Then you can get a secret token and put it into the <USER_HOME>/.ballerina/Settings.toml file. Always remember to set organization name correctly in Ballerina.toml file in your <project_home>.

## Secure password with Ballerina encrypt command

In some scenarios, you may need to use a password inside the code. Assume, for example, that you need to create a twitter bot as a previous example. Here we just keep security tokens as plain text inside the code itself. But keeping a password inside the code is a bad practice as it reveals a password to someone else who can see your source code. Ballerina provides support to hide your password from the source code and only reveal it during runtime.

To encrypt a value, you need to run the following command first. This command first asks for a value to be encrypted. Then ask for a password and verify password.

```
ballerina encrypt
```

This command generates an encrypted value using the CBC mode AES method. You can now read the secret value from the source code as follows.

```
import ballerina/io;
import ballerina/config;

public function main() {
    io:println(config:getAsString("secret.password"));
}

```

Here we use the config module to read the config file. ' secret.password ' is an alias for the real value. When this application is running, you should provide an encrypted value as a command line argument.

```
ballerina run sample --secret.password="@encrypted:{MOT+c6216tQLzSxiDfXclFg75q1ktY6+3VlCa6uhn40=}"
```

When Ballerina starts running, ask for a password. Use the password you used to encrypt the value. This program will print the word you set with the ' ballerina encrypt ' command.

## Conclusion

In this blog post, we've gone through the CLI features provided by the Ballerina language. You can easily create, build and test Ballerina project using Ballerina CLI. Ballerina central can be used to re-use modules developed by other Ballerina developers. You can also share your module with others. Download and try Ballerina today. Follow me on [twitter](https://twitter.com/dhanushkaDEV) to know more about web integration and web app development.

## References

- [https://v1-0.ballerina.io/learn/how-to-write-secure-ballerina-code](https://v1-0.ballerina.io/learn/how-to-write-secure-ballerina-code)
- [https://v1-0.ballerina.io/learn/by-example/config-api.html](https://v1-0.ballerina.io/learn/by-example/config-api.html)
- [https://devform.netlify.com/first-glimpse-of-ballerina-language/](https://devform.netlify.com/first-glimpse-of-ballerina-language/)d