---
title: ECMAScript6
date: 2019-06-20 10:58:36
categories:
- [Java Script]
tags:
- js
- java script
---

# What is ECMAScript?

ECMAScript（或ES）是由Ecma International(前身为欧洲计算机制造商协会) 在 ECMA-262 和 ISO/IEC 16262 中标准化的脚本语言规范。它是为了标准化JavaScript而创建的，以便促进多个独立的实现。自标准首次发布以来，JavaScript一直是ECMAScript最着名的实现，其他知名实现包括JScript和ActionScript。 ECMAScript通常用于万维网上的客户端脚本，它越来越多地用于使用Node.js编写服务器应用程序和服务。

ECMAScript 和 JavaScript 的关系是，前者是后者的规格，后者是前者的一种实现（另外的 ECMAScript 方言还有 JScript 和 ActionScript）。

# What is ECMAScript 6?

ECMAScript第6版，最初称为ECMAScript 6（ES6），后来更名为ECMAScript 2015，于2015年6月完成。此更新为编写复杂应用程序添加了重要的新语法，包括类声明( `class Foo { ... }` )*，ES6的模块`import * as moduleName from "..."; export const Foo`，但在语义上用与ECMAScript 5严格模式相同的术语定义它们。其它新功能包括iterators 和 for/of loops，Python风格的generator，**箭头函数表达式( `()=>{ ... }` )**，**let**关键字为局部声明，关键字为**const**的常量声明，二进制数据类型数组，新的集合（maps，sets和WeakMap）， promise, 数字和数学增强，反射，代理（虚拟对象和wrappers的元编程）和字符串的模板文字。完整的清单很广泛。作为第一个“ECMAScript Harmony”规范，它也被称为“ES6 Harmony”。

# What is Babel?

