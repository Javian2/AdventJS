# Challenge #2: Nobody wants to work overtime

## Instructions

A billionaire has bought a social network and it doesn't bring good news. He has announced that every time a working day is lost due to a public holiday, it will have to be compensated with two hours of overtime on another day of the same year.

Obviously the people who work in the company have not been amused and are preparing a programme that will tell them the number of overtime hours they would work in a year if the new rule were to be applied.

As it is office work, your working hours are Monday to Friday. So you only have to worry about the holidays that fall on those days.

Given a year and an array with the dates of the public holidays, return the number of overtime hours that would be worked that year:

```js
const year = 2022
const holidays = ['01/06', '04/01', '12/25'] // formato MM/DD

// 01/06 es el 6 de enero, jueves. Cuenta.
// 04/01 es el 1 de abril, un viernes. Cuenta.
// 12/25 es el 25 de diciembre, un domingo. No cuenta.

countHours(year, holidays) // 2 días -> 4 horas extra en el año
```

Things to consider and tips:

- The year may be a leap year. Make the necessary checks for this, if necessary.
- Even if 31 December is a public holiday, overtime will be done in the same year and not the following year.
- The Date.getDay() method returns the day of the week of a date. 0 is Sunday, 1 is Monday, etc.

## Solution

```js
function countHours(year, holidays) {
  let horasExtra = 0;
  holidays.forEach(date => {
    let fullDate = `${date}/${year}`
    let day = new Date(fullDate).getDay()
    if(day !== 0 && day !==  6){
      horasExtra += 2
    }
  })
  return horasExtra
}
```
