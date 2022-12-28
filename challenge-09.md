# Challenge #9: The crazy Christmas lights

## Instructions

A company that makes Christmas lights has asked us to give them a hand.

They have LED strips that are like an array. Each position is a led and can be either on (1) or off (0).

Every 7 seconds, the LEDs change state in this way:

- If the led is off, it turns on if the led to its left (index - 1) was on before.
- If the led is on, it stays on all the time.

We have been asked for a program that tells us how many seconds must pass until all the LEDs are on. The seconds are expressed as an integer. For example:

```js
const leds = [0, 1, 1, 1, 0, 1]
countTime(leds) // 7
// 7 seconds since on the first change
// all lights turned on
// 0s: [0, 1, 1, 0, 1]
// 7s: [1, 1, 1, 1, 1]

countTime([0, 0, 0, 0, 1]) // 21
// 21 seconds as it needs three changes:
// 0s: [0, 0, 0, 1]
// 7s: [1, 0, 0, 1]
// 14s: [1, 1, 0, 1]
// 21s: [1, 1, 1, 1]

countTime([0, 0, 1, 1, 0, 0, 0]) // 28
// 28 seconds as it needs four changes:
// 0s: [0, 0, 1, 0, 0]
// 7s: [0, 0, 1, 1, 0]
// 14s: [0, 0, 1, 1, 1]
// 21s: [1, 0, 1, 1, 1]
// 28s: [1, 1, 1, 1, 1]
```
To be taken into account

- The array shall always have at least one LED on.
- The array can be of any length.
- If all LEDs are on, the time is 0.

## Solution

```js
function countTime(leds) {
  let counter = 0;
  while(leds.some(led => led === 0)){
    leds = leds.map(((x, index) => {
      return (x === 0 && leds[index === 0 ? leds.length - 1 : index - 1] === 1)
        ? 1
        : x
    }))
    counter += 7
  }
  return counter;
}
```
