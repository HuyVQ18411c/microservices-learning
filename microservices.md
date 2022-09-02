# Microservices key points:
The first thing I would like to do is to note down a few key points that I have learned so far about this architecture, then I will discuss more about it. 
* CI/CD is a crucial and essential part. Automation should be adapted.
* Logging/Tracing helps you to monitor your system.
* Domain Driven Design suits for Microservices. Bounded context should be considered thoroughly. 
* Microservices architecture suits for Agile.
* Latency and Gridlock should be taken into consideration.
* Asynchronous should be used to transfer data across services, although it could totally possible to use synchronous requests.
* Microservices give you a great sense of distribution and scalability.
* Deployment setup for microservices could be really hard to manage. 
* An API layer or proxy layer on top of services should be taken into account.
* Manage 3rd party APIs with an edge service.
  
### Now let discuss about each of them!
# CI/CD: essential part
This term may not be new to many of us nowadays, literally every products have their own pipelines setup on Jenkins or Github Actions to run and build their applications as soon as it's being push to a SCM. 

Since Microservices have so many "micro" services which may be splitted into tons of different repos of submodules in a huge repo, we need a way to build it automatically, so that we don't need to go through every domain when there are a huge release comming up. It could be a pain for the deployer. 

CI/CD comes to rescue!

It's not solely about building your applications, it also help you to double check your code quality whether it has passed all kind of tests, or it has any code smells need to be updated (SonarQueube as an example).
# Logging/Tracing: monitor your system
Logging/Tracing also exists and play an important part in Monolothic architecture, however, debug for Monolothic application could be (in my opinion) more precise and apparent.

In microservices architecture, many services will be linked to each other, and each of them may be linked externally with 3rd parties which may become disaster when there is sudden bug in your system. 

If you choose to link your app with event-based system, you could see we sometimes will not have a good way to determine which service failed to process or transfer the data. Since it failed within a service, there are no actual way to know from your requester (service). 

This is where logging and tracing are going to come in handy. The more info you add to your log, the more you know about the failure. A centralized logging system such as [Kibana](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiYhe-b5eT5AhUFq1YBHRAeBXwQFnoECAoQAQ&url=https%3A%2F%2Fwww.elastic.co%2Fkibana&usg=AOvVaw1GhD_mgvtW6eKQAhWuJR19) (open source base on Elasticsearch) will help you to gather all the info and categorized it. Database could also be a choice to keep track of failed data, instead of output the whole failed message and failed data at the same time, you could keep the data state in the database, then log only the key id of it. 
# Domain Driven Design
# Latency & Grid lock
# Asynchronous requests
# Distribution & scalability
# Agile Friendly
# Bounded context
# Edge service (connect and control 3rd party service)
# API Layer (Proxy) 



