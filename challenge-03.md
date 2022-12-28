# Challenge #3: How many boxes of presents can Father Christmas carry?

## Instructions

You have a box of Christmas presents that Father Christmas wants to deliver to the children. Each present is represented by a chain. Santa has a sleigh that can carry a limited weight, and each present inside the box has a weight that is equal to the number of letters in the name of the present.

Santa also has a list of reindeer that can help him deliver the presents. Each reindeer has a maximum weight limit that he can carry. The maximum weight limit of each reindeer is equal to twice the number of letters in its name.

Your task is to implement a function distributeGifts(packOfGifts, reindeers) that receives a box of gifts and a list of reindeer and returns the maximum number of boxes of these gifts that Santa can deliver to children. The gift boxes cannot be split.

```js
const packOfGifts = ["book", "doll", "ball"]
const reindeers = ["dasher", "dancer"]

// el pack de regalos pesa 4 + 4 + 4 = 12
// los renos pueden llevar (2 * 6) + (2 * 6) = 24
// por lo tanto, Santa Claus puede entregar 2 cajas de regalos

distributeGifts(packOfGifts, reindeers) // 2
```

Things to consider and tips:

- Gift boxes cannot be divided.
- The names of gifts and reindeer will always be greater than 0.

## Solution

```js
function distributeGifts(packOfGifts, reindeers) {
  const counterPack = packOfGifts.reduce((acc, item) => acc + item.length, 0);
  const counterReindeers = 2 * reindeers.reduce((acc, item) => acc + item.length, 0);

  return parseInt(counterReindeers / counterPack);
}
```
