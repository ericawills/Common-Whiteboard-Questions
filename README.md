# Common Whiteboard Questions

## Palindrome
> A palindrome is a word, sentence or other type of character sequence which reads the same backward as forward. For example, “racecar” and “Anna” are palindromes. “Table” and “John” aren’t palindromes, because they don’t read the same from left to right and from right to left.

* This challenge revolves around the idea of reversing a string. 

###### Solution
Here’s one way you can solve the palindrome challenge:
```javascript
const palindrome = str => {
  // turn the string to lowercase
  str = str.toLowerCase()
  // reverse input string and return the result of the
  // comparisong
  return str === str.split('').reverse().join('')
}
```
* Start by turning your input string into lower case letters. Since you know you’re going to compare each character in this string to each corresponding character in the reversed string, having all the characters either in lower or upper case will ensure the comparison will leave out this aspect of the characters and just focus on the characters themselves.

* Next, reverse the input string. You can do so by turning the string into an array using the String’s .split() method, then applying the Array’s .reverse() method and finally turning the reversed array back into a string with the Array’s .join() method. I’ve chained all these methods above so the code looks cleaner.

* Finally, compare the reversed string with the original input and return the result — which will be true or false according to whether the two are exactly the same or not.

## FizzBuzz

The FizzBuzz challenge goes something like this. Write a function that does the following:

console logs the numbers from 1 to n, where n is the integer the function takes as its parameter
logs fizz instead of the number for multiples of 3
logs buzz instead of the number for multiples of 5
logs fizzbuzz for numbers that are multiples of both 3 and 5

> Example:
> fizzBuzz(5)
> Result:
> // 1
> // 2
> // fizz
> // 4
> // buzz
Reasoning about the challenge
One important point about FizzBuzz relates to how you can find multiples of a number in JavaScript. You do this using the modulo or remainder operator, which looks like this: %. This operator returns the remainder after a division between two numbers. A remainder of 0 indicates that the first number is a multiple of the second number:
```javascript
 12 % 5 // 2 -> 12 is not a multiple of 5
 12 % 3 // 0 -> 12 is multiple of 3
 ```
> If you divide 12 by 5, the result is 2 with a remainder of 2. If you divide 12 by 3, the result is 4 with a remainder of 0. In the first example, 12 is not a multiple of 5, while in the second example, 12 is a multiple of 3.

###### Solution

```javascript

const fizzBuzz = num => {
  for(let i = 1; i <= num; i++) {
    // check if the number is a multiple of 3 and 5
    if(i % 3 === 0 && i % 5 === 0) {
      console.log('fizzbuzz')
    } // check if the number is a multiple of 3
      else if(i % 3 === 0) {
      console.log('fizz')
    } // check if the number is a multiple of 5
      else if(i % 5 === 0) {
      console.log('buzz')
    } else {
      console.log(i)
    }
  }
}
```
The function above simply makes the required tests using conditional statements and logs out the expected output. What you need to pay attention to in this challenge is the order of the if … else statements. Start with the double condition first (&&) and end with the case where no multiples are found. This way, you’ll be able to cover all bases.

## Anagram

> A word is an anagram of another word if both use the same letters in the same quantity, but arranged differently.

Understanding the challenge
* write a function that checks if two provided strings are anagrams of each other; 
* letter casing shouldn’t matter 
* consider only characters, not spaces or punctuation. 

###### Solution

```javascript

const buildCharObject = str => {
  const charObj = {}
  for(let char of str.replace(/[^\w]/g).toLowerCase()) {
    // if the object has already a key value pair
    // equal to the value being looped over,
    // increase the value by 1, otherwise add
    // the letter being looped over as key and 1 as its value
    charObj[char] = charObj[char] + 1 || 1
  }
  return charObj
}

// main function
const anagram = (strA, strB) => {
  // build the object that holds strA data
  const aCharObject = buildCharObject(strA)
  // build the object that holds strB data
  const bCharObject = buildCharObject(strB)

  // compare number of keys in the two objects
  // (anagrams must have the same number of letters)
  if(Object.keys(aCharObject).length !== Object.keys(bCharObject).length) {
    return false
  }
  // if both objects have the same number of keys
  // we can be sure that at least both strings
  // have the same number of characters
  // Now we can compare the two objects to see if both
  // have the same letters in the same amount
  for(let char in aCharObject) {
    if(aCharObject[char] !== bCharObject[char]) {
      return false
    }
  }
  // if both the above checks succeed,
  // you have an anagram: return true
  return true
}
```
