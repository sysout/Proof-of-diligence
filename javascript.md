- Date
  *

- bind
  * onChange={ this.updateEmployee.bind(this, record.address) }

- [arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
  * Returning object literals
    + `var func = () => { foo: 1 };` // Calling func() returns undefined!
    + code inside braces ({}) is parsed as a sequence of statements
    + `var func = () => ({foo: 1});` // ok

- [destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
  ```js
  const {b} = {a: 10, b: 20, c: 30, d: 40};
  console.log(b); // 20
  ```

## [Rapid JavaScript Training](https://app.pluralsight.com/library/courses/rapid-javascript-training/table-of-contents)
- Promise & Obervables
  *

## [Rapid ES6 Training](https://app.pluralsight.com/library/courses/rapid-es6-training/table-of-contents)
- table
  * New Syntax
  * ES6 Modules and Classes
  * New Types and Object Extensions
  * Iterators, Generators and Promises
  * Arrays and Collections
  * The Reflect API
  * The Proxy API
- http://kangax.github.io/compat-table/es6/
- New Syntax
  * let
    + Answer: undefined
      ```javascript
      'use strict';
      console.log(productId);
      var productId = 12;
      ```
    + Answer: ReferenceError: productId is not defined
      ```javascript
      'use strict';
      console.log(productId);
      let productId = 12;
      ```
    + Answer: 12
      ```javascript
      'use strict';
      let productId = 12;
      {
        let productId = 2000;
      }
      console.log(productId);
      ```
    + `**` Answer: 12
      ```javascript
      'use strict';
      function updateProductId(){
        productId = 12;
      }
      let productId = null;
      updateProductId();
      console.log(productId);
      ```
    + Answer: 42
      ```javascript
      'use strict';
      let productId = 42;
      for (let productId = 0; productId < 10; productId++){
      }
      console.log(productId);
      ```
    + Answer: 2
      ```javascript
      'use strict';
      let updateFunctions = [];
      for (var i = 0; i < 2; i++){
        updateFunctions.push(function () { return i; });
      }
      console.log(updateFunctions[0]());
      ```
    + `***` Answer: 0
      ```javascript
      'use strict';
      let updateFunctions = [];
      for (let i = 0; i < 2; i++){
        updateFunctions.push(function () { return i; });
      }
      console.log(updateFunctions[0]());
      ```
      - explain: each iteration of the loop has it's own i variable
  * const
    + Answer: SyntaxError: Unexpected token ;
      ```javascript
      'use strict';
      const MARKUP_PCT;
      console.log(MARKUP_PCT);
      ```
    + Answer: TypeError: Assignment to constant variable.
      ```javascript
      'use strict';
      const MARKUP_PCT = 100;
      MARKUP_PCT = 10;
      console.log(MARKUP_PCT);
      ```
    + `**` Answer: 100
      ```javascript
      'use strict';
      const MARKUP_PCT = 100;
      if (MARKUP_PCT > 0){
        const MARKUP_PCT = 10;
      }
      console.log(MARKUP_PCT);
      ```
      - note: const is like let, anything declared in a block is only scoped to that block
  * Block Scoping
  * Array Functions =>
    + Answer: function
      ```javascript
      'use strict';
      var getPrice = count => count * 4.00;
      console.log(getPrice(2));
      ```
      - note: when only one input, no parentheses is needed
    + `**` Answer: #document
      ```javascript
      'use strict';
      document.addEventListener('click', function(){
        console.log(this);
      });
      ```
    + `**` Answer: Window {...}
      ```javascript
      'use strict';
      document.addEventListener('click', () => console.log(this));
      ```
    + Answer: Object { number: 123, process: f }
      ```javascript
      'use strict';
      var invoice = {
        number: 123,
        process: function () {
          console.log(this);
        }
      };
      invoice.process();
      ```
    + Answer: Window {...}
      ```javascript
      'use strict';
      var invoice = {
        number: 123,
        process: () => console.log(this)
      };
      invoice.process();
      ```
    + `***` Answer: 123
      ```javascript
      'use strict';
      var invoice = {
        number: 123,
        process: function () {
          return () => console.log(this.number);
        }
      };
      invoice.process()();
      ```
    + `***` Answer: 123
      ```javascript
      'use strict';
      var invoice = {
        number: 123,
        process: function () {
          return () => console.log(this.number);
        }
      };
      var newInvoice = {
        number: 456
      };
      invoice.process().bind(newInvoice)();
      invoice.process().call(newInvoice);
      ```
      - note: js runtime just ignore the bind/call when using array function
    + `*` Answer: SyntaxError: unexpected token =>
      ```javascript
      'use strict';
      var getPrice = ()
        => 5.99;
      console.log(typeof getPrice);
      ```
    + `**` Answer: false
      ```javascript
      'use strict';
      var getPrice = () => 5.99;
      console.log(getPrice.hasOwnProperty("prototype"));
      ```
  * Default Function Parameters
    + `*` Answer: 1000, hardware
      ```javascript
      'use strict';
      var getProduct = function(productId = 1000, type = 'software') {
        console.log(productId + ', ' + type);
      };
      getProduct(undefined, 'hardware');
      ```
      - note: when pass undefined, js will use default parameters if there is one
    + `*` Answer: 5.35
      ```javascript
      'use strict';
      var getTotal = function(price, tax = price * 0.07) {
        console.log(price + tax);
      };
      getTotal(5.00);
      ```
    + `*` Answer: 5.35
      ```javascript
      'use strict';
      var getTotal = function(price, tax = price * 0.07) {
        console.log(price + tax);
      };
      getTotal(5.00);
      ```
      - note: think `(price, tax = price * 0.07)` has its own little scope
    + Answer: 1
      ```javascript
      'use strict';
      var getTotal = function(price, tax = 0.07) {
        console.log(arguments.length);
      };
      getTotal(5.00);
      ```
    + `*` Answer: SyntaxError: Use before declaration
      ```javascript
      'use strict';
      var getTotal = function(price = adjustment, adjustment = 1.00) {
        console.log(price + adjustment);
      };
      getTotal();
      ```
      - note: no look ahead in parameter list
    + `*` Answer: 6
      ```javascript
      'use strict';
      var getTotal = function(price = adjustment, adjustment = 1.00) {
        console.log(price + adjustment);
      };
      getTotal(5.00);
      ```
    + `*` Answer: 20
      ```javascript
      'use strict';
      var getTotal = new Function("price = 20.00", "return price;");
      console.log(getTotal());
      ```
  * Rest
    + Answer: true
      ```javascript
      'use strict';
      var showCategories = function (productId, ...categories) {
        console.log(categories instanceof Array);
      }
      showCategories(123, 'search', 'advertising');
      ```
    + Answer: 1
      ```javascript
      'use strict';
      var showCategories = function (productId, ...categories) {
      }
      console.log(showCategories.length);
      ```
    + Answer: 3
      ```javascript
      'use strict';
      var showCategories = function (productId, ...categories) {
        console.log(categories.length);
      }
      showCategories(123, 'search', 'advertising');
      ```
    + Answer: ['search', 'advertising']
      ```javascript
      'use strict';
      var showCategories = new Function ("...categories", "return categories;");
      console.log(showCategories('search', 'advertising'));
      ```
  * Spread
    + Answer: 20
      ```javascript
      'use strict';
      var prices = [12, 20, 18];
      var maxPrice = Math.max(...prices);
      console.log(maxPrice);
      ```
    + Answer: [12, 20, 18]
      ```javascript
      'use strict';
      var prices = [12, 20, 18];
      var newPriceArray = [...prices];
      console.log(newPriceArray);
      ```
    + `*` Answer: [undefined, undefined] [undefined, undefined]
      ```javascript
      'use strict';
      var newPriceArray = Array(...[,,]);
      var newPriceArray2 = [...[,,]];
      console.log(newPriceArray);
      console.log(newPriceArray2);
      ```
      - note: Trailing commas
    + `*` Answer: 4
      ```javascript
      'use strict';
      var maxCode = Math.max(...'43210');
      console.log(maxCode);
      ```
  * Object Literal Extensions
    + Answer: {price: 5.99, quantity: 30}
      ```javascript
      'use strict';
      var price = 5.99, quantity = 30;
      var productView = {
        price,
        quantity
      };
      console.log(productView);
      ```
    + `***` Answer: 7.99
      ```javascript
      'use strict';
      var price = 5.99, quantity = 10;
      var productView = {
        price: 7.99,
        quantity: 1,
        calculateValue() {
          return this.price * this.quantity
        }
      };
      console.log(productView.calculateValue());
      ```
      - note: this refer to the context of the code, like array function
    + `**` Answer: 59.900000000000006
      ```javascript
      'use strict';
      var price = 5.99, quantity = 10;
      var productView = {
        price,
        quantity,
        "calculate value"() {
          return this.price * this.quantity
        }
      };
      console.log(productView["calculate value"]());
      ```
    + `**` Answer: {dynamicField-001: 5.99}
      ```javascript
      'use strict';
      var field = 'dynamicField';
      var price = 5.99;
      var productView = {
        [field + "-001"]: price
      };
      console.log(productView);
      ```
    + `**` Answer: in a method
      ```javascript
      'use strict';
      var method = 'doIt';
      var productView = {
        [method + "-001"]() {
          console.log("in a method");
        }
      };
      productView["doIt-001"]();
      ```
    + `**` Answer: true
      ```javascript
      'use strict';
      var ident = 'productId';
      var productView = {
        get [ident] () { return true; },
        set [ident] (value) {}
      };
      console.log(productView.productId);
      ```
  * for ... of Loops
    + Answer: hardware software vaporware
      ```javascript
      'use strict';
      var categories = ['hardware', 'software', 'vaporware'];
      for (var item of categories){
        console.log(item);
      }
      ```
    + Answer: 5
      ```javascript
      'use strict';
      var codes = 'ABCDE';
      var count = 0;
      for (var code of codes){
        count++;
      }
      console.log(count);
      ```
  * Octal and Binary Literals
    + Answer: 8 8 2 2
      ```javascript
      'use strict';
      var value = 0o10;
      console.log(value);
      var value = 0O10;
      console.log(value);
      var value = 0b10;
      console.log(value);
      var value = 0B10;
      console.log(value);
      ```
  * Template Literals
    + Answer: Invoice Number: 1350
      ```javascript
      'use strict';
      let invoiceNum = '1350';
      console.log(`Invoice Number: ${invoiceNum}`);
      ```
    + `*` Answer: ABC in multiple lines
      ```javascript
      'use strict';
      let message = `A
      B
      C`
      console.log(message);
      ```
    + Answer: Invoice Number: 1350
      ```javascript
      'use strict';
      function showMessage(message){
        let invoiceNum = '99';
        console.log(message);
      }
      let invoiceNum = '1350';
      showMessage(`Invoice Number: ${invoiceNum}`);
      ```
    + Answer: ["Invoice: ", " for ", "", raw: Array(3)] ["1350", "2000"]
      ```javascript
      'use strict';
      function processInvoice(segments, ...values){
        console.log(segments);
        console.log(values);
      }
      let invoiceNum = '1350';
      let amount = '2000';
      processInvoice `Invoice: ${invoiceNum} for ${amount}`;
      ```
  * Destructuring
    + Answer: ["50000", "75000"]
      ```javascript
      'use strict';
      let salary = ['32000', '50000', '75000'];
      let [low, ...remaining] = salary;
      console.log(remaining);
      ```
    + Answer: 88000
      ```javascript
      'use strict';
      let salary = ['32000', '50000', ['88000', '99000']];
      let [low, average, [actualLow, actualHigh]] = salary;
      console.log(actualLow);
      ```
    + `**` Answer: 50000
      ```javascript
      'use strict';
      function reviewSalary([low, average], high = '88000') {
        console.log(average);
      }
      reviewSalary(['32000', '50000']);
      ```
    + `**` Answer: 50000
      ```javascript
      'use strict';
      let salary = {
        low: '32000',
        average: '50000',
        high: '75000'
      };
      let {low: newLow, average: newAverage, high: newHigh} = salary;
      console.log(newHigh);
    ```
    + `***` Answer: Syntax Error
      ```javascript
      'use strict';
      let salary = {
        low: '32000',
        average: '50000',
        high: '75000'
      };
      let newLow, newAverage, newHigh;
      {low: newLow, average: newAverage, high: newHigh} = salary;
      console.log(newHigh);
      ```
      - note: {} is treated as block of code, not destructure statement
    + `***` Answer: 75000
      ```javascript
      'use strict';
      let salary = {
        low: '32000',
        average: '50000',
        high: '75000'
      };
      let newLow, newAverage, newHigh;
      ({low: newLow, average: newAverage, high: newHigh} = salary);
      console.log(newHigh);
      ```
    + Answer: min: Z max: A
      ```javascript
      'use strict';
      let [maxCode, minCode] = 'AZ';
      console.log(`min: ${minCode} max: ${maxCode}`);
      ```
    + Answer
## [JavaScript Design Patterns](https://app.pluralsight.com/library/courses/javascript-design-patterns/table-of-contents)
- Promise & Defer
  * Defer object
    + Progress raised as deferred runs
    + Done raised when deferred action completes successfully
    + Failure raised when deferred action is unsuccessful

## [Advanced JavaScript](https://app.pluralsight.com/library/courses/advanced-javascript/table-of-contents)