[Babel](https://babeljs.io/) 是一个广泛使用的 ES6 转码器，可以将 ES6 代码转为 ES5 代码，从而在现有环境执行。这意味着，你可以用 ES6 的方式编写程序，又不用担心现有环境是否支持。下面是一个例子。

```
// 转码前
input.map(item => item + 1);

// 转码后
input.map(function (item) {
  return item + 1;
});
```

上面的原始代码用了箭头函数，Babel 将其转为普通函数，就能在不支持箭头函数的 JavaScript 环境执行了。

下面的命令在项目目录中，安装 Babel。

`npm install --save-dev @babel/core`

## 配置文件.babelrc

Babel 的配置文件是.babelrc，存放在项目的根目录下。使用 Babel 的第一步，就是配置这个文件。

该文件用来设置转码规则和插件，基本格式如下。

```
{
  "presets": [],
  "plugins": []
}
```

presets字段设定转码规则，官方提供以下的规则集，你可以根据需要安装。

```
# 最新转码规则
$ npm install --save-dev @babel/preset-env

# react 转码规则
$ npm install --save-dev @babel/preset-react
```

然后，将这些规则加入.babelrc。

```
  {
    "presets": [
      "@babel/env",
      "@babel/preset-react"
    ],
    "plugins": []
  }
```

## 命令行转码

Babel 提供命令行工具@babel/cli，用于命令行转码。

安装命令 `npm install --save-dev @babel/cli`

基本用法

```
# 转码结果输出到标准输出
$ npx babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ npx babel example.js --out-file compiled.js
# 或者
$ npx babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ npx babel src --out-dir lib
# 或者
$ npx babel src -d lib

# -s 参数生成source map文件
$ npx babel src -d lib -s
```

## babel-node

@babel/node模块的babel-node命令，提供一个支持 ES6 的 REPL 环境。它支持 Node 的 REPL 环境的所有功能，而且可以直接运行 ES6 代码。

安装命令 `npm install --save-dev @babel/node`

基本用法

```
$ npx babel-node
> (x => x * 2)(1)
2

# es6.js 的代码
# console.log((x => x * 2)(1));
$ npx babel-node es6.js
2
```

## babel/register

@babel/register模块改写require命令，为它加上一个钩子。此后，每当使用require加载.js、.jsx、.es和.es6后缀名的文件，就会先用 Babel 进行转码。

安装命令 `npm install --save-dev @babel/register`

基本用法

```
//使用时，必须首先加载@babel/register。
// index.js
require('@babel/register');
require('./es6.js');

//然后，就不需要手动对index.js转码了。
$ node index.js
2
```

需要注意的是，@babel/register只会对require命令加载的文件转码，而不会对当前文件转码。另外，由于它是实时转码，所以只适合在开发环境使用。

## babel API

如果某些代码需要调用 Babel 的 API 进行转码，就要使用@babel/core模块。

```
var babel = require('@babel/core');

// 字符串转码
babel.transform('code();', options);
// => { code, map, ast }

// 文件转码（异步）
babel.transformFile('filename.js', options, function(err, result) {
  result; // => { code, map, ast }
});

// 文件转码（同步）
babel.transformFileSync('filename.js', options);
// => { code, map, ast }

// Babel AST转码
babel.transformFromAst(ast, code, options);
// => { code, map, ast }
```

配置对象options，可以参看官方文档http://babeljs.io/docs/usage/options/。

```
var es6Code = 'let x = n => n + 1';
var es5Code = require('@babel/core')
  .transform(es6Code, {
    presets: ['@babel/env']
  })
  .code;

console.log(es5Code);
// '"use strict";\n\nvar x = function x(n) {\n  return n + 1;\n};'
```

上面代码中，transform方法的第一个参数是一个字符串，表示需要被转换的 ES6 代码，第二个参数是转换的配置对象。

## @babel/polyfill

Babel 默认只转换新的 JavaScript 句法（syntax），而不转换新的 API，比如Iterator、Generator、Set、Map、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码。

举例来说，ES6 在Array对象上新增了Array.from方法。Babel 就不会转码这个方法。如果想让这个方法运行，必须使用babel-polyfill，为当前环境提供一个垫片。

安装命令 `npm install --save-dev @babel/polyfill`

然后，在脚本头部，加入如下一行代码。

```
import '@babel/polyfill';
// 或者
require('@babel/polyfill');
```

Babel 默认不转码的 API 非常多，详细清单可以查看babel-plugin-transform-runtime模块的[definitions.js](https://github.com/babel/babel/blob/master/packages/babel-plugin-transform-runtime/src/runtime-corejs3-definitions.js)文件。

## 浏览器环境

Babel 也可以用于浏览器环境，使用@babel/standalone模块提供的浏览器版本，将其插入网页。

```
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<script type="text/babel">
// Your ES6 code
</script>
```

注意，网页实时将 ES6 代码转为 ES5，对性能会有影响。生产环境需要加载已经转码完成的脚本。

Babel 提供一个 [REPL 在线编译器](https://babeljs.io/repl/)，可以在线将 ES6 代码转为 ES5 代码。转换后的代码，可以直接作为 ES5 代码插入网页运行。

# Traceur 转码器

Google 公司的 [Traceur转码器](https://github.com/google/traceur-compiler)，也可以将 ES6 代码转为 ES5 代码。

# Promises

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了Promise对象。

所谓 `Promise`，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

`Promise` 对象有以下两个特点。

1. 对象的状态不受外界影响。Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。
2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果。Promise对象的状态改变，只有两种可能：从pending变为fulfilled和从pending变为rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise对象提供统一的接口，使得控制异步操作更加容易。

Promise也有一些缺点。首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。第三，当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

如果某些事件不断地反复发生，一般来说，使用 [Stream](https://nodejs.org/api/stream.html) 模式是比部署Promise更好的选择。

## 基本用法

ES6 规定，`Promise` 对象是一个构造函数，用来生成`Promise`实例。

```
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

`Promise` 构造函数接受一个函数作为参数，该函数的两个参数分别是 `resolve` 和 `reject` 。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。

`resolve` 函数的作用是，将 `Promise` 对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；`reject` 函数的作用是，将 `Promise` 对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

`Promise` 实例生成以后，可以用`then`方法分别指定`resolved`状态和`rejected`状态的回调函数。

```
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```

`then` 方法可以接受两个回调函数作为参数。第一个回调函数是Promise对象的状态变为resolved时调用，第二个回调函数是Promise对象的状态变为rejected时调用。其中，第二个函数是可选的，不一定要提供。这两个函数都接受Promise对象传出的值作为参数。

一个Promise对象的简单例子。

```
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}

timeout(100).then((value) => {
  console.log(value);
});
```

上面代码中，timeout方法返回一个Promise实例，表示一段时间以后才会发生的结果。过了指定的时间（ms参数）以后，Promise实例的状态变为resolved，就会触发then方法绑定的回调函数。

Promise 新建后就会立即执行。

```
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// resolved
```

上面代码中，Promise 新建后立即执行，所以首先输出的是Promise。然后，then方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以resolved最后输出。

下面是一个异步加载图片的例子

```
function loadImageAsync(url) {
  return new Promise(function(resolve, reject) {
    const image = new Image();

    image.onload = function() {
      resolve(image);
    };

    image.onerror = function() {
      reject(new Error('Could not load image at ' + url));
    };

    image.src = url;
  });
}
```

上面代码中，使用Promise包装了一个图片加载的异步操作。如果加载成功，就调用resolve方法，否则就调用reject方法。

下面是一个用Promise对象实现的 Ajax 操作的例子

```
const getJSON = function(url) {
  const promise = new Promise(function(resolve, reject){
    const handler = function() {
      if (this.readyState !== 4) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
    const client = new XMLHttpRequest();
    client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json";
    client.setRequestHeader("Accept", "application/json");
    client.send();

  });

  return promise;
};

getJSON("/posts.json").then(function(json) {
  console.log('Contents: ' + json);
}, function(error) {
  console.error('出错了', error);
});
```

上面代码中，getJSON是对 XMLHttpRequest 对象的封装，用于发出一个针对 JSON 数据的 HTTP 请求，并且返回一个Promise对象。需要注意的是，在getJSON内部，resolve函数和reject函数调用时，都带有参数。


如果调用resolve函数和reject函数时带有参数，那么它们的参数会被传递给回调函数。reject函数的参数通常是Error对象的实例，表示抛出的错误；resolve函数的参数除了正常的值以外，还可能是另一个 Promise 实例，比如像下面这样。

```
const p1 = new Promise(function (resolve, reject) {
  // ...
});

const p2 = new Promise(function (resolve, reject) {
  // ...
  resolve(p1);
})
```

上面代码中，p1和p2都是 Promise 的实例，但是p2的resolve方法将p1作为参数，即一个异步操作的结果是返回另一个异步操作。

注意，这时p1的状态就会传递给p2，也就是说，p1的状态决定了p2的状态。如果p1的状态是pending，那么p2的回调函数就会等待p1的状态改变；如果p1的状态已经是resolved或者rejected，那么p2的回调函数将会立刻执行。

```
const p1 = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error('fail')), 3000)
})

const p2 = new Promise(function (resolve, reject) {
  setTimeout(() => resolve(p1), 1000)
})

p2
  .then(result => console.log(result))
  .catch(error => console.log(error))
// Error: fail
```

上面代码中，p1是一个 Promise，3 秒之后变为rejected。p2的状态在 1 秒之后改变，resolve方法返回的是p1。由于p2返回的是另一个 Promise，导致p2自己的状态无效了，由p1的状态决定p2的状态。所以，后面的then语句都变成针对后者（p1）。又过了 2 秒，p1变为rejected，导致触发catch方法指定的回调函数。

注意，调用resolve或reject并不会终结 Promise 的参数函数的执行。

```
new Promise((resolve, reject) => {
  resolve(1);
  console.log(2);
}).then(r => {
  console.log(r);
});
// 2
// 1
```

上面代码中，调用resolve(1)以后，后面的console.log(2)还是会执行，并且会首先打印出来。这是因为立即 resolved 的 Promise 是在本轮事件循环的末尾执行，总是晚于本轮循环的同步任务。

一般来说，调用resolve或reject以后，Promise 的使命就完成了，后继操作应该放到then方法里面，而不应该直接写在resolve或reject的后面。所以，最好在它们前面加上return语句，这样就不会有意外。

```
new Promise((resolve, reject) => {
  return resolve(1);
  // 后面的语句不会执行
  console.log(2);
})
```

## Async/await

「async/await」是 promises 的另一种更便捷更流行的写法，同时它也更易于理解和使用。

### Async functions

让我们以 `async` 这个关键字开始。它可以被放置在任何函数前面，像下面这样：

```
async function f() {
  return 1;
}
```

在函数前面的「async」这个单词表达了一个简单的事情：即这个函数总是返回一个 **promise**。即使这个函数在语法上返回了一个非 promise 的值，加了「async」这个关键字就会指示 JavaScript 引擎自动将返回值包装成一个解析后的 **promise**。

例如，以下的代码就返回了一个以 1 为结果的解析后的 **promise** , 让我们试一下：

```
async function f() {
  return 1;
}

f().then(alert); // 1
```

... 我们也可以显式返回一个 **promise** ，结果是一样的：

```
async function f() {
  return Promise.resolve(1);
}

f().then(alert); // 1
```

所以说， `async` 确保了函数的返回值是一个 **promise** ，也会包装非 **promise** 的值。很简单是吧？但是还没完。还有一个关键字叫 `await` ，它只在 `async` 函数中有效，也非常酷。

### Await

语法如下：

```
// 只在 async 函数中有效
let value = await promise;
```

关键字 `await` 让 JavaScript 引擎等待直到 **promise** 完成并返回结果。

这里的例子就是一个 1 秒后解析的 **promise**:

```
async function f() {

  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("done!"), 1000)
  });

  let result = await promise; // 等待直到 promise 解析 （*）

  alert(result); // "done!"
}

