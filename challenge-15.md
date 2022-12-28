# Challenge #15: Decorating the Christmas tree

## Instructions

A couple is putting up the Christmas tree. The boy is a Christmas decorations enthusiast and wants it to be perfectly balanced. He has three types of decorations:

- Coloured balls : B
- Small gifts : R
- Pine cones : P

The Christmas tree is a triangle that has to be created. You have already assembled the base, which would be the first row, and from there you have to place the decorations upwards following a formula.

```
At the top you have :     P     R     B     P
If below you have   :    P P   B P   R P   B R
```

The combinations are also the other way round. For example, if the bottom is B P, the top is R. But it will also be R if the bottom is P B. Also, if below you have the same letter twice, above will be the same letter. For example, if below is B B, above is B.

With these rules, we could see the tree that we would generate with the base B P P R P:

```
   R
  P B
 R B B
B P R P
```

Write a program that receives the string B P R P and returns an array with the representation of the tree.

```js
decorateTree('B P R P')
// [
// 'R',
// 'P B',
// 'R B B',
// 'B P R P'
// ]

decorateTree('B B') // ['B', 'B B']
```

To be taken into account

- The program always receives the text string representing the base of the tree.
- The complete tree must be generated, i.e. the base and the rows that are generated from it, up to the top.
- You have to follow the formula to know which decoration to place in each position.

## Solution

```js
function decorateTree(base) {
  
  const combinations = {
    'PP': 'P',
    'BB': 'B',
    'RR': 'R',
    'BP': 'R',
    'PB': 'R',
    'RP': 'B',
    'PR': 'B',
    'BR': 'P',
    'RB': 'P'
  }
  
  const tree = [base]
  base = base.split(' ')
  while(tree[0].length > 1){
    base = base.slice(1).map((item, index) => {
      return combinations[base[index] + item]
    })
    tree.unshift(base.join(' '))
  }
  return tree
}
```
