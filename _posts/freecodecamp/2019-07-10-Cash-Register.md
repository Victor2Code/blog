---
layout: post
title: FreeCodeCamp - Cash Register
tags: freecodecamp
categories: front-end
comments: true
last-modified: 2019-07-10 16:47:00 +0800
---
FreeCodeCamp - JavaScript Algorithms and Data Structures Projects: Cash Register. This project is a great demonstration of IEEE 754 float point arithmetic issue.

## Floating Point Arithmetic
When in the middle of this project, I accidentally found out that the result of `96.73-60` is not `36.73` but `36.730000000000004`. What the hell? A bug of JS?

I did some search on Google, and [this website](https://floating-point-gui.de/) explained this issue thoroughly.
>Because internally, computers use a format (binary floating-point) that cannot accurately represent a number like 0.1, 0.2 or 0.3 at all.

Looks like computers can not handle fractions and decimals such as 1/3, 0.88, maybe the numbers you see on the monitor are identical to what you think they are, but inside memory, they are not stored as precisely as the original number. So when calculations apply, you many encounter various unexpected issues.

That is how PC works.
>It’s not stupid, just different.

>Computers use binary numbers because they’re faster at dealing with those, and because for most calculations, a tiny error in the 17th decimal place doesn’t matter at all since the numbers you work with aren’t round (or that precise) anyway.

And the website also provides us some solutions
> * If you really need your results to add up exactly, especially when you work with money: use a special decimal datatype.
> * If you just don’t want to see all those extra decimal places: simply format your result rounded to a fixed number of decimal places when displaying it.
> * **If you have no decimal datatype available, an alternative is to work with integers**, e.g. do money calculations entirely in cents. But this is more work and has some drawbacks.

I took the third option for this project.

## Approach
Back to this project, the approach is quite straight-forward.

Starting from highest order "ONE HUNDRED", take the change as dividend, and the  par value of the currency as divisor. The quotient times the par value would be the amount from this currency, and the remaining amount of the total change will go to next currency for same calculation. Recursions apply.

A logical judgement is needed to calculate the actual amount of a certain currency to contribute to the change based on the available balance of this currency.

Another logical judgement to distinguish between "OPEN", "CLOSED" and "INSUFFICIENT_FUNDS"

## Code
### Javascript
This snippet can pass freecodecamp tests on publication date of this blog.
```javascript
function checkCashRegister(price, cash, cid) {
  let change=cash-price;
  let database={"ONE HUNDRED":100,"TWENTY":20,"TEN":10,"FIVE":5,"ONE":1,"QUARTER":0.25,"DIME":0.1,"NICKEL":0.05,"PENNY":0.01};
  let result=[];
  let remain=0;
  // First logical block for recursion
  let func=function(money,base,balance){
    let num=Math.floor(money/database[base]);
    let newMoney=money;
    if(num*database[base]>=balance){
      newMoney=(money*1000-balance*1000)/1000;
      result.push([base,balance]);
    }else if(num*database[base]<balance && num!=0){
      newMoney=(money*1000-num*database[base]*1000)/1000;
      result.push([base,num*database[base]]);
      remain=(remain*1000+balance*1000-num*database[base]*1000)/1000;
    }else if(num==0){
      newMoney=money;
      remain=(remain*1000+balance*1000)/1000;
    }
    return newMoney;   
  }
  // recursion as below
  for(let i=8;i>=0;i--){
    change=func(change,cid[i][0],cid[i][1]);
  }
  // Second logical block
  if(change>0){
    return {"status":"INSUFFICIENT_FUNDS","change":[]};
  }else if(change==0 && remain==0){
    return {"status":"CLOSED","change":cid};
  }else if(change==0 && remain>0){
    return {"status":"OPEN","change":result};
  }
}
```


## Summary
Let me know in the comment section below if you think the code above can be improved, and any new approach are welcomed.
