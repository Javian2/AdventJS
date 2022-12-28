# Challenge #24: The ultimate challenge is a labyrinth

## Instructions

The day has come! Today we are going to deliver the presents... but the warehouses are a maze and the elves are lost.

Indielfo Jones wants to write a program that, when it receives a matrix, knows whether or not it can get out of the maze quickly from its entrance to the exit.

The mazes have the following positions:

- W: It's a wall, you can't go through it.
- S: Entry point to the warehouse.
- E: Exit point of the warehouse.
- The blank spaces are where you can pass through.

Valid movements are from one position up, down, left or right. It is not possible to move diagonally.

```js
canExit([
  [' ', ' ', 'W', ' ', 'S'],
  [' ', ' ', ' ', ' ', ' '],
  [' ', ' ', ' ', 'W', ' '],
  ['W', 'W', ' ', 'W', 'W'],
  [' ', ' ', ' ', ' ', 'E']
]) // -> true

// It's possible to exit because we start at [0, 4]
// and there is a path to the exit which is [4, 4].

canExit([
  [' ', ' ', 'W', 'W', 'S'],
  [' ', ' ', ' ', 'W', ' '],
  [' ', ' ', ' ', 'W', ' '],
  ['W', 'W', ' ', 'W', 'W'],
  [' ', ' ', ' ', ' ', 'E']
]) // -> false

// There is no way to get from [0, 4] to [4, 4].
```

Recuerda que:

- Sólo tienes que devolver si se puede salir del laberinto con un booleano.
- Las paredes W no se pueden saltar.
- No se pueden salir de los límites de la matriz, siempre hay que seguir un camino interno.

## Solution

```js
function canExit(maze) {
  let start, end;
  for (let i = 0; i < maze.length; i++) {
    for (let j = 0; j < maze[i].length; j++) {
      if (maze[i][j] === 'S') start = [i, j];
      if (maze[i][j] === 'E') end = [i, j];
    }
  }

  const queue = [start];
  const visited = new Array(maze.length).fill(false).map(() => {
    return new Array(maze[0].length).fill(false)
  });
  
  const directions = [[-1, 0], [1, 0], [0, -1], [0, 1]];

  const isValid = (x, y) => {
    return x >= 0 && x < maze.length && y >= 0 
    && y < maze[x].length && maze[x][y] !== 'W' 
    && !visited[x][y];
  }

  const isEnd = (x, y) => {
    return x === end[0] && y === end[1];
  }

  while (queue.length) {
    const [x, y] = queue.shift();
    if (isEnd(x, y)) return true;
    visited[x][y] = true;
    for (const [dx, dy] of directions) {
      const newX = x + dx;
      const newY = y + dy;
      if (isValid(newX, newY)) queue.push([newX, newY]);
    }
  }

  return false;
}
```
