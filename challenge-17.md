# Challenge #17: Carrying gifts in sacks

## Instructions

We are preparing the sacks for the Christmas presents but each sack has a weight limit.

We are given an array with the names of the gifts and a number which is the maximum weight each bag can carry. The weight of each gift is the length of its name.

Write a function that groups the gifts into bags and returns an array with the names of the gifts in each bag. To group the gifts, separate the names by spaces (the space does not count as weight).

But be careful! Each sack can carry a maximum weight, and if the weight of the gifts in a sack exceeds the maximum weight, the last gift in the sack must be separated and placed in the next sack.

```js
carryGifts(['game', 'bike', 'book', 'toy'], 10)
// ['game bike', 'book toy']
// en cada saco se puede llevar 10kg
// el primer saco lleva 'game' y 'bike' que pesan 4kg y 4kg
// el segundo saco lleva 'book' y ' toy' que pesan 4kg y 3kg

carryGifts(['game', 'bike', 'book', 'toy'], 7)
// ['game', 'bike', 'book toy']
// en cada saco se puede llevar 7kg
// el primer saco sólo puede llevar 'game' que pesa 4kg
// el segundo saco sólo puede llevar 'bike' que pesa 4kg
// el tercer saco lleva 'book' y 'toy' que pesan 4kg y 3kg

carryGifts(['game', 'bike', 'book', 'toy'], 4)
// ['game', 'bike', 'book', 'toy']
// en cada saco se puede llevar 4kg
// cada saco sólo puede llevar un regalo

carryGifts(['toy', 'gamme', 'toy', 'bike'], 6)
// ['toy', 'gamme', 'toy', 'bike']
// en cada saco se puede llevar 6kg
// cada saco sólo puede llevar un regalo
// fíjate que no se puede llevar 'toy toy' en un saco
// porque no está uno al lado del otro
```

To be taken into account

- Gifts are always grouped in order of appearance in the array.
- You cannot change the order of the gifts in the array when grouping them.
- All gifts can be grouped in a single bag.
- If no gifts can be grouped in a bag, an empty array is returned.

## Solution

```js
function carryGifts(gifts, maxWeight) {
  
  let pack = []
  
  gifts
    .filter(gift => gift.length <= maxWeight)  
    .forEach(gift => {
      if(pack.length === 0) pack.push(gift)
      else{
        const lastLength = pack[pack.length - 1].replace(/ /g,'').length
        const currentLength = gift.length
        lastLength + currentLength <= maxWeight 
          ? pack[pack.length - 1] += ` ${gift}`
          : pack.push(gift)
      }
    })
  
  return pack
}
```
