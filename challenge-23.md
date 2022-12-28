# Challenge #23: The Santa Claus Compiler

## Instructions

We are testing a new CPU for Santa's sleigh. But we still have to program the software to make it work.

The CPU has 8 registers available, which are called V00..V07. At the start of the program, all registers contain 0. The CPU supports the following instructions:

- MOV Vxx,Vyy: copies the value of the Vxx register to the Vyy register;
- MOV n,Vxx: assigns the numeric constant n to the Vxx register (overwrites if it already has a value);
- ADD Vxx,Vyy: calculates (Vxx + Vyy) and stores the result in Vxx;
- DEC Vxx: decrements the value of Vxx by 1.
- INC Vxx: increments the value of Vxx by 1.
- JMP i: jumps to instruction number i if V00 is different from 0. i is guaranteed to be a valid instruction number and 0 would be the first instruction.

Since the CPU is 8 bits, the number it could represent ranges from 0 to 255. If you increment the number 255, it causes an overflow and results in 0.

After the last instruction has been executed, you must return an array with the result for each register. From V00 to V07. Examples:

```js
executeCommands([
  MOV 5,V00', // V00 is 5
  MOV 10,V01', // V01 is 10
  'DEC V00', // V00 is now 4
  'ADD V00,V01' // V00 = V00 + V01 = 14
])

// Output: [14, 10, 0, 0, 0, 0, 0, 0, 0, 0]

executeCommands([
  'MOV 255,V00', // V00 is 255
  'INC V00', // V00 is 256, overflows 0
  'DEC V01', // V01 is -1, overflows to 255
  'DEC V01', // V01 is 254
])

// Output: [0, 254, 0, 0, 0, 0, 0, 0, 0, 0]

executeCommands([
  'MOV 10,V00', // V00 is 10
  'DEC V00', // decrements V00 by 1 <---┐
  'INC V01', // increments V01 by 1 <---┐
  'JMP 1', // loop until V00 is 0 ----┘
  'INC V06' // increments V06 by 1
])

// Output: [ 0, 10, 0, 0, 0, 0, 0, 0, 1, 0 ]
```

All instructions provided are already validated and guaranteed to be correct.

Based on CodeSignal's SpaceX technical interview.

## Solution

```js
function executeCommands(commands) {
  
  const cpu = [0, 0, 0, 0, 0, 0, 0, 0]
  
  const instructions = {
    MOV: (params) => {
      const [x, y] = params.split(',')
      x.startsWith('V')
        ? cpu[+y.at(-1)] = cpu[+x.at(-1)]
        : cpu[+y.at(-1)] = +x
    },
    ADD: (params) => {
      const x = +params.split(",")[0].at(-1)
      const y = +params.split(",")[1].at(-1)
      cpu[x] = (cpu[x] + cpu[y]) % 256
    },
    DEC: (params) => {
      const position = +params.at(-1)
      cpu[position] === 0 
        ? cpu[position] = 255 
        : --cpu[position]
    },
    INC: (params) => {
      const position = +params.at(-1)
      cpu[position] === 255 
        ? cpu[position] = 0 
        : ++cpu[position]
    },
    JMP: (params) => {
      if (cpu[0] !== 0) {
        commands = commands.concat(
          commands.slice(+params, 
          commands.indexOf('JMP ' + params) + 1)
        )
      }
    }
  }

  for (let i = 0; i < commands.length; i++) {
    const instruction = commands[i].split(' ')[0]
    const params = commands[i].split(' ')[1]
    instructions[instruction](params)
  }

  return cpu
}
```
