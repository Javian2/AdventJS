# Challenge #13: Backup of Santa Claus files

## Instructions

To avoid losing data when the server goes down, Santa Claus has decided to make incremental backups. A hacker called S4vitelf is helping him.

On the one hand, we have the timestamp of when the last backup was made.

We also have the changes that have been made to an array of arrays. Each internal array contains two elements: the id of the modified file and the timestamp of the modification.

You have to create a program that returns an array with the ids of the files that we would have to backup because they have been modified since the last backup and sorted in ascending order. Example:

```js
const lastBackup = 1546300800
const changes = [
  [ 3, 1546301100 ],
  [ 2, 1546300800 ],
  [ 1, 1546300800 ],
  [ 1, 1546300900 ],
  [ 1, 1546301000 ]
]

getFilesToBackup(lastBackup, changes) // => [ 1, 3 ]
// File with id 1 has been modified twice
// after the last backup.

// The file with id 2 has not been modified after the last backup.
// after the last backup.

// The file with id 3 has been modified once // after the last backup.
// after the last backup.

// We need to make a backup of files 1 and 3.
// of files 1 and 3.
```

To be taken into account

- Returns the id of the files that have been modified after the last backup.
- Returns an empty array if there are no files to backup.
- Remember that the ids must be sorted in ascending order.

## Solution

```js
function getFilesToBackup(lastBackup, changes) {
  
  return [...new Set(
    changes
      .filter(change => change[1] > lastBackup)
      .map(change => change[0])
  )].sort((a, b) => a - b)  
  
}
```
