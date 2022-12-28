# Challenge #19: Ordering gifts

## Instructions

The day is approaching and Father Christmas has his toy storage room in a mess. Help him to sort the toys in the warehouse so that he can find them more easily.

To do this, we are given two arrays. The first is an array of toys, and the second is an array of numbers indicating the position of each toy in the warehouse.

The only thing to take into account is that the positions may not start at 0, although they will always be consecutive and ascending numbers.

We have to return an array where each toy is in its corresponding position.

```js
const toys = ['ball', 'doll', 'car', 'puzzle']
const positions = [2, 3, 1, 0]

sortToys(toys, positions)
// ['puzzle', 'car', 'ball', 'doll']

const moreToys = ['pc', 'xbox', 'ps4', 'switch', 'nintendo']
const morePositions = [8, 6, 5, 7, 9]

sortToys(moreToys, morePositions)
// ['ps4', 'xbox', 'switch', 'pc', 'nintendo']
```

To be taken into account

- There will always be the same number of toys as positions.
- Neither the toys nor the positions are repeated.

## Solution

```js
function sortToys(toys, positions) {
  const sortedPositions = [...positions].sort((a, b) => a - b)
  return positions.map((_, index) => {
    const indexPosition = positions.indexOf(sortedPositions[index])
    return toys[indexPosition] 
  })
}

```
