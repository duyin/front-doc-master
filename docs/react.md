# React规范

## 样式分类

- 对于React项目，可以大致将样式分为四类：

1. 公共样式
2. 第三方样式
3. 容器样式，即container样式
4. 组件样式，即component样式

前两类样式的管理与传统前端项目并无差异，React项目的重点在于后两类样式的管理。

## 公共样式

主要包括：

1. reset——样式重置及设置默认值，通常包括normalize.css和base.css，可根据需求定制
2. layout——项目主体框架布局的相关样式
3. variable——存放sass变量，主要包括各种主题颜色、按钮颜色
4. mixin——可复用的样式片段，包括清除浮动、圆角边框、文本溢出省略显示、文本强制换行

### 引入方式：

reset样式在入口文件index.html中通过link标签引入，layout也可以在index.html引入。如果在layout中使用sass，可以与其他文件统一放在styles文件夹中，在index.js中引入。对于variable和mixin，同样放在styles文件夹中，如果文件体积较小，可以合并成一个文件。

variable.scss

```css
// 主色
$primary-color          : #5a8def;
// 标准色
$green                  : #117511;
$red                    : #950505;
$blue                   : #5a8def;
// 文字颜色、标题颜色、背景颜色、字体大小
$body-background        : #fff;
$text-color             : #666;
$text-color-secondary   : #999;
$font-size-sm           : 12px;
$font-size-base         : 12px;
$font-size-lg           : 14px;
// 边框颜色以及圆角
$border-color-base      : #d9d9d9;        
$border-color-split     : #e9e9e9;        
$border-base            : 1px solid #d9d9d9;
$border-split           : 1px solid #e9e9e9;
$border-radius-base     : 0px;
$border-radius-lg       : 4px;
// 行高
$line-height-sm         : 28px;
$line-height-normal     : 30px;
$line-height-lg         : 36px;
// 间距
$space-sm               : 5px;
$space-base             : 10px;
$space-lg               : 20px;
```
mixin.scss

```css
// 清除浮动
@mixin clearfix() {
    &:before,
    &:after {
        content: "";
        display: table;
    }
    &:after {
        clear: both;
    }
}
.container {
    @include clearfix;
}
// 圆角边框
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
     -moz-border-radius: $radius;
      -ms-border-radius: $radius;
          border-radius: $radius;
}
.box {
    @include border-radius(10px);
}
// 文本溢出省略显示
@mixin text-ellipsis () {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}
```

## 第三方样式

- 主要是第三方类库的依赖样式，一般通过link标签引入。

### 引入方式：
    
    在index.html通过link标签引入

## 容器样式

- 容器即container，一般不为container单独编写样式文件，将所有容器的样式提取到一个文件中（暂定为container.scss，放在styles文件夹中），这样可以避免样式污染，提高代码复用性。
- 类名命名采用类BEM的方式（开发人员表示不太习惯传统BEM命名，所以进行了改进），在项目开始前，前端开发人员集中对页面进行统一分析，分解为模块并命名。之后添加新类名要与其他开发人员统一确认，并保证无重名。

### 引入方式：
    放在styles文件夹中，在入口index.js引入

类BEM命名

```css
// 主要由三部分组成：块名、元素名、状态
.blockName-elName.modifier
// 例
.shopCart
.shopCart-title
.shopCart-item
.shopCart-item.selected
.menu
.menu-item
.menu-item.active
```

## 组件样式

- 根据React的组件化开发思想，同时为了避免CSS的全局作用域的影响，对于组件即component的样式，我们采用css-in-js的方案。
- 我们的项目中使用的是styled-components，它是目前 React 样式方案中最受关注的一种，它既具备了 css-in-js 的模块化与参数化优点，又完全使用CSS的书写习惯，不会引起额外的学习成本。

Styled-components


```js
import React from 'react';
import styled from 'styled-components';
// Title组件将生成一个字体大小1.5em，居中对齐，红色文字的h1标签
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: red;
`;
//Wrapper组件将生成一个内边距为4em，背景颜色为白色的section标签
const Wrapper = styled.section`
  padding: 4em;
  background: white;
`;
// 使用方法和正常的React组件一样
<Wrapper>
  <Title>Hello World, this is my first styled component!</Title>
</Wrapper>
```

##  注释

## (1) 文件顶部的注释，包括描述、作者、日期

```js
/**
 * @description xxxxxx
 * @author chengfeng
 * @since 19/05/21
 */
