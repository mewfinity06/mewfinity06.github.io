# Vibe Coding... Our Downfall

Now let me be honest... I use AI. Almost every day I am using Gemini or ChatGPT because it is genuinely useful, especially for mundane and boring tasks, because no one wants to write boring or mundane tasts. (I am human!).

But here is our mistake: Letting LLMs take over. And not just as a code integrety issue, but it actively replaces what captivated me, like many other devs, to programming: **The Joy of Programming**.

For me, I find problem solving the crux of the issue. *How am I going to write this peice of code?* or *Is this the most effective way to do problem X with data Y?* There is no point to programming if we are not figuring out what is going on! In the (very much paraphrased) words of ThePrimeagen, "How did we go from a context-free grammar to a context-based grammar?"

Take the prompt: `Write a TypeScript function that calculates the sum of all numbers within a potentially nested array. The function should handle arrays with arbitrary levels of nesting`.

***Using Gemini 2.0 Flash***

Run 1:

```ts
function sumNestedArray(inputArray: unknown[]): number {
  let totalSum = 0;

  for (const element of inputArray) {
    if (Array.isArray(element)) {
      totalSum += sumNestedArray(element);
    } else if (typeof element === 'number') {
      totalSum += element;
    }
  }

  return totalSum;
}
```

Run 2:

```ts
function sumNestedArray(arr: any[]): number {
  let result = 0;

  arr.forEach(item => {
    if (Array.isArray(item)) {
      result += sumNestedArray(item);
    } else if (typeof item === 'number') {
      result += item;
    }
  });

  return result;
}
```

Run 3:

```ts
type NestedNumberArray = number | NestedNumberArray[];

function sumNestedArray(array: NestedNumberArray): number {
  let sum = 0;
  for (let i = 0; i < array.length; i++) {
    const value = array[i];
    if (Array.isArray(value)) {
      sum += sumNestedArray(value);
    } else if (typeof value === 'number') {
      sum += value;
    }
  }
  return sum;
}
```

The point of code is to know that there KNOWN outputs for KNOWN inputs, and LLMs fail at one of these. There is nothing in LLMs that say `Input A` give `Output B`. And this is *bad*, like really bad.
