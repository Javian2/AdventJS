# Challenge #14: The best way

## Instructions

Father Christmas is building ice pyramids at the North Pole to train his reindeer.

Each reindeer starts at the top of the pyramid and must choose the optimal path down to travel it in the shortest possible time. Each level has a number that determines the time it takes to get there.

Upon reaching a position, the reindeer can only slide downwards and diagonally to the left or right. Visually, the pyramid looks like this:

```js
    0
   / \
  7   4
 / \ / \
2   4   6
```

In code we represent it as follows:

```js
[
  [0],
  [7, 4],
  [2, 4, 6]
]
```

Santa needs a program that tells him the minimum time it can take for each reindeer to slide down the pyramid using the most optimal path.

In the example above, the most optimal path is 0 -> 4 -> 4, which takes a total of 0 + 4 + 4 = 8 units of time. The result would be: 8.

Why is it not 6? It is not 0 -> 4 -> 2 because when it goes down to the position of 4 it cannot diagonally reach the position of 2 anymore. So the shortest possible path is 8. More examples:

```js
getOptimalPath([[0], [2, 3]]) // 2
// 0 -> 2

getOptimalPath([[0], [3, 4], [9, 8, 1]]) // 5
// 0 -> 4 -> 1

getOptimalPath([[1], [1, 5], [7, 5, 8], [9, 4, 1, 3]]) // 8
// 1 -> 1 -> 5 -> 1
```

To be taken into account

- Note that you can only go down diagonally and downwards from any position.
- The first position of the pyramid can be different from 0.
- Pyramids can have up to 10 levels.
- The numbers in the pyramids can be negative.

## Solution

```js
function getOptimalPath(path) {
  return path.reduceRight((previous, current) => {
    return current.map((val, index) => {
      return val + Math.min(previous[index], previous[index + 1])
    })
  })[0]
}
```
