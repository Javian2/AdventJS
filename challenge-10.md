# Challenge #10: Santa Claus sleigh jumping

## Instructions

Create a program that checks that Santa's sleigh makes a parabola when jumping between cities. You receive an array of numbers representing the height at which the sleigh is at any given moment.

For the parabola to be correct, the sleigh's journey must be upwards at the beginning, reach the highest point and then descend to the end. It cannot go up again once it has descended, nor can it start the journey going down. Let's look at some examples:

```js
const heights = [1, 3, 8, 8, 5, 2]
checkJump(heights) // true

/*
It's `true`.
The jump goes from bottom to top and then top to bottom:

    8 (punto más alto)
   ↗ ↘
  3   5
 ↗     ↘
1       2
*/

const heights = [1, 7, 3, 5]
checkJump(heights) // false

/*
It's `false`.
It goes from bottom to top, top to bottom, and then back up again.

  7   5 
 ↗ ↘ ↗
1   3
*/
```

We need the program to return a boolean indicating whether the sled is making a parabola or not.

To be taken into account

- For the jump to be valid, it has to go up once and down once. If during the jump you stay at the same height between two positions, the parabola continues.
- It is not necessary that the start and end points are the same (the cities can be at different heights).

## Solution

```js
function checkJump(heights) {
  const peakIndex = heights.indexOf(Math.max(...heights))

  if(peakIndex === 0 || peakIndex === heights.length - 1) return false
  
  return heights.every((item, index) => {
    return index === 0 || (
      index <= peakIndex
        ? item >= heights[index - 1]
        : item <= heights[index - 1]
    )
  })
}
```
