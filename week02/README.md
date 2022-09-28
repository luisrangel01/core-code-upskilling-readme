# Week 2

## Palindrome strings

DESCRIPTION:

A palindrome is a word, phrase, number, or other sequence of characters which reads the same backward or forward. This includes capital letters, punctuation, and word dividers.

Implement a function that checks if something is a palindrome. If the input is a number, convert it to string first.

Examples(Input ==> Output)

```
"anna"   ==> true
"walter" ==> false
12321    ==> true
123456   ==> false
```

Solutions:

```
function isPalindrome(line) {
  let result = true;
  const base = String(line);
  for (let index = 0;index < base.length/2;index++){
    if (base[index] !== base[(base.length - 1) - index]) {
      result = false;
      break;
    }
  }
  return result;
}
```

```
function isPalindrome(line) {
  const base = String(line);
  for (let index = 0;index < base.length/2;index++){
    if (base[index] !== base[(base.length - 1) - index]) {
      return false;
    }
  }
  return true;
}
```