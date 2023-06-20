# Brokerless and Broker-based
In the very first day I started to work with Microservices, I had asked: why the heck we need a RabbitMQ that stay between our services?
Can we just simply send requests directly between services? Yes and no. It really depends on what we want to achieve.

## Brokerless
Send directly message (request) to a service will reduce latency, however, it will coupled services and will fail the request if one
contact point was down hence reduce availibity. Moreover, it will reduce your architecture complexity. 

Dispite the fact that this is a asynchronous pattern, it have some common requirements/behaviours with request/response pattern (synchronous). 

## Broker-based
Message broker, is it another service stay between service? Yes, it's an application where messages (QUERY, COMMAND, EVENT) come and go.
It will increase latency.

If it is another service, is there any difference with brokerless? Yes, you will (again) depend on a service, however, your own services
will be loosely coupled. 

It's still have the same drawbacks as brokerless however, current message broker (ActiveMQ, RabbitMQ, etc) are designed to have high
availabily and low latency (which we can trust). 
In additional, with proper configurations, if your services is down, your requests (messages)
will not be lost. As soon as your consumers restart and up, it will continue to pull messages from queue and continue their processes.

