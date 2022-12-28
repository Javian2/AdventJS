# Challenge #22: Lighting in tune

## Instructions

Verify that all independent sequences of Christmas lighting systems are in strictly increasing order. We have two arrays: systemNames and stepNumbers.

systemNames contains the names of the Christmas lighting systems, and stepNumbers contains the step numbers of each system.

We must check that the stepNumbers for each system are in strictly increasing order. If this is true, return true; otherwise, return false.

For example:

```js
const systemNames = ["tree_1", "tree_2", "tree_1", "tree_2", "house", "tree_1", "tree_2", "house"]
const stepNumbers = [1, 33, 10, 2, 44, 20]

checkStepNumbers(systemNames, stepNumbers) // => true.

// tree_1 has the steps: [1, 2]
// tree_2 has the steps: [33, 44]
// house has the steps: [10, 20]

// true: The steps in each system are in strictly increasing order.

checkStepNumbers(["tree_1", "tree_1", "house"], [2, 1, 10]) // => false

// tree_1 has the steps: [2, 1]
// house has the steps: [10]

// false: tree_1 has the steps in decreasing form.
```

To be taken into account

- The position of the system name in systemNames and the step number in stepNumbers correspond to the same system.
- The steps in stepNumbers may be repeated for different systems.

## Solution

```js
function checkStepNumbers(systemNames, stepNumbers) {
  const object = systemNames.reduce((acc, item, index) => {
    acc[item] 
      ? acc[item] = [...acc[item], stepNumbers[index]]
      : acc[item] = [stepNumbers[index]]
    return acc
  }, {})  
  
  return Object.values(object).every(sequence => {
    let sorted = true
    sequence.forEach((number, index) => {
      number > sequence[index + 1] && (sorted = false)
    })
    return sorted
  })
  
}
```