f();
```

这个函数在执行的时候，「暂停」在了 (*) 那一行，并且当 **promise** 完成后，拿到 result 作为结果继续往下执行。所以「done!」是在一秒后显示的。

划重点： `await` 字面的意思就是让 **JavaScript** 引擎等待直到 **promise** 状态完成，然后以完成的结果继续执行。这个行为不会耗费 CPU 资源，因为引擎可以同时处理其他任务：执行其他脚本，处理事件等。

相比 `promise.then` 来获取 **promise** 结果，这只是一个更优雅的语法，同时也更易书写。

### 不能在普通函数中使用 await

如果我们尝试在非 `async` 函数中使用 `await` 的话，就会报语法错误：

```
function f() {
  let promise = Promise.resolve(1);
  let result = await promise; // 语法错误
}
```

如果函数前面没有 `async` 关键字，我们就会得到一个语法错误。就像前面说的，`await` 只在 `async` 函数 中有效。

### async/await example

```
async function showAvatar() {

  // 读取 JSON
  let response = await fetch('/article/promise-chaining/user.json');
  let user = await response.json();

  // 读取 github 用户信息
  let githubResponse = await fetch(`https://api.github.com/users/${user.name}`);
  let githubUser = await githubResponse.json();

  // 显示头像
  let img = document.createElement('img');
  img.src = githubUser.avatar_url;
  img.className = "promise-avatar-example";
  document.body.append(img);

  // 等待 3 秒
  await new Promise((resolve, reject) => setTimeout(resolve, 3000));

  img.remove();

  return githubUser;
}

