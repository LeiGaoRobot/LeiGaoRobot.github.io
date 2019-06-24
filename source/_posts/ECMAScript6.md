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

# What is ECMAScript 6?

ECMAScript第6版，最初称为ECMAScript 6（ES6），后来更名为ECMAScript 2015，于2015年6月完成。此更新为编写复杂应用程序添加了重要的新语法，包括类声明( `class Foo { ... }` )*，ES6的模块`import * as moduleName from "..."; export const Foo`，但在语义上用与ECMAScript 5严格模式相同的术语定义它们。其它新功能包括iterators 和 for/of loops，Python风格的generator，**箭头函数表达式( `()=>{ ... }` )**，**let**关键字为局部声明，关键字为**const**的常量声明，二进制数据类型数组，新的集合（maps，sets和WeakMap）， promise, 数字和数学增强，反射，代理（虚拟对象和wrappers的元编程）和字符串的模板文字。完整的清单很广泛。作为第一个“ECMAScript Harmony”规范，它也被称为“ES6 Harmony”。

# Promises

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
+ [译]带你理解 Async/await : https://savokiss.com/tech/async-await.html
+ javascript.info - async-await : https://javascript.info/async-await