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
 * Set *t = 0*
 * Set *SS = (x,0)*
 * Set the revenue, holding cost and price paid to be *R = 0,H = 0,C = 0*.
 * Generate *X* from a Poisson process with rate *λ*. This will be the time of the first customer arrival.
 * Set *EL = (X,∞)*.
 At the end of the simulation, R is the revenue earned up to time T. The profit earned will be R −H −C.