```

## (2) 模块的注释

```js
/**
 * 拷贝数据
 * @param  {*}  data   要拷贝的源数据
 * @param  {boolean} [isDeep=false] 是否深拷贝，默认浅拷贝
 * @return {*}         返回拷贝后的数据
 */

```

## (3) 业务代码注释

```js
/*业务代码注释*/
```
## (4) 变量注释

```js
interface IState {
  // 名字
  name: string;
  // 电话
  phone: number;
  // 地址
  address: string;
}
```

##  引用组件顺序

- 先引用外部组件库,,再引用当前组件块级组件, 然后是 common 里的公共函数库最后是 css 样式

```js
import * as React from 'react';
import { Dropdown, Menu, Icon } from 'antd';
import Header from './Header';
import toast from 'common/toast';
import './index.less';
```

##  引号

- 使用单引号,或者 es6 的反引号

## 缩进

- 使用两个空格

```js
const handleCheck = () => {
  onCancel && onCancel();
  onClose && onClose();
};
```

## 分号

- 除了代码块的以外的每个表达式后必须加分号。

##  括号

- 下列关键字后必须有大括号（即使代码块的内容只有一行）：if, else, for, while, do, switch, try, catch, finally, with。

```js
// not good
if (condition) doSomething();

// good
if (condition) {
  doSomething();
}
```
##  空格

- 二元和三元运算符两侧必须有一个空格，一元运算符与操作对象之间不允许有空格。

```js// bad
++ x;
y ++;
z = x?1:2;

// good
++x;
y++;
z = x ? 1 : 2;
```
- 用作代码块起始的左花括号 { 前必须有一个空格。

```js
// bad
if (condition){
}

while (condition){
}

function funcName(){
}

// good
if (condition) {
}

while (condition) {
}

function funcName() {
}

```
- if / else / for / while / function / switch / do / try / catch / finally 关键字后，必须有一个空格。

```js
// bad
if(condition) {
}

while(condition) {
}

(function() {
})();

// good
if (condition) {
}

while (condition) {
}

(function () {
})();
```

- 在对象创建时，属性中的 : 之后必须有空格，: 之前不允许有空格。

```js
// bad
var obj = {
    a : 1,
    b:2,
    c :3
};

// good
var obj = {
    a: 1,
    b: 2,
    c: 3
};
```

## 换行

- 每个独立语句结束后必须换行。
- 在函数声明、函数表达式、函数调用、对象创建、数组创建、for 语句等场景中，不允许在 , 或 ; 前换行

```js
// bad
var obj = {
    a: 1
    , b: 2
    , c: 3,
};

function test()
{
    ...
}
for (const key in object)
 {
  if (object.hasOwnProperty(key)) {
    const element = object[key];

  }
}
// good
var obj = {
    a: 1,
    b: 2,
    c: 3,
};

function test() {
    ...
}

for (const key in object) {
  if (object.hasOwnProperty(key)) {
    const element = object[key];

  }
}
```
- 下列关键字后：else, catch, finally 不需要换行

```js
// bad
if (condition) {
    ...
}
else {
    ...
}

try {
    ...
}
catch (e) {
    ...
}
finally {
    ...
}


// good
if (condition) {
    ...
} else {
    ...
}

try {
    ...
} catch (e) {
    ...
} finally {
    ...
}
```

## 数组、对象

- 对象属性名不需要加引号；
- 对象以缩进的形式书写，不要写在一行；
- 数组最后不要有逗号。
- 对象最后要有逗号。

```js

// bad
const a = {
    'b': 1
};

const a = {b: 1};

const a = {
    b: 1,
    c: 2
};
const arr = [1, 2, 3, 4,];

// good
const a = {
    b: 1,
    c: 2,
};

const arr = [1, 2, 3, 4];
```

## 命名

- 类名: 大驼峰式风格，字母和数字，例如：AbcTest。禁止汉字、特殊符号，禁止非大驼峰式风格。
- 函数名: 小驼峰式风格，字母和数字，例如：abcTest。禁止汉字、特殊符号，禁止非小驼峰式风格，例如snake_case等。
- 变量名: 同函数名。
- 常量: 全大写风格，大写字母、数字和下划线，单词之间以下划线分隔，例如：ABC_TEST。禁止汉字、特殊符号、小写字母。
- 使用 onXxx 形式作为 props 中用于回调的属性名称。

```js
interface IProps {
  onClose?: () => void;
  onOk?: (item: Record<string, any>) => void;
}
```

- 组件内的事件函数使用 handle 开头尾,handleCheckBtn。
- 使用 withXxx 形式的词作为高阶组件的名称。
- 接口命名前面带上 I 表示 interface

```js
interface IProps {}
interface IState {}
```
## 类型断言

```js
// bad
function getLength(something: string | number): number {
    return something.length;
}

