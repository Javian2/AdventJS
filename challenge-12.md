# Challenge #12: Electric sledges

## Instructions

Santa Claus has new electric sledges but he has to control the power consumption as he only has a 20W battery.

We are given an array of sleds, from worst to best, with their respective consumptions. Each sled is an object with two properties: name and consumption.

The consumption field is a number representing the amount of watts (W) the sled consumes for each unit of distance. The name field is a text string representing the name of the sled.

Create a program that returns the name of the best available sled that will allow us to cover the distance.

```js
const distance = 30
const sleighs = [
  { name: "Dasher", consumption: 0.3 },
  { name: "Dancer", consumption: 0.5 },
  { name: "Rudolph", consumption: 0.7 },
  { name: "Midu", consumption: 1 }
]

selectSleigh(distance, sleighs) // // => "Dancer".

// Dasher consumes 9W for 30 sleighs of distance
// Dancer consumes 15W to travel 30 distance
// Rudolph consumes 21W to cover 30 distance
// Midu consumes 30W for a distance of 30 miles

// The best sled that can go the distance is Dancer.
// the distance is Dancer.

// Dasher goes the distance but is the worst sled.
// Rudolph and Midu can't go the distance with 20W.
```

To be taken into account

- The battery is always 20W.
- The list of sleds is ordered from worst to best sled.
- You have to return the name of the best sled that allows us to cover the distance with the watts we have available.
- If no sled is usable for the distance, return null.

## Solution

```js
function selectSleigh(distance, sleighs) {
  
  const filtered = sleighs.filter(sleigh => sleigh.consumption * distance <= 20)
  return filtered.length > 0 
    ? filtered.at(-1).name
    : null
}
```
