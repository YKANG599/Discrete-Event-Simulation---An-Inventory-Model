# Discrete-Event-Simulation---An-Inventory-Model

## Problem Set-up
* Consider a shop that stocks a particular type of product that it sells for a price of *r* per unit.
* Customers demanding this product appear in accordance with a Poisson process with rate *λ*.
* The amount demanded by each customer is a random variable having distribution *G*.
* The shopkeeper uses a *(s,S)* ordering policy in order to maintain his stock:
   Whenever the on-hand inventory is less than s (where s < S), and there is no presently outstanding order, then an amount is ordered to bring it up to S.
* For the shopkeeper, the cost of ordering *y* units of the product is a specified function *c(y)*, and it takes *L* units of time until the order is delivered.
* The shopkeeper has to make payment as soon as the items are delivered to him.
* In addition, there is an inventory holding cost of *H* per unit item per unit time.
* Finally, suppose that when a customer demands more than the shopkeeper has, the amount on hand is sold and the remainder of the order is lost. The customer obtains the items he ordered immediately.
 ### The goal is to estimate the shop’s expected profit up to a fixed time T.

 ## DES Variable Definitions
 * Entities: Each customer is an entity. Each order placed by the shopkeeper is also an entity that needs to be represented.
 * SS: The system state will be denoted by *(x,y)*, where *x* is the amount of inventory on hand, and *y* is the amount on order.
 * Event: Events will be either a customer or an order arriving.
 * EL: The event times will be denoted as *t_0* for the next customer and *t_1* forthe time at which the order being filled will be delivered.

 ## Initialisation
 * Set *t = 0*.
 * Set *SS = (x,0)*.
 * Set the revenue, holding cost and price paid to be *R = 0,H = 0,C = 0*.
 * Generate *X* from a Poisson process with rate *λ*. This will be the time of the first customer arrival.
 * Set *EL = (X,∞)*.
 At the end of the simulation, R is the revenue earned up to time T. The profit earned will be R −H −C.

## Updating of System

### Case 1 : *t_0 < t_1* (Next event is a new customer arrival)

* Update *H = H + (t_0 − t)xh* to incorporate the holding cost.
* Update *t = t_0* (Fast-forward to time of next event).
* Generate D ∼ G, the demand of this new customer that just arrived at *t_0*.
* Let *w = min(D , x)*. This is the amount of the customer order that the shopkeeper can fulfil. In the SS, update the inventory amount *x = x − w*.
* Update the revenue earned *R = R + wr*.
* If *x<s* and *y=0* then update:
  The amount on order *y=S−x*
  The time at which the order will be fulfilled in the SS: *t_1 = t + L*.
* Generate U∼Unif[0,1] and update *t_0* in the SS: *t_0 = t−(λ/1)log(U)*

### Case 2 : *t_0 ≥ t_1* (Next event is an order arriving to the shopkeeper)
* Update *H = H + (t_1 − t)xh* to incorporate the holding cost.
* Update t = t_1 (Fast-forward to time of next event).
* Update the amount paid upon delivery by the shopkeeper: *C = C + c(y)*.
* Update SS: Update *x=x+y*, Reset *y=0,t_1=∞*.

## Parameters and Specifications in the Code
* *r = 2* dollars, the cost the shopkeeper charges a customer for each item. 
* *h = 0.25* dollars, the holding cost per unit item per unit time (day).
* *λ = 2.5*, the rate of customers arriving to the shop (per day).
* *L = 3*, the number of days for an order to arrive to the shop.
* Initialize stock *x=S* at *t=0*.
* The demand of a customer *D*, is a random variable given by *D = X + 1*, where X ∼ Bin(10, 0.8).
* For the shopkeeper, the cost price of each item is $1.
* We also add a counter to keep the track of the unmet demand from the customers over the 100 days

     
