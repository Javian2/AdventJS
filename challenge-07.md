# Challenge #7: Taking stock of gifts

## Instructions

Santa's warehouses are taking inventory. There are three warehouses (each represented as an Array). In each warehouse there are gifts.

We have been asked to write a program that tells us which presents to buy to replenish our warehouses now that Christmas is approaching. A gift needs to be replenished when there is only stock in one of the three warehouses.

For example, if we have the following warehouses:

```js
const a1 = ['bike', 'car', 'bike', 'bicycle', 'bicycle'].
const a2 = ['car', 'bike', 'bike', 'doll', 'car']
const a3 = ['bike', 'bike', 'pc', 'pc']

/* Store a1 has 'bike' and 'car'.
Store a2 has 'car', 'bike' and 'doll'.
Warehouse a3 has "bike" and "pc".

The gift "doll" and "pc" are only in warehouses a2 and a3 respectively.
*/

const gifts = getGiftsToRefill(a1, a2, a3) // ['doll', 'pc'] // ['doll', 'pc'] // ['doll', 'pc'] // ['pc'].
```
As you can see, the warehouses can have the same gift repeated several times. But no matter how much stock there is in one warehouse, if we don't have it in the other two, we have to replenish it to have better distribution.

Summary:

1. Create a function getGiftsToRefill that receives three Arrays as parameters.
2. The function should return an Array with the gifts to be replenished.
3. A gift must be replenished when there is only stock in one of the three warehouses.
4. If there is no gift to be replenished, the function shall return an empty Array.
5. If there is more than one gift to be replenished, the function shall return an Array with all gifts to be replenished.

## Solution

```js
function getGiftsToRefill(a1, a2, a3) {
  return [...new Set(a1.concat(a2, a3))].filter(gift => {
    return a1.includes(gift) + a2.includes(gift) + a3.includes(gift) === 1
  })
}
```
