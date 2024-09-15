---
title: "Decoding String Interview Questions: Set 1 - Basics"
seoTitle: "String Interview Questions: Basic Concepts"
seoDescription: "A guide to essential string interview questions including reversing strings, checking palindromes, and counting vowels. Key for coding interviews"
datePublished: Sun Sep 15 2024 03:36:49 GMT+0000 (Coordinated Universal Time)
cuid: cm130yowi00010alebw5eehme
slug: decoding-string-interview-questions-set-1-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1726371268040/19923433-00c8-4db6-9036-1685224a406e.png
tags: interview, javascript, string, coding-challenge, codingnewbies

---

A Guide to Common Basic String Challenges in Coding Interviews

### Introduction

In my previous blog, *"*[*JavaScript String Methods Explained: Practical Examples Tutorial*](https://hardikdhamija.hashnode.dev/javascript-string-methods-explained-practical-examples-tutorial)*,"* I covered essential string manipulation methods with practical examples. If you haven’t read it yet, I recommend checking it out to build a solid foundation for understanding string operations.

In this blog, we'll focus on basic and commonly asked interview questions about strings. These questions are crucial for coding interviews at any level. We’ll save intermediate and advanced questions for future discussions, so stay tuned for more challenging topics down the road. Let’s dive into these basic yet essential string problems!

### 1.Reverse String

The objective here is to reverse a given string.

For example, if we start with the string `"hello"`, our goal is to transform it into `"olleh"`.

1. **Using Built-in Methods:**
    
    It is very easy to do using built in methods.
    
    * **Split the String:** Use `split('')` to convert the string into an array of characters.
        
    * **Reverse the Array:** Apply the `reverse()` method to reverse the order of the characters in the array.
        
    * **Join the Array:** Use `join('')` to concatenate the characters back into a single string.
        

```javascript
function reverseString(str) {
    return str.split('').reverse().join('');
}

console.log(reverseString("hello")); // Output: "olleh"
```

2. **Without Built in function**
    
    If you’re asked to reverse a string without using JavaScript's built-in methods, you can achieve this by manually constructing a new string. The idea is to iterate through the original string from the last character to the first, appending each character to a new string.
    

```javascript
function reverseString(str) {
    let reversed = ''; // Initialize an empty string to store the reversed result
    for (let i = str.length - 1; i >= 0; i--) {
        reversed += str[i]; // Append each character from the end of the string
    }
    return reversed; // Return the reversed string
}

console.log(reverseString("hello")); // Output: "olleh"
```

### 2.Check Palindrome

Determine if the given string is the same backward as forward.

For example, `"abc"` is not a palindrome because its reverse is `"cba"`, is not `"abc"`.

However, `"aba"` is a palindrome because its reverse is also `"aba"`.

**Approach:**

* **Create reverse String:** Create a reversed version of the string.
    
* **Compare:** Check if the original string is the same as its reversed version.
    
* **Return Result:** If they are the same, return `true`; otherwise, return `false`.
    

```javascript
function isPalindrome(str) {
    // Create reverse string
    const reversedStr = str.split('').reverse().join('');
    // Compare original string with reversed string
    return str === reversedStr;
}

console.log(isPalindrome("aba")); // Output: true
console.log(isPalindrome("abc")); // Output: false
```

**Note:** If you are asked to solve this problem without using built-in functions, you can achieve the same result by manually creating the reversed string using a loop. After reversing the string, compare it with the original and return `true` or `false` based on the comparison.

### 3.Reverse Words in sentence

Objective is to reverse the order of words in sentence in string.

Example. `"I write code"` should be transformed to `"code write I"`.

**Approach:**

* **Split the Sentence:** Convert the sentence into an array of words by splitting it using spaces.
    
* **Reverse the Array:** Reverse the order of words in the array.
    
* **Join the Words:** Join the reversed array of words back into a single string with spaces.
    

