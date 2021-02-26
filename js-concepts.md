# Functions type

## Currying

Function that returns other function

### example

```js
function sum(a) {
  return function (b) {
    return a + b;
  };
}

const sum2 = sum(2);

console.log(sum2(2));
console.log(sum2(3));
```

## Hoisting (Elevação)

Hoisting of scope block, function or global

Types: variables and functions

Variables hoisting only in its creation and doesn't in its assingment

Function can hoisting anywhere

### example

```js

```

function fn() {
console.log(text)

let text = 'my text'

log(text)

function log(variable) {
console.log(variable)
}
}

# Immutability

Don't change the value o the object or variable,
You need to create a new based it.

# Symbol

É um identificador unico
Criar propriedades privadas

## Well know symbols

iterator
split
toStringTag

```js
const obj = {
  values: [1, 2, 3, 4],
  [Symbol.iterator]() {
    let i = 0;
    return {
      next() {
        i++;
        return {
          value: this.values[i - 1],
          done: i > this.values.length,
        };
      },
    };
  },
};
const it = obj[Symbol.iterator]();

console.log(it.next());
```

# Generators

```js
function* hello() {
  console.log("Hello");
  yield 1;

  console.log("From");
  const value = yield 2;

  console.log("Function generator", value);
}

const it = hello();

console.log(it.next());
console.log(it.next());
console.log(it.next("Hello from the other side"));
```

```js
const obj = {
  values: [1, 2, 3, 4],
  *[Symbol.iterator]() {
    for (let i = 0; i < this.values.length; i++) {
      yield this.values[i];
    }
  },
};

for (let value of obj) {
  console.log(value);
}
```

# Promise

## Status

Peding
Fulfilled
Rejected
