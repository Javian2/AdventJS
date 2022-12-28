# Challenge #1: Automating the wrapping of Christmas gifts!

## Instructions

This year the elves have bought a machine that wraps presents. But... it doesn't come programmed! We need to create an algorithm to help it with the task.

The machine is given an array of presents. Each gift is a string. We need the machine to wrap each gift in wrapping paper and place it in an array of wrapped gifts.

The wrapping paper is the symbol * and to wrap a gift the symbol * is placed so that it completely surrounds the string on all sides. For example:

```js
const gifts = ['cat', 'game', 'socks']
const wrapped = wrapping(gifts)

console.log(wrapped)
/* [
  "*****\n*cat*\n*****",
  "******\n*game*\n******",
  "*******\n*socks*\n*******"
] */
```

As you can see, the string is wrapped in wrapping paper. At the top and bottom, so as not to leave any gaps, the corners are also covered by the wrapping paper.

Note: The character \n represents a line break.

Make sure you put the right number of * to completely wrap the string. But not too many. Just enough to cover the string.

Oh, and don't modify (mutes) the original array.

## Solution

```js
function wrapping(gifts) {
  return gifts.map(gift => {
    const wrap = '*'.repeat(gift.length + 2)
    return `${wrap}\n*${gift}*\n${wrap}`
  })
}
```