```javascript
function reverseWords(sentence) {
    // Split the sentence into an array of words
    const wordsArray = sentence.split(' ');
    // Reverse the array of words
    const reversedArray = wordsArray.reverse();
    // Join the reversed array into a single string with spaces
    return reversedArray.join(' ');
}
console.log(reverseWords("I write code")); // Output: "code write I"
```

**Note:** The iterative approach to reversing words in a sentence is more complex, involving manual string traversal and array manipulation. We’ll cover this in future articles.

### 4.Reverse Each Word in String

Objective is to Reverse each word in the sentence while keeping the word order the same.

For example, `"Hello World"` should be transformed to `"olleH dlroW"`.

**Approach:**

* **Extract Words:** Split the sentence into an array of words by using spaces as separators.
    
* **Reverse Each Word:** Use `map()` to iterate over the array and apply reverse logic to each word by splitting, reversing, and joining the characters.
    
* **Reconstruct Sentence:** Join the array of reversed words back into a single string with spaces between the words.
    

```javascript
function reverseEachWord(sentence) {
    // Step 1: Split the sentence into an array of words using spaces as the delimiter
    let wordsArray = sentence.split(' ');
    // Step 2: Use map to reverse each word in the array
    let reversedWordsArray = wordsArray.map(word => 
        word.split('').reverse().join(''); // Split the word into characters, reverse them, and join back
    );
    // Step 3: Join the reversed words back into a single string with spaces
    let result = reversedWordsArray.join(' ');

    return result; // Return the final reversed sentence
}
console.log(reverseEachWord("Hello World")); // Output: "olleH dlroW"
```

### 5.Count number of Vowels in a String

Count how many vowels (a, e, i, o, u) are present in a given string.

For example, the string `"hEllo"` has 2 vowels: `'E'` and `'o'`.

**Approach:**

* Define a set of vowels (both lowercase and uppercase if needed).
    
* Iterate through each character of the string.
    
* For each character, check if it is a vowel.
    
* Keep a count of the vowels encountered.
    

```javascript
function countVowels(str) {
    const vowels = 'aeiouAEIOU'; // List of vowels
    let count = 0;
    for (let char of str) {
        if (vowels.includes(char)) {
            count++; // Increment the count if the character is a vowel
        }
    }
    return count; // Return the total number of vowels
}
console.log(countVowels("hello")); // Output: 2
console.log(countVowels("JavaScript")); // Output: 3
```

**Note:** To get the count of consonants, you can subtract the number of vowels from the total length of the string after removing spaces or special characters. For example:

```javascript
javascriptCopy codeconst consonantCount = str.length - countVowels(str);
```

This will give you the count of consonants in the string, assuming the string only contains letters and spaces are not counted.

### 6.Count the Frequency of Characters in a String

Create a frequency map of characters in a string, which counts how many times each character appears.

**Example:** For the string `"hello"`, the frequency map would be:

```javascript
{ h: 1, e: 1, l: 2, o: 1 }
```

**Approach:**

* **Initialize the Frequency Map:** Use an object to keep track of character counts.
    
* **Iterate Through the String:** For each character, update its count in the frequency map.
    
* **Return the Frequency Map:** Output the map that shows character frequencies.
    

```javascript
function createFrequencyMap(str) {
    const charCount = {}; // Initialize the frequency map

    // Iterate through each character in the string
    for (let char of str) {
        // Increment the count of the character in the map
        charCount[char] = (charCount[char] || 0) + 1;
    }
    return charCount; // Return the frequency map
}

// Example usage:
console.log(createFrequencyMap("hello")); // Output: { h: 1, e: 1, l: 2, o: 1 }
console.log(createFrequencyMap("banana")); // Output: { b: 1, a: 3, n: 2 }
```

**Note:** Creating a frequency map of characters is a useful utility function for various string operations. This function can be applied to:

* **Checking if two strings are anagrams.**
    
* **Finding the first non-repeating character.**
    
* **Counting character occurrences.**
    

By separating this functionality into its own utility function, you can efficiently use it across different problems that involve character counting. Let’s see its application in the next question.

### 7.Find the First Non-Repeating Character in a String

Identify the first character in a string that does not repeat.

