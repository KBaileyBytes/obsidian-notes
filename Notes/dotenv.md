---
tags:
  - note
---
# `= this.file.name `
---

## 🌱 Install

```shell
# install locally (recommended)
npm install dotenv --save
```

Create a `.env` file in the root of your project:

```ini
S3_BUCKET="YOURS3BUCKET"
SECRET_KEY="YOURSECRETKEYGOESHERE"
```

As early as possible in your application, import and configure dotenv:

```js
require('dotenv').config()
console.log(process.env) // remove this after you've confirmed it is working
```

.. [or using ES6?](https://www.npmjs.com/package/dotenv#how-do-i-use-dotenv-with-import)

```js
import 'dotenv/config'
```

That's it. `process.env` now has the keys and values you defined in your `.env` file:

```js
require('dotenv').config()

...

s3.getBucketCors({Bucket: process.env.S3_BUCKET}, function(err, data) {})
```




---
Created: November 26, 2024
Last Modified: `= this.file.mtime`
