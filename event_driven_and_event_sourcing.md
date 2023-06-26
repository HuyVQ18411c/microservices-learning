# Event Drivent Architecture and Event Sourcing
## Is it the same thing?
I first had this question a while ago, when I read these 2 articles: [Event Sourcing](https://microservices.io/patterns/data/event-sourcing.html) and
[Saga](https://microservices.io/patterns/data/saga.html). I'm fascinated to see that we have a lot of patterns to follow and implement, each
of them will help us to minimize some drawbacks of Event Driven Architecture.

Event Sourcing is one of them, and yes, it's a part of Event Driven System.
## Why do we use Event Sourcing?
Of course we need some purposes to give out more efforts, Event Driven Architecture build a consise way to found communication lines between
components and Event Sourcing pattern help us to interact precisely. How?

Let take a look on concurrency, when you got an order in state `CREATED`, the 2 next events come: `CANCELED` and `ACCEPTED`, `CANCELED`
will check for the Order's state, however, at the same time when we're travelling to the database, `ACCEPTED` event is faster and update the
state to ACCEPTED (assume that we can't go backward). Hence the second event `CANCELED` failed.

Thanks to event sourcing we can carry out the transaction atomically.

Extra overhead is added to Event object, every previous actions from current state are rebuilt, and we can track down what happened with a
specific record. In order to do this, you must store all the published events to a database and since save to database is a single operation it's atomic.
A drawback of this pattern is the increase in size in the pace of lightning if your system had a large number of daily transactions (Ex: Each record from the beginning to the end has 6 states, each state has a separated event, you have to deal with approximately about 100_000 transactions a day => you will have to store: 6*100_000 = 600_000 records/day, holo moly).

For example: `Order` object have 7 states: `ORDER_CREATED`, `STORE_ACCEPTED`, `PENDING_FOR_DELIVERY`, `DELIVERED_TO_WAREHOUSE`, `DELIVERING_TO_CUSTOMER`, `FINISHED`, `CANCELED`. When your system receive event `DELIVERED_TO_WAREHOUSE`, you will be able to track the current state of the Order, what happened, and whether it's able to be proceeded which we called: replay!

After saving event, in the event store, you will now continue your business logics, sending messages to your message-broker.

### Tip for the day:
I learned this pattern while having a conversation with my line manager, he explained it to me thoroughly and gave me the general view of how Event Arch works. Small talks sometimes just pay off!
