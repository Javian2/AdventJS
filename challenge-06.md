# Challenge #6: Creating Christmas decorations

## Instructions

A couple of Christmas enthusiasts have set up a Christmas ornament company. The first ornament they want to make is a cube to put on trees.

The problem is that they have to program the machine and they don't know how to do it. They have asked us to help them do it.

To create the cubes, they pass a number with the desired size to the program and it returns a string with the design of that size. For example, if we pass a 3, the program should return a 3x3x3 cube:

```js
const cube = createCube(3)
```

```js
  /\_\_\_\
 /\/\_\_\_\
/\/\/\_\_\_\
\/\/\/_/_/_/
 \/\/_/_/_/
  \/_/_/_/
```

As you can see the cube has three faces visually. The symbols used to construct the faces of the cube are: /, \, _ and (blank space).

Other examples of cubes:

```js
const cubeOfOne = createCube(1)
```

```js
/\_\
\/_/
```

```js
const cubeOfTwo = createCube(2)
```

```js
 /\_\_\
/\/\_\_\
\/\/_/_/
 \/_/_/
```

Things to consider and tips:

- Look carefully at the blanks in the cube.1
- The cube must be symmetrical.
- Make sure you use the correct symbols.
- Each new line in the cube must end with a line break (except the last one).

## Solution

```js
function createCube(size) {
  let cubo = '';
  for(let i = 0; i < size; i++){
    cubo += `${' '.repeat(size - 1 - i)}${'/\\'.repeat(i + 1)}${'_\\'.repeat(size)}\n`
  }
  
  for(let i = 0; i < size; i++){
    cubo += `${' '.repeat(i)}${'\\/'.repeat(size - i)}${'_/'.repeat(size)}`
    if(i !== size - 1){
      cubo += '\n'
    }
  }
  
  return cubo
}
```
