# Challenge #21: Creating the gift table

## Instructions

There are many letters from children asking for gifts and it is very difficult for us to make an inventory of all of them. For this reason, we have decided to create a program that draws a table with the gifts they ask for and their quantities.

To do this, we are given an array of objects with the names of the gifts and their quantities. Write a function that receives this array and returns a string with the table drawn.

```js
printTable([
  { name: 'Game', quantity: 2 },
  { name: 'Bike', quantity: 1 },
  { name: 'Book', quantity: 3 }
])
```

```
+++++++++++++++++++
| Gift | Quantity |
| ---- | -------- |
| Game | 2        |
| Bike | 1        |
| Book | 3        |
*******************
```

Another example where you can see that the table always uses just the right amount of space depending on the length of the gift names and amounts.

```js
printTable([
  { name: 'PlayStation 5', quantity: 9234782374892 },
  { name: 'Book Learn Web Dev', quantity: 23531 }
])
```

```
++++++++++++++++++++++++++++++++++++++
| Gift               | Quantity      |
| ------------------ | ------------- |
| PlayStation 5      | 9234782374892 |
| Book Learn Web Dev | 23531         |
**************************************
```

As you can see, the size of the cells depends on the length of the gift names and quantities, although they should be at least the size of the Gift and Quantity headings respectively.

The table uses the symbols: + for the top border, * for the bottom border, - for the horizontal lines and | for the vertical lines.

To be taken into account

- Usa sólo el espacio que necesitas para dibujar la tabla.
- Adapta la tabla a la longitud de los nombres de los regalos y de las cantidades o los títulos de las columnas.
- No hace falta que ordenes los resultados.
- La tabla no termina con salto de línea.

## Solution

```js
function printTable(gifts) {
  
  let maxQuantity = Math.max(
    'Quantity'.length,
    ...gifts.map(gift => String(gift.quantity).length)
  )
  
  let maxName = Math.max(
    'Gift'.length,
    ...gifts.map(gift => gift.name.length)
  )
  
  const sumMax = maxName + maxQuantity + 7
  const topBase = ('+').repeat(sumMax) + '\n'
  const bottomBase = ('*').repeat(sumMax)
  const header = `| ${
    'Gift'.padEnd(maxName)} | ${
    'Quantity'.padEnd(maxQuantity)} |\n| ${
    '-'.repeat(maxName)} | ${
    '-'.repeat(maxQuantity)} |\n`
  
  let body = ''
  gifts.forEach(gift => {
    body += `| ${
      gift.name.padEnd(maxName)} | ${
      gift.quantity.toString().padEnd(maxQuantity)} |\n`
  })
  
  return topBase + header + body + bottomBase
}
```