// index.ts(2,22): error TS2339: Property 'length' does not exist on type 'string | number'.
//   Property 'length' does not exist on type 'number'.

// bad 
function getLength(something: string | number): number {
    if ((<string>something).length) {
        return (<string>something).length;
    } else {
        return something.toString().length;
    }
}

// good
function getLength(something: string | number): number {
  if (typeof something === 'string') {
    return something.length;
  } else {
    return something.toString().length;
  }
}

```

## interface声明顺序

- 日常用到比较多的是四种，只读参数放第一位，必选参数第二位，可选参数次之，不确定参数放最后

```js
interface iProps {
  readonly x: number;
  readonly y: number;
  name: string;
  age: number;
  height?: number;
  [propName: string]: any;
}
```

## ts好用的相关工具泛型

- Record<string,any> 用这个来声明对象结构的类型

```js
用于定义一个javascript的对象，key是字符串，value是任意类型
const people:Record<string,any> = {
    name: 'chengfeng',
    age: 10
}
```
###  仅当初始 state 需要从 props 计算得到的时候，才将 state 的声明放在构造函数中，其它情况下使用静态属性声明 state,并且一般情况下不要将 prop 传给 state

```js
// bad
constructor (){
  this.setState({ people: this.props.people })
}

// good
state: IState = {
  people: {},
};
```

## 渲染默认值

- 添加非空判断可以提高代码的稳健性,例如后端返回的一些值,可能会出现不存在的情况，应该要给默认值.

```js
// bad
render(){
  {name}
}

// good
render(){
  {!!name || '--'}
}

```
- 还有一种情况，就是本来后端应该返回一个数组给你，但是数据库取不到数据，可能后端给你返回了null,然后前端null.length。这样就gg了

```js
// bad
const { list, totalCount } = await getPeopleList(keyword, page, pageSize);
list 可能是null或者undefined
list.length将直接导致前端报错

this.setState({
  status: STATUS.READY,
  apps: list,
  total: totalCount,
  page: page,
});


// good 
const { list, totalCount } = await getPeopleList(keyword, page, pageSize);
this.setState({
  status: STATUS.READY,
  apps: list || [],
  total: totalCount || 0,
  page: page,
});

```
## 数据格式转换

- 1.把字符串转整型可以使用+号

```js
let maxPrice = +form.maxPrice.value;
let maxPrice = Number(form.maxPrice.value);
```
- 2.转成 boolean 值用!!

```js
let mobile = !!ua.match(/iPhone|iPad|Android|iPod|Windows Phone/);

```

## 判断条件真假

js 中以下为假,其他情况为真

- false
- null
- undefined
- 0
- '' (空字符串)
- NaN

## 简单组件可以使用函数代替


```js
// bad
class Listing extends React.Component {
  render() {
    return <div>{this.props.hello}</div>;
  }
}

// good
function Listing({ hello }) {
  return <div>{hello}</div>;
}
```
## input 输入框使用 trim()

```js
// bad
let searchContent = form.search.value;

// good
let searchContent = form.search.value.trim();
```
##  使用 location 跳转前需要先转义

```js

// bad
window.location.href = redirectUrl + '?a=10&b=20';

// good
window.location.href = redirectUrl + encodeURIComponent('?a=10&b=20');
```

##  key

- 对于组件中的 key 优化，起到最大化重用 dom

```js
//bad
this.state.dataAry.map((item, index) => {
  return <span key={index} />;
});

//good
this.state.dataAry.map(item => <span key={item.id} />);
```

## for-in 中一定要有 hasOwnProperty 的判断（即禁止直接读取原型对象的属性）

```js
//bad
const arr = [];
const key = '';

for (key in obj) {
  arr.push(obj[key]);
}

//good
const arr = [];
const key = '';

for (key in obj) {
  if (obj.hasOwnProperty(key)) {
    arr.push(obj[key]);
  }
}

```

## setState有三种用法

```js
// 对象
this.setState({

})

// 函数，一般是用于在setState之前做一些操作
this.setState(
  () => {
    // TODO
    console.log('')
    return {
      a:300
    }
  }
)

// 第二个参数，一般是用于在setState之后做一些操作
this.setState({
  a:300
}, () => {
  // TODO
})
```

## setState可能是同步的

- setState 在react里的合成事件和钩子函数中是“异步”的。
- setState 在原生事件和 setTimeout 中是同步的。

## 不要在 setState 前面加 await

- setState 前面也是可以带 await 的，会变成同步设置状态,但这是一种巧合，不确定未来哪个版本就不支持了，为了遵循 react 框架的设计原则，我们使用回掉函数的形式。

```js
// bad
func = async (name, value, status) => {
  await this.setState({
    name
  });
  // TODO
};

