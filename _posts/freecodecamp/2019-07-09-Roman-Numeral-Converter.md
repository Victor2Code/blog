---
layout: post
title: FreeCodeCamp - Roman Numeral Converter
tags: freecodecamp
categories: front-end
comments: true
last-modified: 2019-07-09 12:47:00 +0800
---
FreeCodeCamp - JavaScript Algorithms and Data Structures Projects: Roman Numeral Converter. Only decimal numbers less than 4000 will be considered in this blog for simplicity.

## Roman Numerals
Based on [Wolfram MathWorld](http://mathworld.wolfram.com/RomanNumerals.html), Roman numerals are an additive system.
>They are an additive (and subtractive) system in which letters are used to denote certain "base" numbers, and arbitrary numbers are then denoted using combinations of symbols. For example, the number 1732 would be denoted MDCCXXXII in Roman numerals.

>|character|numerical value
>|:---:|:---:|
>|I|1|
>|V|5|
>|X|10|
>|L|50|
>|C|100|
>|D|500|
>|M|1000|

So we can divide a decimal number by a base, the quotient will be the quantity needed for the symbol of the base number. And the remainder will be the new dividend for next base. From left to right, from high order to low order.

But some special rules apply when it comes to 4 and 9,
>However, Roman numerals are not a purely additive number system. In particular, instead of using four symbols to represent a 4, 40, 9, 90, etc. (i.e., IIII, XXXX, VIIII, LXXXX, etc.), such numbers are instead denoted by preceding the symbol for 5, 50, 10, 100, etc., with a symbol indicating subtraction.

which means we need to consider various situations for the dividends.

## Approach
Based on analysis above, the main approach consists of 2 parts

* A function which takes 2 arguments, one is the dividend decimal number, and the other is the base. This function will **return the new dividend** for **recursion** purpose. The bases are `[1000,100,10,1]`

* A logical judgement to calculate the new dividend for next recursion. 4 ranges are needed:

  * `0.9*base <= remainder < base`
  * `0.5*base <= remainder < 0.9*base`
  * `0.4*base <= remainder < 0.5*base`
  * `remainder < 0.4*base`

## Code
### Javascript
This snippet can pass freecodecamp tests on publication date of this blog.
```javascript
function convertToRoman(num) {
 let data={1000:["M","D","C"],100:["C","L","X"],10:["X","V","I"],1:["I","",""]};
 let result="";
 let newRem;
 let func=function calc(n,base){
     let quo=Math.floor(n/base);
     let rem=n%base;
     if(quo>0){
         for(let i=0;i<quo;i++){
             result=result.concat(data[base][0]);
         }
     }
     if(rem>=0.9*base){
         result=result.concat(data[base][2]+data[base][0]);
         newRem=rem-0.9*base;
     }else if(rem<0.9*base && rem>=0.5*base){
         result=result.concat(data[base][1]);
         newRem=rem-0.5*base;
     }else if(rem<0.5*base && rem>=0.4*base){
         result=result.concat(data[base][2]+data[base][1]);
         newRem=rem-0.4*base;
     }else{
         newRem=rem;
     }
     return newRem;
 }
 func(func(func(func(num,1000),100),10),1);
 return result;
}
```


## Summary
Let me know in the comment section below if you think the code above can be improved, and any new approach are welcomed.
