# Closures

A closure is a combination of a function and its surrounding lexical environment (its scope)

Closures allow functions to retain access to variables from their present scope even after the parent function has finished executing.


```js
function outerFunction() {
  let outerVariable = 'I am from the outer function';

  function innerFunction() {
    console.log(outerVariable);
  }

  return innerFunction;
}

const closureExample = outerFunction();
closureExample(); // Outputs: I am from the outer function
```

`innerFunction` still has access to outerVariable even though `outerFunction` has finished executing. This is because of the closure created when `closureExample` is assigned the return value of `outerFunction`.


Some practical use cases of closures include:
- __Data Privacy__: Encapsulating variables to prevent direct access.
- __Callbacks__: Retaining context in asynchronous operations.
- __Module Pattern__: Creating private and public methods in an object.

Example with a variable in the outer function that stays available to the inner function, even after the outer function has finishing running:

```js
function counter() {
  let count = 0;

  return function() {
    return ++count;
  };
}

const increment = counter();
console.log(increment()); // Outputs: 1
console.log(increment()); // Outputs: 2
console.log(increment()); // Outputs: 3
```


For this next example let's use a repl. Open a terminal and run the `node` command to open a repl.

Next let's paste this function into the repl:
```js
function createSecretNumber() {
  const secret = Math.floor(Math.random() * 10);

  function checkGuess(guess) {
    if (guess === secret) {
      return `You've guessed the secret number: ${secret}!`;
    } else {
      return 'Try again! The secret number is not correct.';
    }
  }

  return checkGuess; // Return the inner function to maintain access to the secret
}

const guessSecret = createSecretNumber();

console.log(guessSecret(3)); // Outputs: "Try again! The secret number is not correct."
console.log(guessSecret(7)); // Outputs: "You've guessed the secret number: 7!"
```


- The createSecretNumber function generates a random secret number and returns an inner function checkGuess.
- The checkGuess function takes a guess parameter and checks if it matches the secret number.
- Since checkGuess is returned from createSecretNumber, it forms a closure over the secret variable, allowing it to access and compare against the secret number each time it's called.

Now let's create another variable called `otherSecretNumber` and initialize it to be the output of another `createSecretNumber` invocation.

The value saved to each of the variables could be the same, but are they always? Why or why not?


### Exercise:
```js
for(var i = 0; i < 3; i++){
    const log = () => {
        console.log(i)
    }

    setTimeout(log, 1000)
}
```

- What do you expect the output to be?
- Why is the output what it is?
- How could you get a different output?