# Decomposite patterns
We are looking into every single problems of our business and current system, and now we want to migrate the legacy software to microservices architecture. 

The same old fashion, we will be able to do it by breaking down the problems and try to solve them one at a time. We can handle this by:
- Domain based decomposition
- Business based splitting
- Atomic transaction based

And there are also some famous pattern that we can lean on:
- Strangler pattern: gradually skrinking our monolothic applications, and deprecate old functionalities. 
- Sidecar pattern:

# Domain based decomposition
With this approach, we solely take care of logics within the domain instead of waving all over the place in the bussiness and so on. 

Models (or access patterns) will have a more important role than underlying database schema.

## Things to considerate when design
We should start with the models, data models rather than datastore. Because we don't want to instantly break the system, instead we re-create models, and map it to the datastore first, later on, we may do the real migrate to it. 

Consider what will we actually do on those models? Not only CRUD, everything other actions should be taken into account.

We should focus on building the API Contract and the service first which could lead us to an easier life.
# Business based decoposition
Note: business logic may be duplicated and spread all over the application. We will need to consider it thoroughly before taking any actions to breaking the business logic down, because they may have a huge effects on the running business.

We should use this approach as a higher level business layer/function and it should encapsulate related domains. This layer should not have any access to the datastore, instead it will communicate with API modules. Each part should have their own distinct functional use cases.

## Things to considerate when design
- MUST Identify process carefully.
- With the defined processes, identify which domains you want to access/consume.
- Define apis to communicate with domains.
- Since a business can be related to many services, after implementing services, wiring them is a critical stage.

# Atomic based decomposition
(Please read the `notes.md` file to have more understanding about ACID transaction)
This approach usually go with special use cases. especially when business logics are required to be processed in many services/domains. 

We will need to provide and keep track of failure domains and rollbacks in order to keep all transactions healthy. Request will only be resolved if the operation was finished, otherwise it will be blocked.

We should avoid distributed transaction. 

## Things to considerate when design
- Domains must be in shared database (which may have a huge impact in existing functionalities).
- Define transaction (step by steps).
- Define rollback conditions.
- Consider to implement service to handle fast failure and fast roll back (which will take tons of time).
- Make sure you need atomic based transaction, consider other appoach first. 

# How to get to Microservices from a legacy system
## Strangler pattern
## Sidecar pattern