For example, in the string `"swiss"`, the first non-repeating character is `"w"`.

**Approach:**

* **Frequency Map:** Create a frequency map (using an object or hash map) to count the occurrence of each character in the string.
    
* **Identify First Non-Repeating Character:** Iterate through the string and return the first character that has a count of 1 in the frequency map.
    

```javascript
function firstNonRepeatingChar(str) {
    const charCount = {}; // Frequency map to store the count of each character
    // Step 1: Count the frequency of each character
    for (let char of str) {
        if (charCount[char]) {
            // If the character already exists in the map, increment its count
           charCount[char] += 1;
    }   else {
            // If the character is not in the map, initialize its count to 1
            charCount[char] = 1;
            }
    }
    // Step 2: Find the first character with a count of 1
    for (let char of str) {
        if (charCount[char] === 1) {
            return char; // Return the first non-repeating character
        }
    }
    return null; // If no non-repeating character is found
}

console.log(firstNonRepeatingChar("swiss")); // Output: "w"
console.log(firstNonRepeatingChar("racecar")); // Output: "e"
```

### 8.Check if Two Strings are Anagrams

Determine if two given strings are anagrams of each other. An anagram means that both strings contain the same characters in the same frequency but in a different order.

For example, `"listen"` and `"silent"` are anagrams because both have the same characters: `'l', 'i', 's', 't', 'e', 'n'`.

**Approach: Use Frequency Map**

1. Create a frequency map (object) for both strings to count the occurrences of each character.
    
2. Compare the frequency maps. If they are identical, the strings are anagrams.
    

```javascript
function areAnagrams(str1, str2) {
    // Step 1: Check if the strings are of the same length
    // If the lengths are different, the strings cannot be anagrams of each other.
    if (str1.length !== str2.length) {
        return false;
    }

    // Step 2: Create a frequency map for characters in the first string
    const charCount = {};

    // Populate the frequency map with counts of each character in str1
    for (let char of str1) {
        charCount[char] = (charCount[char] || 0) + 1;
    }

    // Step 3: Process the second string
    // For each character in str2, check its frequency in the map
    for (let char of str2) {
        if (!charCount[char]) {
            // If the character is not found or has a count of 0, strings are not anagrams
            return false;
        }
        // Decrement the character count in the map
        charCount[char]--;
    }

    // If all characters match, the strings are anagrams
    return true;
}

console.log(areAnagrams("listen", "silent")); // Output: true
console.log(areAnagrams("hello", "world"));   // Output: false
```

### Conclusion

In this blog, we've explored fundamental string manipulation techniques commonly encountered in interviews. We followed a clear pattern: first, we broke down each problem into simple steps and applied both built-in methods and manual solutions to cover different approaches.

Here’s a quick recap of the topics we covered:

* **Reversing Strings and Words:** Both using built-in methods and manual techniques.
    
* **Palindrome Check:** Comparing a string with its reversed version.
    
* **Word and Character Reversal:** Reversing each word in a sentence and reversing characters within each word.
    
* **Vowel Counting and Frequency Maps:** Counting vowels and creating frequency maps to solve various problems.
    
* **Finding Non-Repeating Characters and Anagram Checking:** Using frequency maps to solve these common string problems.
    

To further deepen your understanding and practice these concepts, consider exploring the following questions:

* **Count the Number of Consonants in a String:** Given a string, count the number of consonants present.
    
* **Remove All Duplicate Characters:** Remove all duplicate characters from a string, leaving only the first occurrence of each character.
    
* **Find the Last Non-Repeating Character:** Identify the last character in a string that does not repeat.
    
* **Reverse Words in a Sentence While Keeping Each Word Intact:** Reverse the order of words in a sentence, but keep the characters within each word in their original order.
    
* **Check if Two Strings are Palindromes of Each Other:** Determine if two given strings are palindromes of each other (i.e., one is the reverse of the other).
    

These questions will help reinforce and expand upon the concepts we've covered, deepening your understanding and preparation for coding challenges. See you in the next blog!