# Challenge #8: We need a mechanic!

## Instructions

Some electric sleds have broken down and the elves are looking for spare parts to fix them, but it is not clear to them if the parts they have are any good.

The spare parts are text strings and the mechanic Elfon Masc has said that a spare part is valid if the part can be a palindrome after removing at most one character.

A palindrome is a word or phrase that reads the same from left to right as it does from right to left.

Our function must return a boolean indicating whether or not the replacement part is valid with that rule:

```js
checkPart("uwu") // true
// "uwu" is a palindrome with no characters removed

checkPart("miidim") // true
// "miidim" can be a palindrome after the first "i" has been removed
// since "midim" is a palindrome

checkPart("midu") // false
// "midu" cannot be a palindrome after removing a character
```

## Solution

```js
function checkPart(part) {
  return part.split('').some((_, index) => {
    let sectioned = part.slice(0, index) + part.slice(index + 1)
    return sectioned.split('').reverse().join('') === sectioned
  })
}
```
