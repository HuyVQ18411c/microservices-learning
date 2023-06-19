# Service Discovery:
An essential part to connect services in microservices architecture, where you track all service locations (IPs and ports).

This is a very important machanism, since for modern deployment platform, you can not easily pre-defined services' locations. It can only
be known during the deployment process (when the service up and running) therefore we should have some ways to track those service,
and ensure every services are connected.

## Service Discovery with an application:
This is a straightforward approach where we add an (fairly small) application to track all IPs and ports by storing them in a database.
We can use many kind of databases, either a table in RDMS or Redis, in memory database likes Redis is tricky, we can lost all information
if it went down during run time. 

## Service Discovery with built-in machanism of deployment platform:
Docker/Kubernetes and many other virtualization services are providing built-in functionalities to track down all services' location.
In short, each service will join a network, and they can communicate with each other using the pre-assigned domain name, and resolve it
with DNS of that network (which is really similar to how our daily life browsing works! - I'm suprised.)