showAvatar();
```

### await 不能在顶层代码运行

刚开始使用 `await` 的人常常会忘记 `await` 不能用在顶层代码中。如，下面这样就不行：

```
// 用在顶层代码中会报语法错误
let response = await fetch('/article/promise-chaining/user.json');
let user = await response.json();
```

我们可以将其包裹在一个匿名 async 函数中，如：

```
(async () => {
  let response = await fetch('/article/promise-chaining/user.json');
  let user = await response.json();
  ...
})();
```

### await 可以接收「thenables」

像 `promise.then` 那样，`await` 被允许接收 `thenable` 对象（具有 `then` 方法的对象）。有些对象虽然不是 `promise`，但是却兼容 `promise`，如果这些对象支持 `.then`，那么就可以对它们使用 `await`。

下面是一个 `Thenable` 类，`await` 接收了该类的实例：

```
class Thenable {
  constructor(num) {
    this.num = num;
  }
  then(resolve, reject) {
    alert(resolve);
    // 1 秒后解析为 this.num*2
    setTimeout(() => resolve(this.num * 2), 1000); // (*)
  }
};

async function f() {
  // 等待 1 秒, result 变为 2
  let result = await new Thenable(1);
  alert(result);
}

f();
```

如果 await 接收了一个非 **promise** 的但是提供了 `.then` 方法的对象，它就会调用这个 `then` 方法，并将原生函数 `resolve，reject` 作为参数传入。然后 `await` 等到这两个方法中的某个被调用（在例子中发生在（*）的那一行），再处理得到的结果。


### Async methods

如果想定义一个 `async` 的类方法，在方法前面添加 `async` 就可以了：

```
class Waiter {
  async wait() {
    return await Promise.resolve(1);
  }
}

new Waiter()
  .wait()
  .then(alert); // 1
