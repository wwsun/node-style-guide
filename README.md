# Node.js 风格指南

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

  - [参考资料](#%E5%8F%82%E8%80%83%E8%B5%84%E6%96%99)
  - [类型](#%E7%B1%BB%E5%9E%8B)
  - [对象](#%E5%AF%B9%E8%B1%A1)
  - [数组](#%E6%95%B0%E7%BB%84)
  - [字符串](#%E5%AD%97%E7%AC%A6%E4%B8%B2)
  - [函数](#%E5%87%BD%E6%95%B0)
  - [属性](#%E5%B1%9E%E6%80%A7)
  - [变量](#%E5%8F%98%E9%87%8F)
  - [Requires](#requires)
  - [回调函数](#%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0)
  - [Try catch](#try-catch)
  - [提升](#%E6%8F%90%E5%8D%87)
  - [条件表达式 & 相等性](#%E6%9D%A1%E4%BB%B6%E8%A1%A8%E8%BE%BE%E5%BC%8F-&-%E7%9B%B8%E7%AD%89%E6%80%A7)
  - [代码块](#%E4%BB%A3%E7%A0%81%E5%9D%97)
  - [注释](#%E6%B3%A8%E9%87%8A)
  - [空格](#%E7%A9%BA%E6%A0%BC)
  - [逗号](#%E9%80%97%E5%8F%B7)
  - [分号作为语句块的结束](#%E5%88%86%E5%8F%B7%E4%BD%9C%E4%B8%BA%E8%AF%AD%E5%8F%A5%E5%9D%97%E7%9A%84%E7%BB%93%E6%9D%9F)
  - [类型转换 & 强制类型转换](#%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2-&-%E5%BC%BA%E5%88%B6%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2)
  - [命名约定](#%E5%91%BD%E5%90%8D%E7%BA%A6%E5%AE%9A)
  - [访问器](#%E8%AE%BF%E9%97%AE%E5%99%A8)
  - [构造函数](#%E6%9E%84%E9%80%A0%E5%87%BD%E6%95%B0)
  - [ES6箭头函数](#es6%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0)
  - [ES6增强的对象字面量](#es6%E5%A2%9E%E5%BC%BA%E7%9A%84%E5%AF%B9%E8%B1%A1%E5%AD%97%E9%9D%A2%E9%87%8F)
  - [ES6模板字符串](#es6%E6%A8%A1%E6%9D%BF%E5%AD%97%E7%AC%A6%E4%B8%B2)
  - [ES6函数参数增强](#es6%E5%87%BD%E6%95%B0%E5%8F%82%E6%95%B0%E5%A2%9E%E5%BC%BA)
  - [ES6新增关键字let和const](#es6%E6%96%B0%E5%A2%9E%E5%85%B3%E9%94%AE%E5%AD%97let%E5%92%8Cconst)
  - [ES6迭代器和`for..of`](#es6%E8%BF%AD%E4%BB%A3%E5%99%A8%E5%92%8Cforof)
  - [ES6生成器](#es6%E7%94%9F%E6%88%90%E5%99%A8)
  - [ES6模块](#es6%E6%A8%A1%E5%9D%97)
  - [ES6新增集合Map和Set](#es6%E6%96%B0%E5%A2%9E%E9%9B%86%E5%90%88map%E5%92%8Cset)
  - [ES6 Promise](#es6-promise)
  - [推荐的书](#%E6%8E%A8%E8%8D%90%E7%9A%84%E4%B9%A6)
  - [推荐的博客](#%E6%8E%A8%E8%8D%90%E7%9A%84%E5%8D%9A%E5%AE%A2)
- [};](#)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### 参考资料

- [Airbnb styleguide](https://github.com/airbnb/javascript)
- RisingStack's [Node.js styleguide](https://github.com/RisingStack/node-style-guide)
- Caolan's [Node.js styleguide](http://caolanmcmahon.com/posts/nodejs_style_and_structure)
- Felixge's [Node.js styleguide](https://github.com/felixge/node-style-guide)
- Baidu EFE: [ES6 develop overview](http://efe.baidu.com/blog/es6-develop-overview/)

## 类型

  - **原始类型**: 当你访问一个原始数据类型时，你直接操作的是它的值

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    var foo = 1;
    var bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```
  - **复杂情况**: 当你访问的是一个复杂类型时，你操作的是它的引用

    + `object`
    + `array`
    + `function`

    ```javascript
    var foo = [1, 2];
    var bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ back to top](#)**

## 对象

  - 在对象创建时使用字面量语法

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

  - 使用可读的别名，避免使用保留字

    ```javascript
    // bad
    var superman = {
      class: 'alien'
    };

    // bad
    var superman = {
      klass: 'alien'
    };

    // good
    var superman = {
      type: 'alien'
    };
    ```

**[⬆ back to top](#)**

## 数组

  - 使用字面量语法创建数组

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

  - 当你不知道数组的长度时使用Array#push.

    ```javascript
    var someStack = [];


    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```

  - 当你需要复制数据时使用Array#slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

    ```javascript
    var len = items.length;
    var itemsCopy = [];
    var i;

    // bad
    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // good
    itemsCopy = items.slice();
    ```

  - 将一个类数组对象转为数组，使用Array#slice.

    ```javascript
    function trigger() {
      var args = Array.prototype.slice.call(arguments);
      ...
    }
    ```

**[⬆ back to top](#)**


## 字符串

  - 使用单引号 `''` 表示字符串

    ```javascript
    // bad
    var name = "Bob Parr";

    // good
    var name = 'Bob Parr';

    // bad
    var fullName = "Bob " + this.lastName;

    // good
    var fullName = 'Bob ' + this.lastName;
    ```

  - 长于80个字符的字符串应该被写成多行（使用字符串拼接或ES6的模板字符串）
  - 注意：如果过度使用，长字符串拼接会影响性能. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40)

    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    var errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';
      
    // good
    var errorMessage = `
      hello
      world
      this
      is
    `;
      
    ```

  - 当使用程序来生成字符串时，使用Array#join，而不是字符串拼接.

    ```javascript
    var items;
    var messages;
    var length;
    var i;

    messages = [{
      state: 'success',
      message: 'This one worked.'
    }, {
      state: 'success',
      message: 'This one worked as well.'
    }, {
      state: 'error',
      message: 'This one did not work.'
    }];

    length = messages.length;

    // bad
    function inbox(messages) {
      items = '<ul>';

      for (i = 0; i < length; i++) {
        items += '<li>' + messages[i].message + '</li>';
      }

      return items + '</ul>';
    }

    // good
    function inbox(messages) {
      items = [];

      for (i = 0; i < length; i++) {
        items[i] = messages[i].message;
      }

      return '<ul><li>' + items.join('</li><li>') + '</li></ul>';
    }
    ```

**[⬆ back to top](#)**


## 函数

  - 函数表达式:

    ```javascript
    // anonymous function expression
    var anonymous = function() {
      return true;
    };

    // named function expression
    var named = function named() {
      return true;
    };

    // immediately-invoked function expression (IIFE)
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  - 永远不要再一个非函数语句块内使用函数声明(if, while, 等). 将函数赋值给一个变量.

    ```javascript
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    var test;
    if (currentUser) {
      test = function test() {
        console.log('Yup.');
      };
    }
    ```

  - 永远不要将你的参数命名为 `arguments`, 这会与函数范围内的 `arguments` 对象冲突.

    ```javascript
    // bad
    function nope(name, options, arguments) {
      // ...stuff...
    }

    // good
    function yup(name, options, args) {
      // ...stuff...
    }
    ```

**[⬆ back to top](#)**



## 属性

  - 当访问属性时请使用`.`操作符.

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    // bad
    var isJedi = luke['jedi'];

    // good
    var isJedi = luke.jedi;
    ```

  - 当你要用变量访问属性时，请使用 `[]` .

    ```javascript
    var luke = {
      jedi: true,
      age: 28
    };

    function getProp(prop) {
      return luke[prop];
    }

    var isJedi = getProp('jedi');
    ```

**[⬆ back to top](#)**


## 变量

  - 始终使用 `var` 来声明变量. 否则会创建全局变量，污染全局命名空间.

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```

  - 声明变量时使用一个新行, 并且每一行都使用 `var` 来声明.

    ```javascript
    // bad
     var items = getItems(),
          goSportsTeam = true,
          dragonball = 'z';

    // good
     var items = getItems();
     var goSportsTeam = true;
     var dragonball = 'z';
    ```

  - 最后声明未赋值的便利. 后面如果你要使用前面的变量进行赋值时会显得很便利.

    ```javascript
    // bad
    var i;
    var items = getItems();
    var dragonball;
    var goSportsTeam = true;
    var len;

    // good
    var items = getItems();
    var goSportsTeam = true;
    var dragonball;
    var length;
    var i;
    ```

  - 避免冗余的变量声明, 可已使用 `Object` 对象来构建命名空间.

    ```javascript

    // bad
    var kaleidoscopeName = '..';
    var kaleidoscopeLens = [];
    var kaleidoscopeColors = [];

    // good
    var kaleidoscope = {
      name: '..',
      lens: [],
      colors: []
    };
    ```

  - 在变量作用范围的最顶端声明变量. 这可以帮你避免赋值提升的问题.

    ```javascript
    // bad
    function() {
      test();
      console.log('doing stuff..');

      //..other stuff..

      var name = getName();

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // good
    function() {
      var name = getName();

      test();
      console.log('doing stuff..');

      //..other stuff..

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // bad
    function() {
      var name = getName();

      if (!arguments.length) {
        return false;
      }

      return true;
    }

    // good
    function() {
      if (!arguments.length) {
        return false;
      }

      var name = getName();

      return true;
    }
    ```

**[⬆ back to top](#)**

## Requires

  - 使用如下顺序来组织node代码中的require语句:
      - core modules
      - npm modules
      - others

    ```javascript
    // bad
    var Car = require('./models/Car');
    var async = require('async');
    var http = require('http');

    // good
    var http = require('http');
    var fs = require('fs');

    var async = require('async');
    var mongoose = require('mongoose');

    var Car = require('./models/Car');
    ```

  - 当你引入模块时，不要加 `.js` 后缀

  ```javascript
    // bad
    var Batmobil = require('./models/Car.js');

    // good
    var Batmobil = require('./models/Car');

  ```

**[⬆ back to top](#)**

## 回调函数

  - 在回调函数中要始终检测错误

  ```javascript
  //bad
  database.get('pokemons', function(err, pokemons) {
    console.log(pokemons);
  });

  //good
  database.get('drabonballs', function(err, drabonballs) {
    if (err) {
      // handle the error somehow, maybe return with a callback
      return console.log(err);
    }
    console.log(drabonballs);
  });
  ```

  - 遇到错误时从回调中返回

  ```javascript
  //bad
  database.get('drabonballs', function(err, drabonballs) {
    if (err) {
      // if not return here
      console.log(err);
    }
    // this line will be executed as well
    console.log(drabonballs);
  });

  //good
  database.get('drabonballs', function(err, drabonballs) {
    if (err) {
      // handle the error somehow, maybe return with a callback
      return console.log(err);
    }
    console.log(drabonballs);
  });
  ```

  - 当你要开发接口给外部时，在你的回调函数中使用描述性的参数。它能够让你的代码更可读。

  ```javascript
  // bad
  function getAnimals(done) {
    Animal.get(done);
  }

  // good
  function getAnimals(done) {
    Animal.get(function(err, animals) {
      if(err) {
        return done(err);
      }

      return done(null, {
        dogs: animals.dogs,
        cats: animals.cats
      })
    });
  }
  ```

**[⬆ back to top](#)**


## Try catch

- 只能在同步函数中使用`throw`

  Try-catch 语句块不能被用在异步代码块中。
  
  ```javascript
  //bad
  function readPackageJson (callback) {
    fs.readFile('package.json', function(err, file) {
      if (err) {
        throw err;
      }
      ...
    });
  }
  //good
  function readPackageJson (callback) {
    fs.readFile('package.json', function(err, file) {
      if (err) {
        return  callback(err);
      }
      ...
    });
  }
  ```

- 在同步调用中捕获错误，`JSON.parse()`应该使用`try-catch`语句块

  ```javascript
  //bad
  var data = JSON.parse(jsonAsAString);

  //good
  var data;
  try {
    data = JSON.parse(jsonAsAString);
  } catch (e) {
    //handle error - hopefully not with a console.log ;)
    console.log(e);
  }
  ```

**[⬆ back to top](#)**

## 提升

  - 变量声明会被提升到作用域的顶端，而赋值操作则不会。

    ```javascript
    // 先看个简单的例子，显然它会抛出错误
    function example() {
      console.log(notDefined); // => throws a ReferenceError
    }

    // 我们先使用了一个变量，而后再声明并初始化这个变量
    // 输出结果没有报错，而是 `undefined`，意思是未被初始化
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // 变量声明部分会被提升，赋值部分仍保持不变
    // 上面的代码等同于
    function example() {
      var declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }
    ```

  - 匿名函数表达式会提升它们的变量名，但是函数赋值部门不会被提升

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function() {
        console.log('anonymous function expression');
      };
    }
    ```

  - 命名函数表达式会提升它们的变量名，但函数名或函数体不会被提升。

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        console.log('Flying');
      };
    }

    // the same is true when the function name
    // is the same as the variable name.
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        console.log('named');
      }
    }
    ```

  - 函数声明会被整体提升到作用域顶端

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  - 更多信息请参考 [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) by [Ben Cherry](http://www.adequatelygood.com/)

**[⬆ back to top](#)**

## 条件表达式 & 相等性

  - 使用 `===` 和 `!==` 来代替 `==` 和 `!=`.
  - 条件表达式会被使用`ToBoolean`方法进行强制类型转换。并且服从如下规则：

    + **Objects** 被转换为 **true**
    + **Undefined** 被转换为 **false**
    + **Null** 被转换为 **false**
    + **Booleans** 被转换为 **实际的boolean值**
    + **Numbers** 被转换为 **false** 如果是 **+0, -0, or NaN**, 其他都为 **true**
    + **Strings** 被转换为 **false** 如果是空字符串 `''`, 其他都为 **true**

    ```javascript
    if ([0]) {
      // true
      // 数组是对象，对象始终被转换为 `true`
    }
    ```

  - 使用缩减版.

    ```javascript
    // bad
    if (name !== '') {
      // ...stuff...
    }

    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (collection.length > 0) {
      // ...stuff...
    }

    // good
    if (collection.length) {
      // ...stuff...
    }
    ```

  - 更多信息请参考 [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll

**[⬆ back to top](#)**


## 代码块

  - 所有的多行代码块都要使用大括号，并且不要写在一行

    ```javascript
    // bad
    if (test)
      return false;

    // bad
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function() { return false; }

    // good
    function() {
      return false;
    }
    ```

**[⬆ back to top](#)**


## 注释

  - 使用 `/** ... */` 进行多行注释. 请在你们加入注释说明，指明参数和返回值的类型 

    ```javascript
    // bad
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param <String> tag
    // @return <Element> element
    function make(tag) {

      // ...stuff...

      return element;
    }

    // good
    /**
     * make() returns a new element
     * based on the passed in tag name
     *
     * @param <String> tag
     * @return <Element> element
     */
    function make(tag) {

      // ...stuff...

      return element;
    }
    ```

  - 使用 `//` 进行单行注释. 请用一个新行来添加注释。并在注释行前增加一个空行。 

    ```javascript
    // bad
    var active = true;  // is current tab

    // good
    // is current tab
    var active = true;

    // bad
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }

    // good
    function getType() {
      console.log('fetching type...');

      // set the default type to 'no type'
      var type = this._type || 'no type';

      return type;
    }
    ```

  - 如果是为了指明一个错误，请在你的注释前加上`FIXME`或`TODO`前缀来帮助其他开发者快速的了解你的注释意图。
  其中`FIXME`可以表示这个问题需要解决，或者`TODO`来表示需要被实现的功能块。

  - 使用 `// FIXME:` 来注解一个问题。

    ```javascript
    function Calculator() {

      // FIXME: shouldn't use a global here
      total = 0;

      return this;
    }
    ```

  - 使用 `// TODO:` 来注解一个需要被实现（完成）的任务。

    ```javascript
    function Calculator() {

      // TODO: total should be configurable by an options param
      this.total = 0;

      return this;
    }
  ```


**[⬆ back to top](#)**

## 空格

  - 推荐使用2个空格作为缩进

    ```javascript
    // bad
    function() {
    ∙∙∙∙var name;
    }

    // bad
    function() {
    ∙var name;
    }

    // good
    function() {
    ∙∙var name;
    }
    ```

  - 在所有起始的大括号前加一个空格

    ```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog'
    });
    ```

  - 在操作符见使用一个空格

    ```javascript
    // bad
    var x=y+5;

    // good
    var x = y + 5;
    ```

  - 文件结束后增加一个空行

    ```javascript
    // bad
    (function(global) {
      // ...stuff...
    })(this);
    ```

    ```javascript
    // bad
    (function(global) {
      // ...stuff...
    })(this);↵
    ↵
    ```

    ```javascript
    // good
    (function(global) {
      // ...stuff...
    })(this);↵
    ```

  - 对链接起来的方法使用缩进成多行的形式

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // good
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // bad
    var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
        .attr('width',  (radius + margin) * 2).append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);

    // good
    var leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .class('led', true)
        .attr('width',  (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);
    ```

**[⬆ back to top](#)**

## 逗号

  - 推荐的做法是逗号在每一行的末尾

    ```javascript
    // bad
    var hero = {
        firstName: 'Bob'
      , lastName: 'Parr'
      , heroName: 'Mr. Incredible'
      , superPower: 'strength'
    };

    // good
    var hero = {
      firstName: 'Bob',
      lastName: 'Parr',
      heroName: 'Mr. Incredible',
      superPower: 'strength'
    };
    ```

**[⬆ back to top](#)**


## 分号作为语句块的结束

  - **Yup.**

    ```javascript
    // bad
    (function() {
      var name = 'Skywalker'
      return name
    })()

    // good
    (function() {
      var name = 'Skywalker';
      return name;
    })();

    // good
    ;(function() {
      var name = 'Skywalker';
      return name;
    })();
    ```

**[⬆ back to top](#)**


## 类型转换 & 强制类型转换

  - 在声明语句的最前端执行强制类型转换.
  - Strings:

    ```javascript
    //  => this.reviewScore = 9;

    // bad
    var totalScore = this.reviewScore + '';

    // good
    var totalScore = '' + this.reviewScore;

    // bad
    var totalScore = '' + this.reviewScore + ' total score';

    // good
    var totalScore = this.reviewScore + ' total score';
    ```

  - 使用 `parseInt` 来进行整数的类型转换，并且始终提供一个基数.

    ```javascript
    var inputValue = '4';

    // bad
    var val = new Number(inputValue);

    // bad
    var val = +inputValue;

    // bad
    var val = inputValue >> 0;

    // bad
    var val = parseInt(inputValue);

    // good
    var val = Number(inputValue);

    // good
    var val = parseInt(inputValue, 10);
    ```

  - 如果某种情况下你为了性能原因需要避免使用`parseInt`，而是使用移位操作符，请添加注释说明

    ```javascript
    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    var val = inputValue >> 0;
    ```

  - **Note:** 在使用移位操作符时需要特别谨慎. 数字使用 [64-bit values](http://es5.github.io/#x4.3.19)表示的, 但是移位操作符总是返回32-bit的整数 ([source](http://es5.github.io/#x11.7)). 这对大于32-bit的整数而言，这会导致意向不到的行为. [Discussion](https://github.com/airbnb/javascript/issues/109). 最大的有符号32位整数是 2,147,483,647:

    ```javascript
    2147483647 >> 0 //=> 2147483647
    2147483648 >> 0 //=> -2147483648
    2147483649 >> 0 //=> -2147483647
    ```

  - Booleans:

    ```javascript
    var age = 0;

    // bad
    var hasAge = new Boolean(age);

    // good
    var hasAge = Boolean(age);

    // good
    var hasAge = !!age;
    ```

**[⬆ back to top](#)**


## 命名约定

  - 避免使用当个字符命名，使用描述性的名字：

    ```javascript
    // bad
    function q() {
      // ...stuff...
    }

    // good
    function query() {
      // ..stuff..
    }
    ```

  - 对于对象、函数、和实例采用小驼峰（camelCase）命名法

    ```javascript
    // bad
    var OBJEcttsssss = {};
    var this_is_my_object = {};
    function c() {}
    var u = new user({
      name: 'Bob Parr'
    });

    // good
    var thisIsMyObject = {};
    function thisIsMyFunction() {}
    var user = new User({
      name: 'Bob Parr'
    });
    ```

  - 当命名类或构造函数时使用大驼峰或Pascal命名法（PascalCase）

    ```javascript
    // bad
    function user(options) {
      this.name = options.name;
    }

    var bad = new user({
      name: 'nope'
    });

    // good
    function User(options) {
      this.name = options.name;
    }

    var good = new User({
      name: 'yup'
    });
    ```

  - 在私有属性前加上一个 `_` 前缀

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';

    // good
    this._firstName = 'Panda';
    ```

  - 当你要保存 `this` 值时，可以将其命名为 `_this`.

    ```javascript
    // bad
    function() {
      var self = this;
      return function() {
        console.log(self);
      };
    }

    // bad
    function() {
      var that = this;
      return function() {
        console.log(that);
      };
    }

    // good
    function() {
      var _this = this;
      return function() {
        console.log(_this);
      };
    }
    ```

  - 命名你的函数。这将有助于堆栈跟踪。

    ```javascript
    // bad
    var log = function(msg) {
      console.log(msg);
    };

    // good
    var log = function log(msg) {
      console.log(msg);
    };
    ```

**[⬆ back to top](#)**


## 访问器

  - 属性访问器并不是必须的。
  - 如果你确实需要，请命名为 getVal() 和 setVal('hello') 的形式

    ```javascript
    // bad
    dragon.age();

    // good
    dragon.getAge();

    // bad
    dragon.age(25);

    // good
    dragon.setAge(25);
    ```

  - 如果属性是一个布尔值，请使用 isVal() 或 hasVal()

    ```javascript
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  - 你也可以创建 get() 和 set() 函数, 但一定要保持一致.

    ```javascript
    function Jedi(options) {
      options || (options = {});
      var lightsaber = options.lightsaber || 'blue';
      this.set('lightsaber', lightsaber);
    }

    Jedi.prototype.set = function(key, val) {
      this[key] = val;
    };

    Jedi.prototype.get = function(key) {
      return this[key];
    };
    ```

**[⬆ back to top](#)**

## 构造函数

  - 在原型链上增加属性，而不是覆写原型链。

    ```javascript
    function Jedi() {
      console.log('new jedi');
    }

    // bad
    Jedi.prototype = {
      fight: function fight() {
        console.log('fighting');
      },

      block: function block() {
        console.log('blocking');
      }
    };

    // good
    Jedi.prototype.fight = function fight() {
      console.log('fighting');
    };

    Jedi.prototype.block = function block() {
      console.log('blocking');
    };
    ```

  - 你可以在方法中返回 `this` 从而来构建可链接的方法。

    ```javascript
    // bad
    Jedi.prototype.jump = function() {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function(height) {
      this.height = height;
    };

    var luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20) // => undefined

    // good
    Jedi.prototype.jump = function() {
      this.jumping = true;
      return this;
    };

    Jedi.prototype.setHeight = function(height) {
      this.height = height;
      return this;
    };

    var luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```


  - 你可以创建一个自定义的`toString()`方法，但是你要确保它能正常工作并且没有其他副作用。

    ```javascript
    function Jedi(options) {
      options || (options = {});
      this.name = options.name || 'no name';
    }

    Jedi.prototype.getName = function getName() {
      return this.name;
    };

    Jedi.prototype.toString = function toString() {
      return 'Jedi - ' + this.getName();
    };
    ```

**[⬆ back to top](#)**

## ES6箭头函数

  - 所有的Arrow Function的参数均使用 `()`包裹，即便只有一个参数：
  
    ```javascript
    // good
    let foo = (x) => x + 1;
    
    // bad
    let foo = x => x + 1;
    ```
    
  - 定义函数尽量使用Arrow functions，而不是`function`关键字
  
    ```javascript
    // good
    let foo = () => {
      // code  
    };
    
    // bad
    function foo() {
      // code  
    }
    
    // bad
    let foo = function () {
      // code  
    }
    ```

  除非当前场景不适合使用Arrow Function，如函数表达式需要自递归、需要运行时可变的`this`对象等。
  
  - 对于对象、类中的方法，使用增强的对象字面量
  
    ```javascript
    // good
    let foo = {
      bar () {
        // code  
      }
    }
    
    // bad
    let foo = {
      bar: () => {
        // code 
      }
    }
    
    // bad
    let foo = {
      bar: function () {
        // code
      }
    }
    ```

**[⬆ back to top](#)**    

    
## ES6增强的对象字面量

  - 可以在对象总直接定义方法
  
    ```javascript
    // good
    let foo = {
      bar() {
        // code  
      }
    }
    ```
  
  - 可使用通过计算得出的键值
  
    ```javascript
    // 当你需要的时候使用
    let MY_KEY = 'bar';
    let foo = {
      [MY_KEY + 'Hash']: 123
    }
    ```
  
  - 与当前scope中同名变量的简写

    ```javascript
    // bad
    let bar = 'bar';
    let foo = {
        bar // 相当于bar: bar
    };
    ```

**[⬆ back to top](#)**

        
## ES6模板字符串

  - 不推荐使用多行字符串，因为不方便代码缩进
    
    ```javascript
    // bad
    let html = 
    `<div>
      <p>Hello world</p>
    </div>`
    ```
  
  - 推荐使用ES6的字符串变量替换功能，这样可以取代字符串拼接
  
    ```javascript
    //good
    let name = 'weiwei';
    let time = '22:00';
    let message = `Hello ${name}, it's ${time} now`;
    ```

**[⬆ back to top](#)**

## ES6函数参数增强

  - 推荐使用默认值、剩余参数等功能，这能让你的函数声明和调用变得更为简洁
  
    ```javascript
    var foo = (x = 1) => x + 1;
    foo(); // 2
    
    var extend = (source, ...args) => {
        for (let target in args) {
            for (let name in Object.keys(target) {
                if (!source.hasOwnProperty(name) {
                    source[name] = target[name];
                }
            }
        }
    };
    
    var extensions = [
        {name: 'Zhang'},
        {age: 17},
        {work: 'hard'}
    ];
    extend({}, ...extensions);
    ```

**[⬆ back to top](#)**


## ES6新增关键字let和const

  - 推荐使用`let`全面代替`var`，因为它创建了块级作用域变量（变量只在代码块内生效），尤其是`for`循环
  
    ```javascript
    for(let i = 0; i < 10; i++) {
      foo[i].onclick = function() {
        console.log(i);
      };
    }    
    ```
    
  - 建议自由在逻辑上是常量的情况才使用 `const`，它代表常量，定的同时必须赋值
  
    ```javascript
    // good
    const MAX_CAT_SIZE_KG = 3000; 

    // bad
    MAX_CAT_SIZE_KG = 5000; // SyntaxError
    MAX_CAT_SIZE_KG++; // nice try, but still a SyntaxError
    ```

**[⬆ back to top](#)**


## ES6迭代器和`for..of`

  - 推荐使用`for..of`来迭代集合对象（Array, Map, Set, arguments对象）的**值**
  
    ```javascript
    // good
    for (let item of array) {
      // do somehting
    }
    ```
    
  - 避免使用`for...in`来迭代结合对象，它通常用于迭代对象的**属性名**


**[⬆ back to top](#)**

  
## ES6生成器

  - 谨慎使用生成器，异步控制器的未来是`async`和`await`这两个关键字

    ```javascript
    // good
    async function save(Something) {  
      try {
        await Something.save(); // 等待await后面的代码执行完，类似于yield
      } catch (ex) {
        //error handling
      }
      console.log('success');
    }
    ```

**[⬆ back to top](#)**

    
## ES6模块

  - 谨慎使用ES6的模块系统，Node项目建议使用CommonJS方案，因为ES6并没有包括模块加载器规范，[参考文章](http://www.csdn.net/article/2015-04-30/2824595-Modules-in-ES6) 
  - 或者使用ES6的模块定义，但使用ADM作为运行时模块解决方案
    - 保持使用`import`和`export`进行模块的引入和定义，可以安全地使用命名`export`和默认`export`
    - 在使用Babel转换时，配置`modules: 'amd'`转换为AMD的模块定义
    - 不要依赖`SystemJS`这样的ES6模块加载器


**[⬆ back to top](#)**

    
## ES6新增集合Map和Set

  - 当你的元素或者键值有可能不是字符串时，无条件地使用`Map`和`Set`
  - 有移除操作的需求时，使用`Map`和`Set`
  - 当仅需要一个不可重复的集合时，使用`Set`优先于普通对象，而不要使用`{foo: true}`这样的对象
  - 当需要遍历功能时，使用`Map`和`Set`，因为其可以简单地使用`for..of`进行遍历
  - `WeakMap`和`WeakSet`是没有办法模拟实现的，因此不要使用

**[⬆ back to top](#)**
  
## ES6 Promise

  - 建议所有异步均使用Promise实现
  
    ```javascript
    // 构造一个Promise实例
    var promise = new Promise(function(resolve, reject) {
      // ... some code
    
      if (/* 异步操作成功 */){
        resolve(value);
      } else {
        reject(error);
      }
    });
    ```
    
  - Promise实例生成后，可以用`then`方法分别制定Resolved状态和Reject状态的回调函数
  
    ```javascript
    promise.then(function(value) {
      // success
    }, function(value) {
      // failure
    });
    ```

**[⬆ back to top](#)**


## 推荐的书

  - [JavaScript: The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](http://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](http://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](http://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](http://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](http://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](http://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](http://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](http://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
  - [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
  - [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](http://jsbooks.revolunet.com/)
  - [Third Party JavaScript](http://manning.com/vinegar/) - Ben Vinegar and Anton Kovalyov

## 推荐的博客

  - [DailyJS](http://dailyjs.com/)
  - [JavaScript Weekly](http://javascriptweekly.com/)
  - [JavaScript, JavaScript...](http://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](http://weblog.bocoup.com/)
  - [Adequately Good](http://www.adequatelygood.com/)
  - [NCZOnline](http://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](http://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [Dustin Diaz](http://dustindiaz.com/)
  - [nettuts](http://net.tutsplus.com/?s=javascript)

**[⬆ back to top](#table-of-contents)**

**The JavaScript Style Guide Guide**

  - [Reference](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)


**[⬆ back to top](#table-of-contents)**

# };