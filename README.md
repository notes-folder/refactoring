# 笔记:《重构：改善既有代码的设计（第二版）》

<!-- markdownlint-disable MD036-->

Notes on "Refactoring: Improving the Design of Existing Code (2nd Edition)"

## 目录

- [代码的坏味道（Bad Smells In Code）](###代码的坏味道（Bad-Smells-In-Code）)
  - [神秘命名（Mysterious Name）](#神秘命名（Mysterious-Name）)
  - [重复代码（Duplicated Code）](#重复代码（Duplicated-Code）)
  - [过长函数（Long Function）](#过长函数（Long-Function）)
  - [过长参数列表（Long Parameter List）](#过长参数列表（Long-Parameter-List）)
  - [全局数据（Global Data）](#全局数据（Global-Data）)
  - [可变数据（Mutable Data）](#可变数据（Mutable-Data）)
  - [发散式变化（Divergent Change）](#发散式变化（Divergent-Change）)
  - [散弹式修改（Shotgun Surgery）](#散弹式修改（Shotgun-Surgery）)
  - [依恋情结（Feature Envy）](#依恋情结（Feature-Envy）)
  - [数据泥团（Data Clumps）](#数据泥团（Data-Clumps）)
  - [基本类型偏执（Primitive Obsession）](#基本类型偏执（Primitive-Obsession）)
  - [重复的switch（Repeated Switches）](#重复的switch（Repeated-Switches）)
  - [循环语句（Loops）](#循环语句（Loops）)
  - [冗赘的元素（Lazy Element）](#冗赘的元素（Lazy-Element）)
  - [夸夸奇谈通用型（Speculative Generality）](#夸夸奇谈通用型（Speculative-Generality）)
  - [临时字段（Temporary Field）](#临时字段（Temporary-Field）)
  - [过长的消息链（Message Chains）](#过长的消息链（Message-Chains）)
  - [中间人（Middle Man）](#中间人（Middle-Man）)
  - [内幕交易（Insider Trading）](#内幕交易（Insider-Trading）)
  - [过大的类（Large class）](#过大的类（Large-class）)
  - [异曲同工的类（Alternative Classes with Different Interfaces）](#异曲同工的类（Alternative-Classes-with-Different-Interfaces）)
  - [纯数据类（Data class）](#纯数据类（Data-class）)
  - [被拒绝的遗赠（Refused Bequest）](#被拒绝的遗赠（Refused-Bequest）)
  - [注释（Comment）](#注释（Comment）)
- [最有用的一组重构 (Most Useful Set Of Refactoring)](#最有用的一组重构（Most-Useful-Set-Of-Refactoring）)
  - [提炼函数（Extract Function）](#提炼函数（Extract-Function）)
  - [内联函数（Inline Function）](#内联函数（Inline-Function）)
  - [提炼变量（Extract Variable）](#提炼变量（Extract-Variable）)
  - [内联变量（Inline Variable）](#内联变量（Inline-Variable）)
  - [改变函数声明（Change Function Declaration）](#改变函数声明（Change-Function-Declaration）)
  - [封装变量（Encapsulate Variable）](#封装变量（Encapsulate-Variable）)
  - [变量改名（Rename Variable）](#变量改名（Rename-Variable）)
  - [引入参数对象（Introduce Parameter Object）](#引入参数对象（Introduce-Parameter-Object）)
  - [函数组合成类（Combine Functions Into Class）](#函数组合成类（Combine-Functions-Into-Class）)
  - [函数组合成变换（Combine Functions Into Transform）](#函数组合成变换（Combine-Functions-Into-Transform）)
  - [拆分阶段（Split Phase）](#拆分阶段（Split-Phase）)
- [封装（Encapsulate）](#封装（Encapsulate）)
  - [封装记录（Encapsulate Record）](#封装记录（Encapsulate-Record）)
  - [封装集合（Encapsulate Collection）](#封装集合（Encapsulate-Collection）)
  - [以对象取代基本类型（Replace Primitive with Object）](#以对象取代基本类型（Replace-Primitive-with-Object）)
  - [以查询取代临时变量（Replace Temp with Query）](#以查询取代临时变量（Replace-Temp-with-Query）)
  - [提炼类（Extract Class）](#提炼类（Extract-Class）)
  - [内联类（Inline Class）](#内联类（Inline-Class）)
  - [隐藏委托关系（Hide Delegate）](#隐藏委托关系（Hide-Delegate）)
  - [移除中间人（Remove Middle Man）](#移除中间人（Remove-Middle-Man）)
  - [替换算法（Substitute Algorithm）](#替换算法（Substitute-Algorithm）)
- [搬移特性（Moving Features）](#搬迁特性（Moving-Features）)
  - [搬移函数（Move Function）](#搬移函数（Move-Function）)
  - [搬移字段（Move Field）](#搬移字段（Move-Field）)
  - [搬移语句到函数（Move Statements into Function）](#搬移语句到函数（Move-Statements-into-Function）)
  - [搬移语句到调用者（Move Statements To Callers）](#搬移语句到调用者（Move-Statements-To-Callers）)
  - [以函数调用取代内联代码（Replace Inline Code with Function Call）](#以函数调用取代内联代码（Replace-Inline-Code-with-Function-Call）)
  - [移动语句（Slide Statements）](#移动语句（Slide-Statements）)
  - [拆分循环（Split Loop）](#拆分循环（Split-Loop）)
  - [以管道取代循环（Replace Loop with Pipeline）](#以管道取代循环（Replace-Loop-with-Pipeline）)
  - [移除死代码（Remove Dead Code）](#移除死代码（Remove-Dead-Code）)
- [重新组织数据（Organizing Data）](#重新组织数据（Organizing-Data）)
  - [拆分变量（Split Variable）](#拆分变量（Split-Variable）)
  - [字段改名（Rename Field）](#字段改名（Rename-Field）)
  - [以查询取代派生变量（Replace Derived Variable With Query）](#以查询取代派生变量（Replace-Derived-Variable-With-Query）)
  - [将引用对象改为值对象（Change Reference To Value）](#将引用对象改为值对象（Change-Reference-To-Value）)
  - [将值对象改为引用对象（Change Value To Reference）](#将值对象改为引用对象（Change-Value-To-Reference）)
- [简化条件逻辑（Simplifying Conditional Logic）](#简化条件逻辑（Simplifying-Conditional-Logic)
  - [分解条件表达式（Decompose Conditional）](#分解条件表达式（Decompose-Conditional）)
  - [合并条件表达式（Consolidate Conditional Expression）](#合并条件表达式（Consolidate-Conditional-Expression）)
  - [以卫语句取代件套表达式（Replace Nested Conditional with Guard Clauses）](#3-replace-nested-conditional-with-guard-clauses)
  - [以多态取代条件表达式（Replace Conditional with Polymorphism）](#以多态取代条件表达式（Replace-Conditional-with-Polymorphism）)
  - [引入特例（Introduce Special Case）](#引入特例（Introduce-Special-Case）)
  - [引入断言（Introduce Assertion）](#引入断言（Introduce-Assertion）)
- [重构API（Refactoring APIS）](#重构API（Refactoring-APIS）)
  - [将查询函数和修改函数分离（Separate Query from Modifier）](#将查询函数和修改函数分离（Separate-Query-from-Modifier）)
  - [函数参数化（Parameterize Function）](#函数参数化（Parameterize-Function）)
  - [移除标记参数（Remove Flag Argument）](#移除标记参数（Remove-Flag-Argument）)
  - [保持完整对象（Preserve Whole Object）](#保持完整对象（Preserve-Whole-Object）)
  - [以查询取代参数（Replace Parameter with Query）](#以查询取代参数（Replace-Parameter-with-Query）)
  - [以参数取代查询（Replace Query with Parameter）](#以参数取代查询（Replace-Query-with-Parameter）)
  - [移除设值方法（Remove Setting Method）](#移除设值方法（Remove-Setting-Method）)
  - [以工厂函数取代构造方法（Replace Constructor with Factory Function）](#以工厂函数取代构造方法（Replace-Constructor-with-Factory-Function）)
  - [以命令取代函数（Replace Function with Command）](#以命令取代函数（Replace-Function-with-Command）)
  - [以函数取代命令（Replace Command with Function）](#以函数取代命令（Replace-Command-with-Function）)
- [处理继承关系（Dealing With Inheritance）](#处理继承关系（Dealing-With-Inheritance）)
  - [方法上移（Pull Up Method）](#方法上移（Pull-Up-Method）)
  - [字段上移（Pull Up Field）](#字段上移（Pull-Up-Field）)
  - [构造方法本体上移（Pull Up Constructor Body）](#构造方法本体上移（Pull-Up-Constructor-Body）)
  - [方法下移（Push Down Method）](#方法下移（Push-Down-Method）)
  - [字段下移（Push Down Field）](#字段下移（Push-Down-Field）)
  - [以子类取代类型码（Replace Type Code with Subclasses）](#以子类取代类型码（Replace-Type-Code-with-Subclasses）)
  - [移除子类（Remove Subclass）](#移除子类（Remove-Subclass）)
  - [提炼超类（Extract Superclass）](#提炼超类（Extract-Superclass）)
  - [折叠继承关系（Collapse Hierarchy）](#折叠继承关系（Collapse-Hierarchy）)
  - [以委托取代子类（Replace Subclass with Delegate）](#以委托取代子类（Replace-Subclass-with-Delegate）)
  - [以委托取代超类（Replace Superclass with Delegate）](#以委托取代超类（Replace-Superclass-with-Delegate）)

## 代码的坏味道（Bad Smells In Code）

### 神秘命名（Mysterious Name）

Name should clearly communicate what they do and how to use them

### 重复代码（Duplicated Code）

Same code structure in more than one place

### 过长函数（Long Function）

the longer a function is, the more difficult it is to understand

### 过长参数列表（Long Parameter List）

Difficult to understand and easily introduce bug

### 全局数据（Global Data）

Global variable is difficult to track and debug

### 可变数据（Mutable Data）

Changes to data can often lead to unexpected consequences and tricky bugs

### 发散式变化（Divergent Change）

One module is changed in different ways for different reasons

### 散弹式修改（Shotgun Surgery）

When every time you make a change, you have to make a lot of little edits to a lot of different classes

### 依恋情结（Feature Envy）

When a function in one module spends more time communicating with functions or data inside another module than it does within its own module

### 数据泥团（Data Clumps）

Same three or four data items together in lots of places

### 基本类型偏执（Primitive Obsession）

Use primitive types instead of custom fundamental types

### 重复的switch（Repeated Switches）

Same conditional switching logic pops up in different places

### 循环语句（Loops）

Using loops instead of first-class functions such as filter or map

### 冗赘的元素（Lazy Element）

A class, struct or function that isn't doing enough to pay for itself should be eliminated.

### 夸夸奇谈通用型（Speculative Generality）

All sorts of hooks and special cases to handle things that aren’t required

### 临时字段（Temporary Field）

An instance variable that is set only in certain circumstances.

### 过长的消息链（Message Chains）

When a client asks one object for another object, which the client then asks for yet another object...

### 中间人（Middle Man）

When an object delegates much of its functionality.

### 内幕交易（Insider Trading）

Modules that whisper to each other by the coffee machine need to be separated by using Move Function and Move Field to reduce the need to chat.

### 过大的类（Large class）

A class is trying to do too much, it often shows up as too many fields

### 异曲同工的类（Alternative Classes with Different Interfaces）

Classes with methods that look to similar.

### 纯数据类（Data class）

Classes that have fields, getting and setting methods for the fields, and nothing else

### 被拒绝的遗赠（Refused Bequest）

Subclasses doesn't make uses of parents method

### 注释（Comment）

The comments are there because the code is bad

## 最有用的一组重构（Most Useful Set Of Refactoring）

### 提炼函数（Extract Function）

Extract fragment of code into its own function named after its purpose.

```typescript
function printOwing(invoice) {
  printBanner();
  let outstanding = calculateOutstanding();

  // print details
  console.log(`name: ${invoice.customer}`);
  console.log(`amount: ${outstanding}`);
}
```

to

```typescript
function printOwing(invoice) {
  printBanner();
  let outstanding = calculateOutstanding();
  printDetails(outstanding);

  function printDetails(outstanding) {
    console.log(`name: ${invoice.customer}`);
    console.log(`amount: ${outstanding}`);
  }
}
```

**Motivation**:

- You know what's the code doing without reading the details
- Short function is easier to read
- Reduce comment

### 内联函数（Inline Function）

Get rid of the function when the body of the code is just as clear as the name

```typescript
function rating(aDriver) {
  return moreThanFiveLateDeliveries(aDriver) ? 2 : 1;
}
function moreThanFiveLateDeliveries(aDriver) {
  return aDriver.numberOfLateDeliveries > 5;
}
```

to

```typescript
function rating(aDriver) {
  return aDriver.numberOfLateDeliveries > 5 ? 2 : 1;
}
```

**Motivation**

- When Indirection is needless (simple delegation) becomes irritating.
- If group of methods are badly factored and grouping them makes it clearer

### 提炼变量（Extract Variable）

Add a name to an expression

```typescript
//price is base price ­ quantity discount + shipping
return order.quantity * order.itemPrice -
  Math.max(0, order.quantity - 500) * order.itemPrice * 0.05 +
  Math.min(order.quantity * order.itemPrice * 0.1, 100);
```

to

```typescript
const basePrice = order.quantity * order.itemPrice;
const quantityDiscount = Math.max(0, order.quantity - 500) * order.itemP;
const shipping = Math.min(basePrice * 0.1, 100);
return basePrice - quantityDiscount + shipping;
```

**Motivation**

- Break down and name a part of a more complex piece of logic
- Easier for debugging

### 内联变量（Inline Variable）

Remove variable which doesn't really communicate more than the expression itself.

```typescript
let basePrice = anOrder.basePrice;
return (basePrice > 1000);
```

to

```typescript
return anOrder.basePrice > 1000;
```

### 改变函数声明（Change Function Declaration）

Rename a function, change list of parameters

```typescript
function circum(radius) {...}
```

to

```typescript
function circumference(radius) {...}
```

**Motivation**

- Easier to understand
- Easier to reuse, sometime better encapsulation

### 封装变量（Encapsulate Variable）

Encapsulate a reference to some data structure

```typescript
let defaultOwner = {firstName: "Martin", lastName: "Fowler"};
```

to

```typescript
// defaultOwner.js
let defaultOwnerData = {firstName: "Martin", lastName: "Fowler"};
export function defaultOwner() { return defaultOwnerData; }
export function setDefaultOwner(arg) { defaultOwnerData = arg; }
```

**Motivation**

- Provide a clear point to monitor changes and use of the data, like validation.

### 变量改名（Rename Variable）

Make shared variable's name can self-explain

```typescript
let a = height * width;
```

to

```typescript
let area = height * width;
```

### 引入参数对象（Introduce Parameter Object）

Replace groups of data items that regularly travel together with a single data structure

```typescript
function amountInvoiced(startDate, endDate) {}
function amountReceived(startDate, endDate) {}
function amountOverdue(startDate, endDate) {}
```

to

```typescript
function amountInvoiced(aDateRange) {}
function amountReceived(aDateRange) {}
function amountOverdue(aDateRange) {}
```

**Motivation**

- Make explicit the relationship between the data items
- Reduce the size of parameter list
- Make code more consistent
- Enable deeper changes to the code

### 函数组合成类（Combine Functions Into Class）

Form a class base on group of functions that operate closely on a common data

```typescript
function base(aReading) {}
function taxableCharge(aReading) {}
function calculateBaseCharge(aReading) {}
```

to

```typescript
class Reading() {
  base() {}
  taxableCharge() {}
  calculateBaseCharge() {}
}
```

**Motivation**

- Simplify function call by removing many arguments
- Easier to pass object to other parts of the system

### 函数组合成变换（Combine Functions Into Transform）

Takes the source data as input and calculates all the derivations, putting each derived value as a field in the output data

```typescript
function base(aReading) {}
function taxableCharge(aReading) {}
```

to

```typescript
function enrichReading(argReading) {
  const aReading = _.cloneDeep(argReading);
  aReading.baseCharge = base(aReading);
  aReading.taxableCharge = taxableCharge(aReading);
  return aReading;
}
```

**Motivation**

- Avoid duplication of logic

### 拆分阶段（Split Phase）

Split code which do different things into separate modules

```typescript
const orderData = orderString.split(/\s+/);
const productPrice = priceList[orderData[0].split("-")[1]];
const orderPrice = parseInt(orderData[1]) * productPrice;
```

to

```typescript
const orderRecord = parseOrder(orderString)
const orderPrice = price(orderRecord, priceList)

function parseOrder(aString) {
  const values = aString.split(/\s+/)
  return {
    productID: values[0].split("-")[1],
    quantity: parseInt(values[1])
  }
}
function price(order, priceList) {
  return order.quantity * priceList[order.productID]
}
```

**Motivation**

- Make the different explicit, revealing the different in the code
- Be able to deal with each module separately

## 封装（Encapsulate）

### 封装记录（Encapsulate Record）

Create record (class) from object

```typescript
organization = {name: "Acme gooseberries", country: "GB"};
```

to

```typescript
class Organization {
  constructor(data) {
    this._name = data.name;
    this._country = data.country;
  }

  get name() { return this._name; }
  set name(arg) { this._name = arg; }
  get country() { return this._country; }
  set country(arg) { this._country = arg; }
}
```

**Motivation**

- Hide what's stored and provide methods to get value
- Easier to refactoring, for example: rename

### 封装集合（Encapsulate Collection）

A method returns a collection. Make it return a read-only view and provide add/remove methods

```typescript
class Person {
  get courses() { return this._courses; }
  set courses(aList) { this._courses = aList; }
}
```

to

```typescript
class Person {
  get courses() { return this._courses.slice(); }
  addCourse(aCourse) {}
  removeCourse(aCourse) {}
}
```

**Motivation**

- Change to the collection should go through the owning class to prevent unexpected changes.
- Prevent modification of the underlying collection for example: return a copy or read-only proxy instead of collection value

### 以对象取代基本类型（Replace Primitive with Object）

Create class for data

```typescript
orders.filter(o => "high" === o.priority || "rush" === o.priority);
```

to

```typescript
orders.filter(o => o.priority.higherThan(new Priority("normal")));
```

**Motivation**

- Encapsulate behaviour with data

### 以查询取代临时变量（Replace Temp with Query）

Extract the assignment of the variable into a function

```typescript
const basePrice = this._quantity * this._itemPrice
if (basePrice > 1000) {
  return basePrice * 0.95;
} else {
  return basePrice * 0.98;
}
```

to

```typescript
get basePrice() { return this._quantity * this._itemPrice }
//...
if (this.basePrice > 1000) {
  return this.basePrice * 0.95;
} else {
  return this.basePrice * 0.98;
}
```

**Motivation**

- Avoid duplicating the calculation logic in similar functions

### 提炼类（Extract Class）

Extract class base on a subset of data and a subset of methods

```typescript
class Person {
  get officeAreaCode() { return this._officeAreaCode; }
  get officeNumber() { return this._officeNumber; }
}
```

to

```typescript
class Person {
  get officeAreaCode() { return this._telephoneNumber.areaCode; }
  get officeNumber() { return this._telephoneNumber.number; }
}
class TelephoneNumber {
  get areaCode() { return this._areaCode; }
  get number() { return this._number; }
}
```

**Motivation**

- Smaller class is easier to understand
- Separate class's responsibility

### 内联类（Inline Class）

Merge class if class isn't doing very much. Move its feature to another class then delete it.

```typescript
class Person {
  get officeAreaCode() { return this._telephoneNumber.areaCode; }
  get officeNumber() { return this._telephoneNumber.number; }
}
class TelephoneNumber {
  get areaCode() { return this._areaCode; }
  get number() { return this._number; }
}
```

to

```typescript
class Person {
  get officeAreaCode() { return this._officeAreaCode; }
  get officeNumber() { return this._officeNumber; }
}
```

**Motivation**

- Class is no longer pulling its weight and shouldn’t be around any more
- When want to refactor pair of classes. First Inline Class -> Extract Class to make new separation

### 隐藏委托关系（Hide Delegate）

A client is calling a delegate class of an object, create methods on the server to hide the delegate.

```typescript
manager = aPerson.department.manager;
```

to

```typescript
manager = aPerson.manager;

class Person {
  get manager() {
    return this.department.manager;
  }
}
```

**Motivation**

- Client doesn't need to know and response to delegation's change
- Better encapsulation

### 移除中间人（Remove Middle Man）

Client call the delegate directly

```typescript
manager = aPerson.manager;

class Person {
  get manager() {
    return this.department.manager;
  }
}
```

to

```typescript
manager = aPerson.department.manager;
```

**Motivation**

- When there are too many delegating methods

### 替换算法（Substitute Algorithm）

Replace complicated algorithm with simpler algorithm

```typescript
function foundPerson(people) {
  for (let i = 0; i < people.length; i++) {
    if (people[i] === "Don") {
      return "Don";
    }
    if (people[i] === "John") {
      return "John";
    }
    if (people[i] === "Kent") {
      return "Kent";
    }
  }
  return ""
}
```

to

```typescript
function foundPerson(people) {
  const candidates = ["Don", "John", "Kent"];
  return people.find(p => candidates.includes(p)) || "";
}
```

**Motivation**

- Change to algorithm which make changes easier
- The clearer algorithm is, the better.

## 搬迁特性（Moving Features）

### 搬移函数（Move Function）

Move a function when it references elements in other contexts more than the one it currently resides in

```typescript
class Account {
  get overdraftCharge() {}
}
class AccountType {}
```

to

```typescript
class Account {}
class AccountType {
  get overdraftCharge() {}
}
```

**Motivation**

- Improve encapsulation, loose coupling

### 搬移字段（Move Field）

Move field from once class to another

```typescript
class Customer {
  get plan() { return this._plan; }
  get discountRate() { return this._discountRate; }
}
```

to

```typescript
class Customer {
  get plan() { return this._plan; }
  get discountRate() { return this.plan.discountRate; }
}
```

**Motivation**

- Pieces of data that are always passed to functions together are usually best put in a single record
- If a change in one record causes a field in another record to change too, that’s a sign of a field in the wrong place

### 搬移语句到函数（Move Statements into Function）

When statement is a part of called functions (always go together), move it inside the function

```typescript
result.push(`<p>title: ${person.photo.title}</p>`);
result.concat(photoData(person.photo));

function photoData(aPhoto) {
  return [
    `<p>location: ${aPhoto.location}</p>`,
    `<p>date: ${aPhoto.data.toDateString()}</p>`
  ];
}
```

to

```typescript
result.concat(photoData(person.photo));

function photoData(aPhoto) {
  return [
    `<p>title: ${aPhoto.title}</p>`,
    `<p>location: ${aPhoto.location}</p>`,
    `<p>date: ${aPhoto.data.toDateString()}</p>`
  ];
}
```

**Motivation**

- Remove duplicated code

### 搬移语句到调用者（Move Statements To Callers）

```typescript
emitPhotoData(outStream, person.photo);

function emitPhotoData(outStream, photo) {
  outStream.write(`<p>title: ${photo.title}</p>\n`);
  outStream.write(`<p>location: ${photo.location}</p>\n`);
}
```

to

```typescript
emitPhotoData(outStream, person.photo);
outStream.write(`<p>location: ${photo.location}</p>\n`);

function emitPhotoData(outStream, photo) {
  outStream.write(`<p>title: ${photo.title}</p>\n`);
}
```

**Motivation**

- When common behavior used in several places needs to vary in some of its call

### 以函数调用取代内联代码（Replace Inline Code with Function Call）

Replace the inline code with a call to the existing function

```typescript
let appliesToMass = false;
for (const s of states) {
  if (s === "MA") appliesToMass = true;
}
```

```typescript
appliesToMass = states.includes("MA");
```

**Motivation**

- Remove duplication
- Meaningful function name is easier to understand

### 移动语句（Slide Statements）

Move related code to near each other

```typescript
const pricingPlan = retrievePricingPlan();
const order = retrieveOrder();
let charge
const chargePerUnit = pricingPlan.unit;
```

to

```typescript
const pricingPlan = retrievePricingPlan();
const chargePerUnit = pricingPlan.unit;
const order = retrieveOrder();
let charge;
```

**Motivation**

- It makes code easier to understand and easier to extract function

### 拆分循环（Split Loop）

Split the loop which does two different things

```typescript
let averageAge = 0;
let totalSalary = 0;
for (const p of people) {
  averageAge += p.age;
  totalSalary += p.salary;
}
averageAge = averageAge / people.length;
```

to

```typescript
let totalSalary = 0;
for (const p of people) {
  totalSalary += p.salary;
}

let averageAge = 0;
for (const p of people) {
  averageAge += p.age;
}
averageAge = averageAge / people.length;
```

**Motivation**

- Easier to use
- Easier to understand because each loop will do only 1 thing

### 以管道取代循环（Replace Loop with Pipeline）

Replace loop with collection pipeline, like `map` or `filter`

```typescript
const names = [];
for (const i of input) {
  if (i.job === "programmer") {
    names.push(i.name);
  }
}
```

to

```typescript
const names = input.filter(i => i.job === "programmer").
                    map(i => i.name);
```

**Motivation**

- Easier to understand the flow of data

### 移除死代码（Remove Dead Code）

```typescript
if (false) {
  doSomethingThatUsedToMatter();
}
```

to

```typescript

```

**Motivation**

- Easier and quicker for developer to understand the codebase

## 重新组织数据（Organizing Data）

### 拆分变量（Split Variable）

Any variable with more than one responsibility should be replaced with multiple variables, one for each responsibility

```typescript
let temp = 2 * (height + width);
console.log(temp);
temp = height * width;
console.log(temp);
```

to

```typescript
const perimeter = 2 * (height + width);
console.log(perimeter);
const area = height * width;
console.log(area);
```

**Motivation**

- Easier to understand

### 字段改名（Rename Field）

```typescript
class Organization {
  get name() {}
}
```

to

```typescript
class Organization {
  get title() {}
}
```

### 以查询取代派生变量（Replace Derived Variable With Query）

Remove any variables which cloud be easily calculate

```typescript
get discountedTotal() { return this._discountedTotal; }
set discount(aNumber) {
  const old = this._discount;
  this._discount = aNumber;
  this._discountedTotal += old - aNumber;
}
```

to

```typescript
get discountedTotal() { return this._baseTotal - this._discount; }
set discount(aNumber) { this._discount = aNumber; }
```

**Motivation**

- Minimize scope of mutable data
- A calculate makes it clearer what the meaning of data is

### 将引用对象改为值对象（Change Reference To Value）

Treat data as value. When update, replace entire inner object with a new one

```typescript
class Product {
  applyDiscount(arg) {
    this._price.amount -= arg;
  }
}
```

to

```typescript
class Product {
  applyDiscount(arg) {
    this._price = new Money(this._price.amount - arg, this._price.currency);
  }
}
```

**Motivation**

- Immutable data is easier to deal with

### 将值对象改为引用对象（Change Value To Reference）

When need to share an object in different place, or have duplicated objects

```typescript
let customer = new Customer(customerData);
```

to

```typescript
let customer = customerRepository.get(customerData.id);
```

**Motivation**

- Update one reference is easier and more consistent than update multiple copies

## 简化条件逻辑（Simplifying Conditional Logic

### 分解条件表达式（Decompose Conditional）

Decomposing condition and replacing each chunk of code with a function call

```typescript
let charge;
if (!aDate.isBefore(plan.summerStart) && !aData.isAfter(plan.summerEnd)) {
  charge = quantity * plan.summerRate;
} else {
  charge = quantity * plan.regularRate + plan.regularServiceCharge;
}
```

to

```typescript
const charge = isSummer() ? summerCharge() : regularCharge();
```

**Motivation**

- Clearer intention of what we're branching on

### 合并条件表达式（Consolidate Conditional Expression）

Consolidate different condition check which the result action is same to a single condition check with single result

```typescript
if (anEmployee.seniority < 2) return 0;
if (anEmployee.monthsDisabled > 12) return 0;
if (anEmployee.isPartTime) return 0;
```

to

```typescript
if (isNotEligibleForDisability()) return 0;

function isNotEligibleForDisability() {
   return ((anEmployee.seniority < 2)
    || (anEmployee.monthsDisabled > 12)
    || (anEmployee.isPartTime));
}
```

**Motivation**

- Often lead to Extract Function, which reveal instead of the code by function name
- If conditions are not related, don't consolidate them

### 3. Replace Nested Conditional with Guard Clauses

If condition is unusual condition, early return (Guard Clauses) and exist the function

```typescript
function getPayAmount() {
  let result;
  if (isDead) {
    result = deadAmount();
  } else {
    if (isSeparated) {
      result = separatedAmount();
    } else {
      if (isRetired) {
        result = retiredAmount();
      } else {
        result = normalPayAmount();
      }
    }
  }
  return result;
}
```

to

```typescript
function getPayAmount() {
  if (isDead) return deadAmount();
  if (isSeparated) return separatedAmount();
  if (isRetired) return retiredAmount();
  return normalPayAmount();
}
```

**Motivation**

- It shows conditional branch are normal or unusual

### 以多态取代条件表达式（Replace Conditional with Polymorphism）

Using object oriented class instead of complex condition

```typescript
switch (bird.type) {
  case 'EuropeanSwallow':
    return 'average';
  case 'AfricanSwallow':
    return bird.numberOfCoconuts > 2 ? 'tired' : 'average';
  case 'NorwegianBlueParrot':
    return bird.voltage > 100 ? 'scorched' : 'beautiful';
  default:
    return 'unknown';
}
```

to

```typescript
class EuropeanSwallow {
  get plumage() {
    return 'average';
  }
}
class AfricanSwallow {
  get plumage() {
    return this.numberOfCoconuts > 2 ? 'tired' : 'average';
  }
}
class NorwegianBlueParrot {
  get plumage() {
    return this.voltage > 100 ? 'scorched' : 'beautiful';
  }
}
```

**Motivation**

- Make the separation more explicit

### 引入特例（Introduce Special Case）

Bring special check case to a single place

```typescript
if (aCustomer === "unknown") {
  customerName = "occupant";
}
```

to

```typescript
class UnknownCustomer {
  get name() {
    return "occupant";
  }
}
```

**Motivation**

- Remove duplicate code
- Easy to add additional behavior to special object

### 引入断言（Introduce Assertion）

Make the assumption explicit by writing an assertion

```typescript
if (this.discountRate) {
  base = base - (this.discountRate * base);
}
```

to

```typescript
assert(this.discountRate >= 0);
if (this.discountRate) {
  base = base - (this.discountRate * base);
}
```

**Motivation**

- Reader can understand the assumption easily
- Help in debugging

## 重构API（Refactoring APIS）

### 将查询函数和修改函数分离（Separate Query from Modifier）

Separate function that returns a value (query only) and function with side effects (example: modify data)

```typescript
function alertForMiscreant (people) {
  for (const p of people) {
    if (p === "Don") {
      setOffAlarms();
      return "Don";
    }
    if (p === "John") {
      setOffAlarms();
      return "John";
    }
  }
  return "";
}
```

to

```typescript
function findMiscreant (people) {
  for (const p of people) {
    if (p === "Don") {
      return "Don";
    }
    if (p === "John") {
      return "John";
    }
  }
  return "";
}
function alertForMiscreant (people) {
  if (findMiscreant(people) !== "") setOffAlarms();
}
```

**Motivation**

- Immutable function (query only) is easy to test and reuse

### 函数参数化（Parameterize Function）

Combine function with similar logic and different literal value

```typescript
function tenPercentRaise(aPerson) {
  aPerson.salary = aPerson.salary.multiply(1.1);
}
function fivePercentRaise(aPerson) {
  aPerson.salary = aPerson.salary.multiply(1.05);
}
```

to

```typescript
function raise(aPerson, factor) {
  aPerson.salary = aPerson.salary.multiply(1 + factor);
}
```

**Motivation**

- Increase usefulness of the function

### 移除标记参数（Remove Flag Argument）

Remove _literal_ flag argument by clear name functions

```typescript
function setDimension(name, value) {
  if (name === 'height') {
    this._height = value;
    return;
  }
  if (name === 'width') {
    this._width = value;
    return;
  }
}
```

to

```typescript
function setHeight(value) { this._height = value; }
function setWidth(value) { this._width = value; }
```

**Motivation**

- Easy to read and understand code
- Be careful if flag argument appears more than 1 time in the function, or is passed to further function

### 保持完整对象（Preserve Whole Object）

Passing whole object instead of multiple parameters

```typescript
const low = aRoom.daysTempRange.low;
const high = aRoom.daysTempRange.high;
if (aPlan.withinRange(low, high)) {}
```

to

```typescript
if (aPlan.withInRange(aRoom.daysTempRange)) {}
```

**Motivation**

- Shorter parameter list
- Don't need to add additional parameter if function needs more data in the future
- Be careful if function and object are in different modules, which make tight coupling if we apply this refactor

### 以查询取代参数（Replace Parameter with Query）

```typescript
availableVacation(anEmployee, anEmployee.grade);

function availableVacation(anEmployee, grade) {
  // calculate vacation...
}
```

to

```typescript
availableVacation(anEmployee)

function availableVacation(anEmployee) {
  const grade = anEmployee.grade;
  // calculate vacation...
}
```

**Motivation**

- Shorter list of parameters
- Simpler work for the caller (because fewer parameters)
- Be careful because it can increase function's dependency

### 以参数取代查询（Replace Query with Parameter）

Replace internal reference with a parameter

```typescript
targetTemperature(aPlan)

function targetTemperature(aPlan) {
  currentTemperature = thermostat.currentTemperature;
  // rest of function...
}
```

to

```typescript
targetTemperature(aPlan, thermostat.currentTemperature);

function targetTemperature(aPlan, currentTemperature) {
  // rest of function...
}
```

**Motivation**

- Reduce function's dependency
- Create more pure functions

### 移除设值方法（Remove Setting Method）

Make a field immutable by removing setting method

```typescript
class Person {
  get name() {...}
  set name(aString) {...}
}
```

to

```typescript
class Person {
  get name() {...}
}
```

### 以工厂函数取代构造方法（Replace Constructor with Factory Function）

```typescript
leadEngineer = new Employee(document.leadEngineer, 'E');
```

to

```typescript
leadEngineer = createEngineer(document.leadEngineer);
```

**Motivation**

- You want to do more than simple construction when you create an object.

### 以命令取代函数（Replace Function with Command）

Encapsulate function into its own object

```typescript
function score(candidate, medicalExam, scoringGuide) {
  let result = 0;
  let healthLevel = 0;
  // long body code
}
```

to

```typescript
class Scorer {
  constructor(candidate, medicalExam, scoringGuide) {
    this._candidate = candidate;
    this._medicalExam = medicalExam;
    this._scoringGuide = scoringGuide;
  }

  execute() {
    this._result = 0;
    this._healthLevel = 0;
    // long body code
  }
}
```

**Motivation**

- You want to add complimentary operation, such as undo
- Can have richer lifecycle
- Can build customization such as inheritance and hooks
- Easily break down a complex function to simpler steps

### 以函数取代命令（Replace Command with Function）

```typescript
class ChargeCalculator {
  public constructor (customer, usage){
    this._customer = customer;
    this._usage = usage;
  }

  public execute() {
    return this._customer.rate * this._usage;
  }
}
```

to

```typescript
function charge(customer, usage) {
  return customer.rate * usage;
}
```

**Motivation**

- Function call is simpler than command object

## 处理继承关系（Dealing With Inheritance）

### 方法上移（Pull Up Method）

Move similar methods in subclass to superclass

```typescript
class Employee {...}

class Salesman extends Employee {
  get name() {...}
}

class Engineer extends Employee {
  get name() {...}
}
```

to

```typescript
class Employee {
  get name() {...}
}

class Salesman extends Employee {...}
class Engineer extends Employee {...}
```

**Motivation**

- Eliminate duplicate code in subclass
- If two methods has similar workflow, consider using Template Method Pattern

### 字段上移（Pull Up Field）

Pull up similar field to superclass to remove duplication

```typescript
class Employee {...}

class Salesman extends Employee {
  private name:string;
}

class Engineer extends Employee {
  private name:string;
}
```

to

```typescript
class Employee {
  protected name:string;
}

class Salesman extends Employee {...}
class Engineer extends Employee {...}
```

### 构造方法本体上移（Pull Up Constructor Body）

You have constructors on subclasses with mostly identical bodies.
Create a superclass constructor; call this from the subclass methods

```typescript
class Party {...}

class Employee extends Party {
  constructor(name, id, monthlyCost) {
    super();
    this._id = id;
    this._name = name;
    this._monthlyCost = monthlyCost;
  }
}
```

to

```typescript
class Party {
  constructor(name){
    this._name = name;
  }
}

class Employee extends Party {
  constructor(name, id, monthlyCost) {
    super(name);
    this._id = id;
    this._monthlyCost = monthlyCost;
  }
}
```

### 方法下移（Push Down Method）

If method is only relevant to one subclass, moving it from superclass to subclass

```typescript
class Employee {
  get quota {...}
}

class Engineer extends Employee {...}
class Salesman extends Employee {...}
```

to

```typescript
class Employee {...}
class Engineer extends Employee {...}
class Salesman extends Employee {
  get quota {...}
}
```

### 字段下移（Push Down Field）

If field is only used in one subclass, move it to those subclasses

```typescript
class Employee {
  private quota:string;
}

class Engineer extends Employee {...}
class Salesman extends Employee {...}
```

to

```typescript
class Employee {...}
class Engineer extends Employee {...}

class Salesman extends Employee {
  protected quota:string;
}
```

### 以子类取代类型码（Replace Type Code with Subclasses）

```typescript
function createEmployee(name, type) {
  return new Employee(name, type);
}
```

to

```typescript
function createEmployee(name, type) {
  switch (type) {
    case "engineer": return new Engineer(name);
    case "salesman": return new Salesman(name);
    case "manager":  return new Manager (name);
  }
}
```

**Motivation**

- Easily to apply Replace Conditional with Polymorphism later
- Execute different code depending on the value of a type

### 移除子类（Remove Subclass）

You have subclasses do to little. Replace the subclass with a field in superclass.

```typescript
class Person {
  get genderCode() {return "X";}
}
class Male extends Person {
  get genderCode() {return "M";}
}
class Female extends Person {
  get genderCode() {return "F";}
}
```

to

```typescript
class Person {
  get genderCode() {return this._genderCode;}
}
```

### 提炼超类（Extract Superclass）

If 2 classes have similar behaviors, create superclass and move these behaviors to superclass

```typescript
class Department {
  get totalAnnualCost() {...}
  get name() {...}
  get headCount() {...}
}

class Employee {
  get annualCost() {...}
  get name() {...}
  get id() {...}
}
```

to

```typescript
class Party {
  get name() {...}
  get annualCost() {...}
}

class Department extends Party {
  get annualCost() {...}
  get headCount() {...}
}

class Employee extends Party {
  get annualCost() {...}
  get id() {...}
}
```

**Motivation**

- Remove duplication
- Prepare for Replace Superclass with Delegate refactor

### 折叠继承关系（Collapse Hierarchy）

Merge superclass and subclass when there are no longer different enough to keep them separate

```typescript
class Employee {...}
class Salesman extends Employee {...}
```

to

```typescript
class Employee {...}
```

### 以委托取代子类（Replace Subclass with Delegate）

"Favor object composition over class inheritance" (where composition is effectively the same as delegation

```typescript
class Order {
  get daysToShip() {
    return this._warehouse.daysToShip;
  }
}

class PriorityOrder extends Order {
  get daysToShip() {
    return this._priorityPlan.daysToShip;
  }
}
```

to

```typescript
class Order {
  get daysToShip() {
    return (this._priorityDelegate)
      ? this._priorityDelegate.daysToShip
      : this._warehouse.daysToShip;
  }
}

class PriorityOrderDelegate {
  get daysToShip() {
    return this._priorityPlan.daysToShip;
  }
}
```

**Motivation**

- If there are more than 1 reason to vary something, inheritance is not enough
- Inheritance introduce very close relationship

### 以委托取代超类（Replace Superclass with Delegate）

If functions of the superclass don’t make sense on the subclass, replace with with delegate

```typescript
class List {...}
class Stack extends List {...}
```

to

```typescript
class Stack {
  constructor() {
    this._storage = new List();
  }
}
class List {...}
```

**Motivation**

- Easier to maintain code
