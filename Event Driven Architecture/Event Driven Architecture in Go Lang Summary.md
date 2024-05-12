> This summarises the book, "Event Driven Architecture in Go Lang"

## Introduction to Event Driven Architecture

Three different patterns for EDA:

- Event Notifications
- Event-Carried State Transfer
- Event Sourcing


 ### Event Notifications
 
Carry the minimum state (maybe just an ID). Consumers may need to call-back to the originator to fetch additional information.

```
type Payment Received struct {
	PaymentID string
}
```


### Event-Carried State Transfer

Data changes are sent out to be consumed (negating the need to query the originators)


```
type Payment Received struct {
	PaymentID string
	CustomerID string
	OrderID string
	Amount int
}
```


### Event Sourcing

Streams of events are stored and can be read/processed to recreate the final state of an entity.



