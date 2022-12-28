# Challenge #4: A box inside a box and another...

## Instructions

Santa needs to do a check of his gift boxes to make sure he can pack them all in his sleigh. He has a number of boxes of different sizes, characterised by their length, width and height.

Your task is to write a function that, given a list of boxes with their sizes, determines whether it is possible to pack all the boxes into one box so that each box contains another box (which in turn contains another box, and so on).

Each box represents its measurements with an object. For example: {l: 2, w: 3, h: 2}. This means that the box has a length of 2, a width of 3 and a height of 2.

A box fits into another box if all the sides of the first box are smaller than the sides of the second box. The elves have told us that boxes cannot be rotated, so you cannot put a 2x3x2 box into a 3x2x2 box. Let's look at some examples:

```js
fitsInOneBox([
  { l: 1, w: 1, h: 1 },
  { l: 2, w: 2, h: 2 }
]) // true
```

In the example above, the smallest box fits into the largest box. Therefore, it is possible to pack all boxes into one box. Now let's look at a case that does not:

```js
const boxes = [
  { l: 1, w: 1, h: 1 },
  { l: 2, w: 2, h: 2 },
  { l: 3, w: 1, h: 3 }
]

fitsInOneBox(boxes) // false
```

In the example above, the smaller box fits into the middle box, but the middle box does not fit into the larger box. Therefore, it is not possible to pack all the boxes into one box.

Note that the boxes may not come in order:

```js
const boxes = [
  { l: 1, w: 1, h: 1 },
  { l: 3, w: 3, h: 3 },
  { l: 2, w: 2, h: 2 }
]

fitsInOneBox(boxes) // true
```

In the example above, the first box fits into the third box, and the third box fits into the second box. Therefore, it is possible to pack all the boxes into one box.

Things to consider and tips:

- Boxes cannot be rotated as the elves have told us that the machine is not ready.
- Boxes can come unordered in size.
- Boxes are not always square, they can be rectangular.

## Solution

```js
function fitsInOneBox(boxes) {
  return boxes
    .sort((a, b) => (a.l + a.w + a.h) - (b.l + b.w + b.h))
    .every((box, index) => {
      let nextBox = boxes[index + 1]
      return index === boxes.length - 1 
        ? true
        : box.l < nextBox.l && box.w < nextBox.w && box.h < nextBox.h
    })
}
```
