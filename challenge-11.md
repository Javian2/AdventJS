# Challenge #11: Father Christmas is a scrum master

## Instructions

Father Christmas is a bit worried because the preparations are taking a long time. He recently got a Scrum certification and has decided to use the methodology to organise the work of his elves.

They tell him the expected duration of the tasks with a string in the format hh:mm:ss and in the same format how long they have been working on it.

But Santa doesn't quickly find out how much time is left, so he has asked us to make a program that tells us the portion of the task that has already been completed.

For example, if the task takes 03:00:00 and they've been working for 01:00:00 then they've already completed 1/3 of the task. In code:

```js
getCompleted('01:00:00', '03:00:00') // '1/3'
getCompleted('02:00:00', '04:00:00') // '1/2'
getCompleted('01:00:00', '01:00:00') // '1/1'
getCompleted('00:10:00', '01:00:00') // '1/6'
getCompleted('01:10:10', '03:30:30') // '1/3'
getCompleted('03:30:30', '05:50:50') // '3/5
```

To be taken into account

- The time format is hh:mm:ss.
- The output format is a string a/b where a is the portion of the task - that has already been completed and b is the portion of the task that remains to be completed.
The portion is always displayed with the smallest possible fraction (e.g., 2/4 would never be displayed because it can be represented as 1/2).
- if the task
- No elves have been mistreated during the execution of this challenge nor have they had to use real Scrum.

## Solution

```js
function getCompleted(part, total) {
  //Obtengo los segundos totales de cada uno
  const arrPart = part.split(':')
  const arrTotal = total.split(':')
  
  const secPart = Number(arrPart[0] * 3600) 
    + Number(arrPart[1] * 60 
    + Number(arrPart[2])) 

  const secTotal = Number(arrTotal[0] * 3600) + 
    Number(arrTotal[1] * 60 + 
    Number(arrTotal[2])) 
  
  //Lo transformo a fracción la división entre estos
  let num = secPart;
  let den = secTotal;
  let auxiliar;
  while (den) {
    auxiliar = num % den; num = den; den = auxiliar;
  }
  return `${secPart / num}/${secTotal / num}`
}
```
