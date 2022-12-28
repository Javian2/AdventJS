# Challenge #5: Optimising santa travel

## Instructions

In order not to tire the reindeer, Father Christmas wants to leave as many presents as possible by making as few trips as possible.

He has an array of cities where each element is the number of presents he can leave there. [12, 3, 11, 5, 7]. On the other hand, the limit of gifts that fit in your bag. And finally, the maximum number of cities your reindeer can visit.

As you don't want to leave a city half full, if you can't leave all the gifts that are from that city, you don't leave any there.

He creates a program that tells him the highest amount of gifts he could give out, taking into account the maximum number of gifts he can transport and the maximum number of cities he can visit:

```js
const giftsCities = [12, 3, 11, 5, 7]
const maxGifts = 20
const maxCities = 3

// la suma más alta de regalos a repartir
// visitando un máximo de 3 ciudades
// es de 20: [12, 3, 5]

// la suma más alta sería [12, 7, 11]
// pero excede el límite de 20 regalos y tendría
// que dejar alguna ciudad a medias.

getMaxGifts(giftsCities, maxGifts, maxCities) // 20
```
Si no se puede realizar ningún viaje que satisface los requerimientos, el resultado debe ser 0. Más ejemplos:

```js
getMaxGifts([12, 3, 11, 5, 7], 20, 3) // 20
getMaxGifts([50], 15, 1) // 0
getMaxGifts([50], 100, 1) // 50
getMaxGifts([50, 70], 100, 1) // 70
getMaxGifts([50, 70, 30], 100, 2) // 100
getMaxGifts([50, 70, 30], 100, 3) // 100
getMaxGifts([50, 70, 30], 100, 4) // 100
```

Things to consider and tips:

- maxGifts >= 1
- giftsCities.length >= 1
- maxCities >= 1
- Number of maxCities can be greater than giftsCities.length

## Solution

```js
function getMaxGifts(giftsCities, maxGifts, maxCities) {
  //Devuelvo el máximo valor encontrado en un array
  return Math.max(...
    //Donde primero obtenemos todas las combinaciones posibles de suma
    giftsCities.reduce((acc, item) => acc.concat(acc.map(x => [item].concat(x))), [[]])
    //Mapeamos para obtener la suma de estas combinaciones eliminando los arrays que superan maxCities
    .map(combination => {
      return combination.length <= maxCities
        ? combination.reduce((acc, item) => acc + item, 0)
        : 0
    })
    //Y filtramos de nuevo para eliminar los valores que superen maxGifts
    .filter(sumCombination => sumCombination <= maxGifts)
  )  
}
```
