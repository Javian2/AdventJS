# Challenge #18: We're out of ink!

## Instructions

We are printing the barcodes for the shipments at the Father Christmas factory. We use a number stamping system where each digit is printed with a different ink. It is an old but reliable system. However, sometimes we run out of ink for a digit.

Write a function that receives the digit for which we have no ink (a number that will be from 0 to 9) and as a second parameter, the number of barcodes to print (we start from 1 to this number that we receive).

It should return an array with the numbers that include the number that we don't have ink. Let's see an example:

```js
dryNumber(1, 15) // [1, 10, 11, 12, 13, 14, 15].

// we have no ink for digit 1
// we have to print 15 barcodes from 1 to 15
// the barcodes that will come out wrong due to lack of ink are:
// 1, 10, 11, 12, 13, 14, 15

dryNumber(2, 20) // [2, 12, 20] // no ink for the digit

// we have no ink for digit 2
// we have to print 20 barcodes from 1 to 20
// the barcodes that will come out wrong due to lack of ink are:
// 2, 12, 20
```

To be taken into account

- The number for which we do not have ink can only be from 0 to 9.
- The number for which we do not have ink can be in any position of the barcode.
- The number of barcodes to be printed can be very large.

## Solution

```js
function dryNumber(dry, numbers) {
  return Array.from(Array(numbers + 1).keys()).slice(1)
    .filter(number => {
      return String(number).includes(dry)
    })
}
```
