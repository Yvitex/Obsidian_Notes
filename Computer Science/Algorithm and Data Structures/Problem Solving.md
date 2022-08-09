# Problem
Tips and tricks to solve programming problems using [[Algorithm]]s. This is the best way to approach an interview. 

- When the interviewer says the question, write down the key points at the top (i.e. sorted array). Make sure you have all the details. Show how organized you are.

This is an example of what you may want to write. Ask questions to the interviewer for some things that you may don't understand.
```js
// Given 2 arrays, create a function that let's a user know (true/false) whether these two arrays contain any common items
```

- Make sure you double check: What are the inputs? What are the outputs?

Here is an example of it. Speak your thoughts out loud to how you might want to approach this problem. Here we could confirm if all items in an array could be objects or other data types. Or would it always be an array or an object or a string.
```js
//For Example:
//const array1 = ['a', 'b', 'c', 'x'];//const array2 = ['z', 'y', 'i'];
//should return false.
//-----------
//const array1 = ['a', 'b', 'c', 'x'];//const array2 = ['z', 'y', 'x'];
//should return true.

// 2 parameters - arrays
// return true or false
```

- What is the most important value of the problem? Do you have time, and space and memory, etc.. What is the main goal?

We ask questions to the interviewer weather if for example, an array of input would be in a fixed size. If yes, then we don;t need to think about any [[Algorithm]]. But if the interviewer said that the program should be adhere to [[Scalability]], the items could grow very large and we want the most efficient function available, then you may start to think. 

Write it down
```js
// 2 parameters - arrays - no size limit
// return true or false
```

- Don't be annoying and ask too many questions. They are humans not robots.

- Start with the naive/brute force approach. First thing that comes into mind. It shows that you’re able to think well and critically (you don't need to write this code, just speak about it).

Yep, brute force has [[Quadratic Time]] complexity of O(a * b). A nested loop meant to compare each items  to one another. This is not the most optimal solution so you may not want to code it but yeah. Just to show that you could think of it and you are aware of it.
```js
function containsCommonItem(arr1, arr2) {
  for (let i=0; i < arr1.length; i++) {
    for ( let j=0; j < arr2.length; j++) {
      if(arr1[i] === arr2[j]) {
        return true;
      }
    }
  }
  return false
}
```

- Tell them why this approach is not the best (i.e. O(n^2) or higher, not readable, etc...)

Spell your thoughts outloud, if required, speak in english

- Walk through your approach, comment things and see where you may be able to break things. Any repetition, bottlenecks like O(N^2), or unnecessary work? Did you use all the information the interviewer gave you? Bottleneck is the part of the code with the biggest Big O. Focus on that. Sometimes this occurs with repeated work as well

The same as before, explain the bottlneck, break the solutions into separate function if needed. 

- Before you start coding, walk through your code and write down the steps you are going to follow

This is a critical step as we are showing the interviewer how we think, which in this case, even if we create a wrong solution, the process or the steps we took solving those will reflect our thought process.  Here is an example where we write the steps we are trying to take.
![[Pasted image 20220801045125.png]]

- Modularize your code from the very beginning. Break up your code into beautiful small pieces and add just comments if you need to

Yes modularize!!

- Start actually writing your code now. Keep in mind that the more you prepare and understand what you need to code, the better the whiteboard will go. So never start a whiteboard interview not being sure of how things are going to work out. That is a recipe for disaster. Keep in mind: A lot of interviews ask questions that you won’t be able to fully answer on time. So think: What can I show in order to show that I can do this and I am better than other coders. Break things up in Functions (if you can’t remember a method, just make up a function and you will at least have it there. Write something, and start with the easy part.

Best tip for buying some time before coding. So that's how it is. 
```js
function containsCommonItem2(arr1, arr2) {
  // loop through first array and create object where properties === items in the array
  // can we assume always 2 params?

  let map = {};
  for (let i=0; i < arr1.length; i++) {
    if(!map[arr1[i]]) {
      const item = arr1[i];
      map[item] = true;
    }
  }
  // loop through second array and check if item in second array exists on created object. 
  for (let j=0; j < arr2.length; j++) {
    if (map[arr2[j]]) {
      return true;
    }
  }
  return false
}
```

```ad-Danger
collapse: open
The function is not modularized, make it modularized and separate the loops into individual functions!!!
```

- Think about error checks and how you can break this code. Never make assumptions about the input. Assume people are trying to break your code and that Darth Vader is using your function. How will you safeguard it? Always check for false inputs that you don’t want. Here is a trick: Comment in the code, the checks that you want to do… write the function, then tell the interviewer that you would write tests now to make your function fail (but you won't need to actually write the tests).

Errors may arise, so we need to think about the ways we may break our code and give a solution to it as soon as possible, we don;t neeed to code it, just explain it like what if we don't have a second parameter, what if some of the values are not strings but integers, what if there is a null value. Make try and catch exception or an if else statement that will check for the arguments. 

- Don’t use bad/confusing names like i and j. Write code that reads well.

Except for for loops, maybe but still try to make it more meaningful and let the interviewer knows that you are thinking about it.

- Test your code: Check for no params, 0, undefined, null, massive arrays, async code, etc… Ask the interviewer if we can make assumption about the code. Can you make the answer return an error? Poke holes into your solution. Are you repeating yourself?

Like we will run a unit test. OR if else statement

- Finally talk to the interviewer where you would improve the code. Does it work? Are there different approaches? Is it readable? What would you google to improve? How can performance be improved? Possibly: Ask the interviewer what was the most interesting solution you have seen to this problem

What will you research? Some new methods in specific language that improves the readability of the code without making it slower? Yes, there is a lot to improve that is yet to be known by us and let the interviewer knows that we are willing to learn.

```js
function containsCommonItem3(arr1, arr2) {
  return arr1.some(item => arr2.includes(item))
}
```

- If your interviewer is happy with the solution, the interview usually ends here. It is also common that the interviewer asks you extension questions, such as how you would handle the problem if the whole input is too large to fit into memory, or if the input arrives as a stream. This is a common follow-up question at Google, where they care a lot about scale. The answer is usually a divide-and-conquer approach — perform distributed processing of the data and only read certain chunks of the input from disk into memory, write the output back to disk and combine them later.

What we could do, well explain that our first solution, the brute force is better because it have a [[Space Complexity]] of O(1) and the second solution event though it is fast, it is still dull when it comes to memory with a [[Space Complexity]] of O(n)


![[4.2 cheatsheet.pdf.pdf]]

<iframe width="560" height="315" src="https://www.youtube.com/embed/XKu_SEDAykw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>




