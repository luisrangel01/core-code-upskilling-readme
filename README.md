# core-code-from-scratch-readme

## Ensure Question

DESCRIPTION:

Given a string, write a function that returns the string with a question mark ("?") appends to the end, unless the original string ends with a question mark, in which case, returns the original string.

For example (Input --> Output)

```
"Yes" --> "Yes?" 
"No?" --> "No?"
```

Solutions:

```
function ensureQuestion(s) {
  return s.charAt(s.length - 1) === '?' ? s : `${s}?`;
}
```

```
const ensureQuestion = (s) => s.charAt(s.length - 1) === '?' ? s : `${s}?`;
```

```
const ensureQuestion = (s) => s[s.length - 1] === '?' ? s : `${s}?`;
```

```
const ensureQuestion = (s) => s.endsWith('?') ? s : `${s}?`;
```

## Reversed Words

DESCRIPTION:

Complete the solution so that it reverses all of the words within the string passed in.

Example(Input --> Output):

"The greatest victory is that which requires no battle" --> "battle no requires which that is victory greatest The"

Solutions:

```
function reverseWords(str){
  return str.split(' ').reverse().join(' '); // reverse those words
}
```

```
const reverseWords = (str) => str.split(' ').reverse().join(' '); 
```


## Smallest Integer In Array

DESCRIPTION:

Given an array of integers your solution should find the smallest integer.

For example:

Given [34, 15, 88, 2] your solution will return 2
Given [34, -345, -1, 100] your solution will return -345
You can assume, for the purpose of this kata, that the supplied array will not be empty.

Solutions:

```
function findSmallestInt(args) {
  return Math.min(...args);
}
```

```
const findSmallestInt = (args) => Math.min(...args);
```
