---
tags:
  - note
  - programming
language: JavaScript
---
# `= this.file.name`
---

`````ad-code
title: 5-es6-objects.js

```js
/* Object property shorthand */

const name = "Kyle";
const userAge = 26;

// const user = {
//   name: name,
//   age: userAge,
//   location: "Winnipeg",
// };

const user = {
  name,
  age: userAge,
  location: "Winnipeg",
};

console.log(user.name);

/* Object destructuring */
/* 1. Destructuring */
/* 2. Renaming */
/* 3. Default Values */
/* 4. Function Parameters */

const product = {
  label: undefined,
  price: 3,
  stock: 201,
  salePrice: undefined,
};

// 1.
// const { label, price, stock } = product;

// console.log(label);

// 2.
// const { label: productLabel, price, stock } = product;

// console.log(productLabel);

// 3.
// const { label: productLabel = "Item", price, stock } = product;

// console.log(productLabel);

// 4.
// const transaction = (type, product) => {
//   console.log(type, price, stock);
// };

const transaction = (type, { price, stock }) => {
  console.log(type, price, stock);
};

transaction("order", product);

```
`````

---
Created: February 26, 2024
Last Modified: `= this.file.mtime`
