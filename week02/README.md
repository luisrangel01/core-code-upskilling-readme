# Week 2

## Palindrome strings

DESCRIPTION:

A palindrome is a word, phrase, number, or other sequence of characters which reads the same backward or forward. This includes capital letters, punctuation, and word dividers.

Implement a function that checks if something is a palindrome. If the input is a number, convert it to string first.

Examples(Input ==> Output)

``` bash
"anna"   ==> true
"walter" ==> false
12321    ==> true
123456   ==> false
```

Solutions:

``` javascript
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

``` javascript
function isPalindrome(line) {
  const base = String(line);
  for (let index = 0; index < base.length / 2; index++) {
    if (base[index] !== base[base.length - 1 - index]) {
      return false;
    }
  }
  return true;
}
```

``` javascript
function isPalindrome(line) {
  return (String(line) == String(line).split('').reverse().join('')); 
}
```

## Well of Ideas - Easy Version

DESCRIPTION:

For every good kata idea there seem to be quite a few bad ones!

In this kata you need to check the provided array (x) for good ideas 'good' and bad ideas 'bad'. If there are one or two good ideas, return 'Publish!', if there are more than 2 return 'I smell a series!'. If there are no good ideas, as is often the case, return 'Fail!'.

Solutions:

``` javascript
function well(x){
  const count = x.filter((element) => element === 'good').length;
  return count > 2 ? 'I smell a series!' : count === 0 ? 'Fail!' : 'Publish!';
}
```


``` javascript
function well(x) {
  switch (x.filter(i => i === 'good').length) {
    case 0:
      return 'Fail!'
    case 1:
    case 2:
      return 'Publish!'
    default:
      return 'I smell a series!'
  }
}
```