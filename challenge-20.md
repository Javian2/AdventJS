# Challenge #20: More challenging journeys

## Instructions

Father Christmas has realised that even with the cooperation of all the elves he won't be able to deliver all the presents on time. That is why he is going to ask his friends at Autentia for help.

Autentia has told us that they need a programme to know which reindeer team to send to which country. There are different types of reindeer and each of them can carry a weight of gifts. For example:

```js
const reindeerTypes = [
  { type: 'Nuclear', weightCapacity: 50 },
  { type: 'Electric', weightCapacity: 10 },
  { type: 'Gasoline', weightCapacity: 5 },
  { type: 'Diesel', weightCapacity: 1 }
]
```

In the list of gifts Father Christmas has, it is stated how much each gift weighs and which country it is destined for. The weight of the gifts is always a natural number. For example:

```js
const gifts = [
  { country: 'Spain', weight: 30 },
  { country: 'Spain', weight: 7 },
  { country: 'France', weight: 17 }
]
```

Autentia tells us that, in order for the reindeer team to be sent to each country to be optimal, we should:

- Send as many reindeer as possible with the highest carrying capacity.
- Make maximum use of the weight that each reindeer can carry.
- Reindeer behave strangely and do not allow more reindeer of one type in the team than reindeer of the next type in descending order of carrying capacity.

For example. Seventeen diesel reindeer (17 * 1) would not be sent to France (17). There are reindeer with a higher carrying capacity, but you would not send a nuclear reindeer (50) either, as you would be wasting their capacity. One electric reindeer (10), one petrol (5) and two diesel (2 * 1) would be sent.

A team of three electric (3 * 10), one petrol (5) and two diesel (2 * 1) could not be sent to Spain (37), as there cannot be more electric than petrol. Nor could two electric (2 * 10), three petrol (3 * 5) and two diesel (2 * 1), as there cannot be more petrol than diesel. There should be two electric (2 * 10), two petrol (2 * 5) and seven diesel (7 * 1).

```js
const reindeerTypes = [
  { type: 'Nuclear', weightCapacity: 50 },
  { type: 'Electric', weightCapacity: 10 },
  { type: 'Gasoline', weightCapacity: 5 },
  { type: 'Diesel', weightCapacity: 1 }
]

const gifts = [
  { country: 'Spain', weight: 30 },
  { country: 'France', weight: 17 },
  { country: 'Italy', weight: 50 }
]

howManyReindeers(reindeerTypes, gifts)
// [{
//   country: 'Spain',
//   reindeers: [
//     { type: 'Electric', num: 1 },
//     { type: 'Gasoline', num: 3 },
//     { type: 'Diesel', num: 5 }
//   ]
// }, {
//   country: 'France',
//   reindeers: [
//     { type: 'Electric', num: 1 },
//     { type: 'Gasoline', num: 1 },
//     { type: 'Diesel', num: 2 }
//   ]
//  }, {
//   country: 'Italy',
//   reindeers: [
//     { type: 'Electric', num: 3 },
//     { type: 'Gasoline', num: 3 },
//     { type: 'Diesel', num: 5 }
//   ]
// }]
```

To be taken into account

- There will always be one type of reindeer with carrying capacity 1.
- There will always be at least two types of reindeer available.
- There is no limit to the number of reindeer of the same type you can send as long as you adhere to the above restrictions.
- Your function must return the reindeer sorted by load capacity from highest to lowest.

## Solution

```js
function howManyReindeers(reindeerTypes, gifts) {
  return gifts.map(gift => {
    
    let { weight, country } = gift
    const orderedReindeers = reindeerTypes
      .filter(reindeer => reindeer.weightCapacity < weight)
      .sort((a, b) => b.weightCapacity - a.weightCapacity)
    
    let sum = orderedReindeers.reduce((acc, item) => {
      return acc + item.weightCapacity
    }, 0)
    
    const reindeers = orderedReindeers.map(reindeer => {
      const num = Math.floor(weight / sum)
      weight -= num * reindeer.weightCapacity
      sum -= reindeer.weightCapacity
      return { type: reindeer.type, num: num }
    })
        
    return { country, reindeers }
  })
}
```
