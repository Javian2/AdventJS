# Challenge #16: Fixing the Santa Claus letters

## Instructions

Father Christmas is starting to receive a lot of letters but they have a lot of formatting problems. To improve the reading, he is going to write a program that, given a text, formats it according to the following rules:

- Eliminar espacios al inicio y al final
- Eliminar múltiples espacios en blanco y dejar sólo uno
- Dejar un espacio después de cada coma
- Quitar espacios antes de coma o punto
- Las preguntas sólo deben terminar con un signo de interrogación
- La primera letra de cada oración debe estar en mayúscula
- Poner en mayúscula la palabra "Santa Claus" si aparece en la carta
- Poner un punto al final de la frase si no tiene puntuación

Letters are written in English and here is an example:

```js
fixLetter(` hello,  how are you??     do you know if santa claus exists?  i really hope he does!  bye  `)
// Hello, how are you? Do you know if Santa Claus exists? I really hope he does! Bye.

fixLetter("  Hi Santa claus. I'm a girl from Barcelona , Spain . please, send me a bike.  Is it possible?")
// Hi Santa Claus. I'm a girl from Barcelona, Spain. Please, send me a bike. Is it possible?
```

To be taken into account

- You don't have to worry about punctuation marks other than commas, full stops and question marks.
- Be sure to respect the original line breaks and spaces.

## Solution

```js
function fixLetter(letter) {  
  return letter
    .trim()
    .replace(/([.,!])(.*)/g, '$1 $2')
    .replace(/([.,?!\s])(?=\1)/g, "")
    .replace(/\s+([.,?!])/g, "$1")
    .replace(/santa claus/ig, 'Santa Claus')
    .replace(/\b([.?!] \w)|(^\w)/g, m => m.toUpperCase())
    .replace(/^.*\w$/, m => m + '.')
}
```