```

### 异常处理

如果一个 **promise** 正常解析，`await promise` 返回的就是其结果。但是如果 **promise** 被拒绝，就会抛出一个错误，就像在那一行有个 `throw` 语句那样。

这里的代码：

```
async function f() {
  await Promise.reject(new Error("Whoops!"));
}
```

...和下面是一样的：

```
async function f() {
  throw new Error("Whoops!");
}
```

在真实的环境下，**promise** 被拒绝前通常会等待一段时间。所以 `await` 会等待，然后抛出一个错误。

我们可以用 `try...catch` 来捕获上面的错误，就像对一般的 `throw` 语句那样：

```
async function f() {

  try {
    let response = await fetch('http://no-such-url');
  } catch(err) {
    alert(err); // TypeError: failed to fetch
  }
}

f();
```

如果有错误发生，代码就会跳到 `catch` 块中。当然也可以用 `try` 包裹多行 `await` 代码：

```
async function f() {

  try {
    let response = await fetch('/no-user-here');
    let user = await response.json();
  } catch(err) {
    // 捕获到 fetch 和 response.json 中的错误
    alert(err);
  }
}

f();
```

如果我们不使用 `try...catch`，由f() 产生的 **promise** 就会被拒绝。我们可以在函数调用后添加 `.catch` 来处理错误：

```
async function f() {
  let response = await fetch('http://no-such-url');
}

// f() 变为一个被拒绝的 promise
f().catch(alert); // TypeError: failed to fetch // (*)
```

如果我们忘了添加 `.catch`，我们就会得到一个未处理的 **promise** 错误（显示在控制台）。我们可以通过在错误处理与全局事件处理器来捕获这些。

### async/await 和 promise.then/catch

当我们使用 `async/await` 时，几乎就不会用到 `.then` 了，因为为我们`await` 处理了异步等待。并且我们可以用 `try...catch` 来替代 `.catch`。这通常更加方便（当然不是绝对的）。

但是当我们在顶层代码，外面并没有任何 `async` 函数，我们在语法上就不能使用 `await` 了，所以这时候就可以用 `.then/catch` 来处理结果和异常。

就像上面代码的 (*) 那行一样。

### async/await 可以和 Promise.all 一次使用

当我们需要同时等待多个 **promise** 时，我们可以用 `Promise.all` 来包裹他们，然后使用 `await`：

```
// 等待多个 promise 结果
let results = await Promise.all([
  fetch(url1),
  fetch(url2),
  ...
 ]);
```

如果发生错误，也会正常传递：先从失败的 **promise** 传到 `Promise.all`，然后变成我们能用 `try...catch` 处理的异常。

### Microtask queue

**promise** 回调是异步执行的。每个 `.then/catch/finally` 回调首先被放入「微任务队列」然后在当前代码执行完成后被执行。

`Async/await` 是基于 **promise** 的，所以它内部使用相同的微任务队列，并且相对宏任务来说具有更高的优先级。

例如，看代码：

+ `setTimeout(handler, 0)`，应该以零延迟运行 handler 函数。
+ `let x = await f()`，函数 f() 是异步的，但是会立即运行。

那么如果 `await` 在 `setTimeout` 下面，哪一个先执行呢？

```
async function f() {
  return 1;
}

(async () => {
    setTimeout(() => alert('timeout'), 0);

    await f();

    alert('await');
})();
```

这里很确定：`await` 总是先完成，因为（作为微任务）它相比 `setTimeout` 具有更高的优先级。

### 总结

函数前面的关键字 `async` 有两个作用：

1. 让这个函数返回一个 promise
2. 允许在函数内部使用 await

这个 `await` 关键字又让 **JavaScript** 引擎等待直到 **promise** 完成，然后：

1. 如果有错误，就会抛出异常，就像那里有一个 throw error 语句一样。
2. 否则，就返回结果，并赋值。

这两个关键字一起用就提供了一个很棒的方式来控制异步代码，并且易于读写。

有了 `async/await` 我们就几乎不需要使用 `promise.then/catch`，但是不要忘了它们是基于 **promise** 的，所以在有些时候（如在最外层代码）我们就可以用 **promise** 的形式。再有就是 `Promise.all` 可以帮助我们同时处理多个异步任务。

# 原文资料

+ Wikipedia - ECMAScript : https://en.wikipedia.org/wiki/ECMAScript#cite_note-27
+ ecma-international - 官网 : https://www.ecma-international.org/ecma-262/6.0/
+ ECMAScript 6 入门 - 阮一峰 : http://es6.ruanyifeng.com/
+ [译]带你理解 Async/await : https://savokiss.com/tech/async-await.html
+ javascript.info - async-await : https://javascript.info/async-await