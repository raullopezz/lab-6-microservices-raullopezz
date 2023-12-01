# Lab 6

## REPORT
This document contains a brief of how the following activities have been accomplished:

- Create your own configuration repository based on <https://github.com/UNIZAR-30246-WebEngineering/lab6-microservices-config-repo>
  and update the configuration of your service `config` to use it. **Link to the repository**.
- Two services `accounts (2222)` and `web` are running and registered (two terminals). **2 Log screenshot**.
- The service registration service has these two services registered (a third terminal). **Eureka dashboard screenshot**.
- Update the configuration repository so that the `accounts` service uses now the port 3333. **Link to the commit**.
- Run a second instance of the `accounts` service using the new configuration (a fourth terminals). What happens? **Explain and Eureka dashboard screenshot**
- What happens when you kill the service `accounts (2222)` and do requests to `web`?. **Explain and screenshots, including at least one Eureka dashboard screenshot**
- Can the web service provide information about the accounts again?. Why? **Explain and screenshots, including at least one Eureka dashboard screenshot**

### STEP 1
Here is the link to the repository: <https://github.com/raullopezz/lab6-microservices-config-repo/tree/main>. Here is 
also the update of the configuration of the service:
![image](/docs/configServer.png)

### STEP 2
Here we are going to start de registration application. It will lunch the discovery service Eureka in the 8761 port. 
If we access to this application on the navigator with _localhost:8761_, this is what we see:
![image](/docs/step2_1.png)

And we will see this on the terminal:
![image](/docs/step2_1.png)

Then, we will launch the service config. It will use the port 8762 and will provide the configuration for the other services.
We can observe something like the following picture (_localhost:8762/account-service/default & terminal_):
![image](/docs/step2_2.png)

After that,  we are going to launch the account service. It is a standalone process that provides a RESTful server to a 
repository of accounts that will use the port 2222. What it makes special is that it registers itself to Eureka with the
name **ACCOUNTS-SERVICE**. After launching this service you can see in the dashboard of Eureka that after a few seconds 
(10-20 secs) the ACCOUNTS-SERVICE service appears.
We can observe something like the following picture (_localhost:2222 & terminal_):
![image](/docs/step2_3.png)

Next, we have to launch the web application one, which works at port 4444. It is an Eureka client and defines
a web server.
We can observe something like the following picture (_localhost:4444 & terminal_):
![image](/docs/step2_4.png)

### STEP 3
After launch all the servicies, the registration service has these two services registered (ACCOUNTS-SERVICE and WEB-SERVICE) and
one config server registered (the CONFIGSERVER). We can see it on the web browser at port 8761.
![image](/docs/step3.png)

### STEP 4
Here is the link to the commit where we change to configuration to make account service use the 3333 port.
<https://github.com/raullopezz/lab6-microservices-config-repo/commit/aa9a105c5d7465be1c8622418dbc9cd1aab90af4>

### STEP 5
After changing the port, we launch the config service and the account service (port 2222 and port 3333)
![image](/docs/step5.png)

### STEP 6
Now, if we kill the account service in the port 2222 with _CTRL + C_, the eureka registration service frontend 
inmediately doesn't show the instance.
![image](/docs/step6.png)

### STEP 7
If we try to get information about the accounts, there won't be any errors. We will see in the picture how the request has worked 
and how the terminal shows the information.
![image](/docs/step7_2.png)

This is happenning because the web server searches for the account service in the Eureka
server, and it finds the account service in the port 3333. So everything is still working porperly even thought we have 
killed the accounts service on port 2222.
![image](/docs/step7.png)