// good
func = (name, value, status) => {
  this.setState(
    {
      name
    },
    () => {
      // TODO
    }
  );
};
```

##  阻止事件默认行为

- 在 React 中你不能通过返回 false 来阻止默认行为。必须明确调用 preventDefault 。

## 防止 xss 攻击

- input，textarea 等标签，不要直接把 html 文本直接渲染在页面上,使用 xssb 等过滤之后再输出到标签上;

```js
import { html2text } from 'xss';
render(){
  <div
  dangerouslySetInnerHTML={{
    __html: html2text(htmlContent)
  }}
/>
}
```

## 第三方库函数的使用

- 用 try catch 包裹，防止第三方库的出现错误，导致整个程序崩溃

```js
/*
 * Echart 用于代绘制图表，但当其自身发生错误时，可能影响到业务代码的执行
 */
// bad
const iniDom = document.getElementById('init-container');
const echartObj = echarts.init(iniDom);
this.setState(
  {
    echartObj
  },
  () => {
    const { echartObj } = this.state;
    // 更新图表
    echartObj.setOption(CHART_CONFIG, true);
  }
);

// good
try {
  const iniDom = document.getElementById('init-container');
  const echartObj = echarts.init(iniDom);
  this.setState(
    {
      echartObj
    },
    () => {
      const { echartObj } = this.state;
      // 更新图表
      echartObj.setOption(CHART_CONFIG, true);
    }
  );
} catch (error) {
  // TODO
}
```

##  减少魔法数字

- 写代码的时候尽量减少一些未知含义的数字，尽量用英文单词。例如type === 0的时候做了一些操作，让人不知所以然。

```js
// bad
if (type !== 0) {
  // TODO
}

// good
const STATUS: Record<string, any> = {
  READY: 0,
  FETCHING: 1,
  FAILED: 2
};

if (type === STATUS.READY) {
  // TODO
}

// best
enum STATUS {
  // 就绪
  READY = 0,
  // 请求中
  FETCHING = 1,
  // 请求失败
  FAILED = 2,
}

```

##  if else 等判断太多了，后期难以维护。

- 个人觉得if else 嵌套深看起来也不会太难受，难受的是，项目迭代久之后，自己都忘记曾经写过这些代码，而且类型多或者不确定有什么类型，是否后期还会加的情况下，改起来就非常复杂了，而且很容易踩坑和背锅。
- 用配置取代if嵌套，大概就是抽离一个config.ts出来，里面放一些配置。

```js
例如你的业务代码里面，会根据不同url参数，代码会执行不同的逻辑.
/info?type=wechat&uid=123456&
const qsObj = qs(window.location.url)
const urlType = qsObj.type
// bad 
if (urlType === 'wechat') {
    doSomeThing()
} else if () {
    doSomeThing()
} else if () {
    doSomeThing()
} else if () {
    doSomeThing()
}

// good 
config.t
const urlTypeConfig: Record<string, typeItem> = {
  'wechat': { // key 就是对应的type
    name: 'wechat', 
    show: ['header', 'footer', 'wechat'] // 展示什么，可能是异步的
    pession: ['admin'], // 权限是什么，可能是异步的
  },
  'zhifubao': { // key 就是对应的type
    name: 'zhifubao', 
    show: ['header', 'footer', 'zhifubao'] // 展示什么，可能是异步的
    pession: ['admin'], // 权限是什么，可能是异步的
  },
}

// 业务逻辑
const qsObj = qs(window.location.url)
const urlType = qsObj.type
Object.keys(urlTypeConfig).forEach(item => {
  if(urlType === item.type) {
    doSomeThing(item.show)
  }
})

```

## a标签安全问题

- 使用a标签打开一个新窗口过程中的安全问题。新页面中可以使用window.opener来控制原始页面。如果新老页面同域，那么在新页面中可以任意操作原始页面。如果是不同域，新页面中依然可以通过window.opener.location，访问到原始页面的location对象

- 在带有target="_blank"的a标签中，加上rel="noopener"属性。如果使用window.open的方式打开页面，将opener对象置为空。

```js
var newWindow = window.open();
newWindow.opener = null;

```
## 前端不要操作cookie

- 在做一些前后端鉴权的时候，后端应该开启domain,secure,httponly严格模式，禁止前端操作cookie，防止csrf攻击。