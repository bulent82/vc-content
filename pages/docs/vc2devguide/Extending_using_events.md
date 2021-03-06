---
title: Extending using events
layout: docs
date: 2015-09-03T23:03:50.230Z
permalink: /docs/vc2devguide/Extending+using+events
---

## Events overview

Events are notifications that are broadcasted to interested parties. Events can be triggered on data changes like inserts, updates and deletes. There should be a publisher and consumer (subscriber) for events.

## Subscribe for event

It needs to create a new implementation of the generic event handler interface IObserver<EventType> in order to listen for an appropriate event. This implementation must be registered in both an IoC container and VCF, each will use it when the event of a specific type is raised.

Example:

```
//This line registers new event publisher for OrderChangeEvent
_container.RegisterType<IEventPublisher<OrderChangeEvent>, EventPublisher<OrderChangeEvent>>();
Â 
//This line register event handler. "AdjustInventoryObserver" name in IoC type registration it necessary for correct publisher type resolving.
_container.RegisterType<IObserver<OrderChangeEvent>, AdjustInventoryObserver>("AdjustInventoryObserver");
```

## Raising event

First it needs to inject IEventPublisher<EventType> in the class constructor or resolve it manually through ServiceLocator or IUnityContainer instance. Then call it Publish method with event data.

```
_eventPublisher.Publish(new OrderChangeEvent(EntryState.Added, null, order));
```

## Events processing priority

In situations when it needs to prioritize event processing, you can define an event handler with priority for your event handler execution. It needs to implement the event handler from IPriorityObserver interface and set the Priority property, which should return integer priority value. Smaller value means higher priority. That means the event handler with priority 10 will be called earlier than the handler with priority 20.

## Customer order and shopping cart events

VCF has event types OrderChangeEvent and CartChangeEvent which are raised when the shopping cart or customer order is changed, created or deleted. Each event has information about changing type and also contains original and modified objects instances for finding out changes made in order or cart.

You can define custom OrderChangeEvent or CartChangeEvent handlers in your module and thereby infiltrate into the customer order and shopping cart processing.

  
 


