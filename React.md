## <font style="color:rgb(31, 35, 40);">描述UI</font>
### 组件<font style="color:rgb(31, 35, 40);">Component</font>
组件：**<font style="color:rgb(35, 39, 47);">可复用的 UI 元素</font>**

+ <font style="color:rgb(35, 39, 47);">一个满足两个条件的 js </font>**<font style="color:rgb(35, 39, 47);">function</font>**
    - **<font style="color:rgb(35, 39, 47);">return JSX元素</font>**
    - <font style="color:rgb(35, 39, 47);">名字以大写字母开头</font>
        * <font style="color:rgb(35, 39, 47);">React识别标签<>时，小写开头认为是HTML标签，大写开头认为是React组件</font>

### <font style="color:rgb(35, 39, 47);">组件的导入导出</font>
<img src="https://intranetproxy.alipay.com/skylark/lark/0/2023/png/88656377/1697427652763-3e719c81-dc70-4f08-b631-3a9d284b50e0.png" width="686" title="" crop="0,0,1,1" id="ud04e8c6a" class="ne-image">

<font style="color:rgb(35, 39, 47);">一个文件里有且仅有一个 默认导出，但是可以有任意多个 具名导出。</font>

<font style="color:rgb(35, 39, 47);">通常，文件中仅包含一个组件时，选择默认导出；文件中包含多个组件或某个值需要导出时，则会选择具名导出 或 混合：</font>

```jsx
// a file
import Gallery from './Gallery.js';
import { Profile } from './Gallery.js';

// Gallery.js
export function Profile() {
  return (
    <img
      src="https://i.imgur.com/QIrZWGIs.jpg"
      alt="Alan L. Hart"
    />
  );
}

export default function Gallery() {
  return (
    <section>
      <h1>了不起的科学家们</h1>
      <Profile />
      <Profile />
      <Profile />
    </section>
  );
}
```

### JSX
_什么是JSX？_

+ 一种语法规则
+ 允许你在 JavaScript 中编写类似 HTML 的标签，从而使渲染的逻辑和内容可以写在一起。
+ 允许你在标签中使用 JavaScript 编写逻辑或者引用动态的属性（使用{}）



_为什么React使用JSX？_

+ <font style="color:rgb(35, 39, 47);">多年以来，web 开发者都是将网页内容存放在 HTML 中，样式放在 CSS 中，而逻辑则放在 JavaScript 中 —— 通常是在不同的文件中</font>
+ <font style="color:rgb(35, 39, 47);">由于渲染逻辑和标签是紧密相关的，所以 React 将它们存放在一个组件中</font>

<font style="color:rgb(35, 39, 47);"></font>

_<font style="color:rgb(35, 39, 47);">一些规则：</font>_

**1.只能返回一个根元素**

    - why？A：JSX元素实际会被转化为 JavaScript 对象，你不能在一个函数中返回多个对象
    - <font style="color:rgb(35, 39, 47);">可以用 </font><></>（<font style="color:rgb(35, 39, 47);"> </font><Fragment><font style="color:rgb(35, 39, 47);"> </font>）<font style="color:rgb(35, 39, 47);"> 包裹多个元素，这不会在 HTML 结构中添加额外节点，就像元素没有被组合一样。</font>

<font style="color:rgb(35, 39, 47);">2.标签必须闭合</font>

<font style="color:rgb(35, 39, 47);">3.使用驼峰式命名法给 所有 大部分属性命名</font>

```jsx
<img 
  src="https://i.imgur.com/yXOvdOSs.jpg" 
  alt="Hedy Lamarr" 
  className="photo"
/>
```

    - <font style="color:rgb(35, 39, 47);">JSX 最终会被转化为 JavaScript，而 JSX 中的属性也会变成 JavaScript 对象中的键值对，要遵守JS命名规范</font>
    - <font style="color:rgb(35, 39, 47);">某些属性由于历史原因，命名中会存在</font><font style="color:rgb(35, 39, 47);background-color:#E7E9E8;"> - </font><font style="color:rgb(35, 39, 47);">符号</font>

**<font style="color:rgb(35, 39, 47);">4.{}中编写js</font>**

    - <font style="color:rgb(35, 39, 47);">这里主要写：</font>**<font style="color:rgb(35, 39, 47);">传入变量、表达式</font>**<font style="color:rgb(35, 39, 47);">（例如isA?<A/>:<B/>、isA && <A/>）、</font>**<font style="color:rgb(35, 39, 47);">函数（返回节点</font>**<font style="color:rgb(35, 39, 47);">，例如createPortal函数），js逻辑代码要往return前面写</font>
    - <font style="color:rgb(35, 39, 47);">内联CSS时，常常出现双大括号</font>

```jsx
<ul style={
  {
    backgroundColor: 'black',
    color: 'pink'
  }
}>
```

        * <font style="color:rgb(35, 39, 47);">在 JSX 中传递对象，要包裹{}，而对象本身用{}写的</font>
        * <font style="color:rgb(35, 39, 47);">所以</font>**{{****<font style="color:rgb(35, 39, 47);"> 和 </font>****}}****<font style="color:rgb(35, 39, 47);">只不过是包在大括号里的一个对象</font>**
        * **<font style="color:rgb(35, 39, 47);">内联 style 属性 使用驼峰命名法编写。</font>**<font style="color:rgb(35, 39, 47);">例如，HTML <ul style="background-color: black"> 在你的组件里应该写成 <ul style={{ backgroundColor: 'black' }}>。</font>

### <font style="color:rgb(35, 39, 47);">props</font>
<font style="color:rgb(106, 115, 125);background-color:rgb(255, 251, 221);">不要在组件中定义组件</font>

<font style="color:rgb(106, 115, 125);background-color:rgb(255, 251, 221);">当子组件需要使用父组件的数据时，你需要 </font>[<font style="color:rgb(106, 115, 125);background-color:rgb(255, 251, 221);">通过 props 的形式进行传递</font>](https://zh-hans.react.dev/learn/passing-props-to-a-component)<font style="color:rgb(106, 115, 125);background-color:rgb(255, 251, 221);">，而不是嵌套定义。</font>

<font style="color:rgb(35, 39, 47);"></font>

<font style="color:rgb(35, 39, 47);">原生props->html标签的，例如src、alt等是<img>的props</font>

```html
<img
  src="https://i.imgur.com/1bX5QH6.jpg"
  alt="Lin Lanying"
  width={100}
  height={100}
  />
```

<font style="color:rgb(35, 39, 47);"></font>

<font style="color:rgb(35, 39, 47);">拓展->可以给自己定义的组件传props</font>

```jsx
// father
export default function Profile() {
  return (
    <Avatar
      person={{ name: 'Lin Lanying', imageId: '1bX5QH6' }}
      size={100}
      test='111'
      />
  );
}

// son
function Avatar({ person, size=100 }) { 
  // 解耦的写法,等价于从函数参数中读取属性
  // 可以为props设置默认值
  // ...
}
// 等价于
function Avatar(props) {
  let person = props.person;
  let size = props.size;
  // ...
}
```



**将组件作为props传递：**

此时，要传递的组件作为props的children属性

<font style="color:rgb(35, 39, 47);">例如，下面的 </font>Card<font style="color:rgb(35, 39, 47);"> 组件将接收一个被设为 </font><Avatar /><font style="color:rgb(35, 39, 47);"> 的 </font>children<font style="color:rgb(35, 39, 47);"> prop 并将其包裹在 div 中渲染：</font>

```jsx
import Avatar from './Avatar.js';

function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}

export default function Profile() {
  return (
    <Card>
      <Avatar
        size={100}
        person={{ 
          name: 'Katsuko Saruhashi',
          imageId: 'YfeOqp2'
        }}
      />
    </Card>
  );
}
```

这样 Card<font style="color:rgb(35, 39, 47);"> 组件</font>**<font style="color:rgb(35, 39, 47);">可以包裹任意嵌套内容</font>**<font style="color:rgb(35, 39, 47);">。它</font>**<font style="color:rgb(35, 39, 47);">不必“知道”</font>**<font style="color:rgb(35, 39, 47);">其中渲染的内容。</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2023/png/88656377/1697441650073-c565584f-fbec-4745-9a27-a60f81d58144.png" width="700" title="" crop="0,0,1,1" id="u1b764fe0" class="ne-image">

### 渲染列表
<font style="color:rgb(35, 39, 47);">由数组生成列表->使用 </font>[filter()](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)<font style="color:rgb(35, 39, 47);"> 筛选，使用 </font>[map()](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array/map)<font style="color:rgb(35, 39, 47);"> 把数组转换成组件数组</font>

```jsx
import { people } from './data.js';
import { getImageUrl } from './utils.js';
export default function List() {
  return <ul>{
    people
    .filter(person =>
      person.profession === '化学家'
    )
    .map(person =>
      <li key={person.id}>
        <img
          src={getImageUrl(person)}
          alt={person.name}
        />
        <p>
          <b>{person.name}:</b>
          {' ' + person.profession + ' '}
          因{person.accomplishment}而闻名世界
        </p>
      </li>
    )
  }</ul>;
}
```

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2023/png/88656377/1697445336501-d3327121-c354-46c5-a2da-1376d3728c2e.png" width="703" title="" crop="0,0,1,1" id="ua19d688d" class="ne-image">

<font style="color:rgb(33, 37, 41);"></font>

<font style="color:rgb(33, 37, 41);">在编写 JSX（JavaScript XML）时，当你</font>**<font style="color:rgb(33, 37, 41);">使用数组渲染列表或使用动态生成的元素</font>**<font style="color:rgb(33, 37, 41);">时，通常</font>**<font style="color:rgb(33, 37, 41);">需要为每个元素提供一个唯一的静态的 key 属性</font>**<font style="color:rgb(33, 37, 41);">。</font>

+ <font style="color:rgb(33, 37, 41);">key 用于帮助 React 识别列表中的每个元素，并进行高效的更新和重渲染。它有助于 React 跟踪每个元素的身份，以便在列表中进行插入、删除或重新排序时，能够正确地更新组件</font>
+ **<font style="color:rgb(33, 37, 41);">map() 里，要用 key 标识元素</font>**
+ <font style="color:rgb(33, 37, 41);">把数组项的索引当作 key</font>

```jsx
strings.map((str, index) => 
  <div key={index}>{str}</div>)
```

    - <font style="color:rgb(33, 37, 41);">如果你没有显式地指定 key ，React 会直接把数组项的索引当作 key</font>
    - <font style="color:rgb(33, 37, 41);">若数组是const的，那么这样ok</font>
    - <font style="color:rgb(33, 37, 41);"></font>_<font style="color:rgb(33, 37, 41);">若数组的顺序在插入、删除或者重新排序等操作中会发生改变，此时把索引顺序用作 key 值会产生一些微妙且令人困惑的 bug</font>_<font style="color:rgb(33, 37, 41);">。</font>
+ <font style="color:rgb(33, 37, 41);">组件不会把 key 当作 props 的一部分。Key 的存在只对 React 本身起到提示作用。</font>

### <font style="color:rgb(33, 37, 41);">保持组件纯粹</font>
保持组件纯粹是很重要的，这可以避免bug出现



组件函数应该是**纯函数（like y=2x）**

+ <font style="color:rgb(35, 39, 47);">对于相同的输入，返回</font>**<font style="color:rgb(35, 39, 47);">相同</font>**<font style="color:rgb(35, 39, 47);">的 JSX</font>
    - <font style="color:rgb(35, 39, 47);">各个组件之间的渲染互不干扰，渲染结果与渲染顺序无关</font>
+ **<font style="color:rgb(35, 39, 47);">不改变渲染前存在的：不改变函数作用域外的变量 或 在函数调用前创建的对象 </font>**
    - **<font style="color:rgb(35, 39, 47);">可以改函数内部变量</font>**
+ <font style="color:rgb(35, 39, 47);">在 React 中，你可以在渲染时读取三种输入：</font>[<font style="color:#117CEE;">props</font>](https://zh-hans.react.dev/learn/passing-props-to-a-component)<font style="color:#117CEE;">，</font>[<font style="color:#117CEE;">state</font>](https://zh-hans.react.dev/learn/state-a-components-memory)<font style="color:#117CEE;"> </font>和<font style="color:#117CEE;"> </font>[<font style="color:#117CEE;">context</font>](https://zh-hans.react.dev/learn/passing-data-deeply-with-context)<font style="color:rgb(35, 39, 47);">。你应该始终将这些输入视为</font>**<font style="color:rgb(35, 39, 47);">只读</font>**<font style="color:rgb(35, 39, 47);">。</font>
+ **<font style="color:rgb(35, 39, 47);">当你想根据用户输入更改某些内容时，你应该调用state的set函数</font>**

### 副作用
**副作用****<font style="color:rgb(18, 18, 18);">指的是与组件渲染结果无关的任何操作</font>**<font style="color:rgb(18, 18, 18);">，例如：</font>

1. <font style="color:rgb(18, 18, 18);">发送网络请求</font>
2. <font style="color:rgb(18, 18, 18);">修改 DOM 元素</font>
3. <font style="color:rgb(18, 18, 18);">访问本地存储</font>
4. <font style="color:rgb(18, 18, 18);">订阅或取消订阅事件</font>
5. <font style="color:rgb(18, 18, 18);">改变组件状态外的变量等</font>

<font style="color:rgb(18, 18, 18);">这些操作会影响组件的行为和状态，但是并不会直接影响渲染结果。在 React 中，应该</font>**<font style="color:rgb(18, 18, 18);">将副作用分离</font>**<font style="color:rgb(18, 18, 18);">出来，以便更好地控制组件的行为和状态。</font>

<font style="color:rgb(18, 18, 18);">通常，React 使用</font>**<font style="color:rgb(18, 18, 18);">hook函数</font>**<font style="color:rgb(18, 18, 18);">（如 useEffect）来处理副作用。在 useEffect 中，可以执行一些副作用操作，例如发送网络请求或订阅事件，以及在组件卸载时清除这些操作。这可以保持组件的一致性和可维护性。</font>

## 添加交互
### 用state响应输入


### 响应事件
**事件处理函数：**响应交互（如点击、悬停、表单输入框获得焦点等）时触发

+ <font style="color:rgb(35, 39, 47);">通常在你的组件 </font>**<font style="color:rgb(35, 39, 47);">内部</font>**<font style="color:rgb(35, 39, 47);"> 定义。</font>
    - <font style="color:rgb(35, 39, 47);">因此可以使用组件内的变量</font>
+ <font style="color:rgb(35, 39, 47);">名称以 </font>handle<font style="color:rgb(35, 39, 47);"> 开头，后跟事件名称。</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2023/png/88656377/1698224800837-230c82f3-bf1a-474b-a1a3-26b47c6844c8.png" width="736.8" title="" crop="0,0,1,1" id="ub9c6a350" class="ne-image">

<font style="color:rgb(35, 39, 47);"></font>

<font style="color:rgb(35, 39, 47);">在父组件中定义子组件的事件处理函数，则将</font>**<font style="color:rgb(35, 39, 47);">事件处理函数作为props传递</font>**

<font style="color:rgb(35, 39, 47);">内置组件（</font><button><font style="color:rgb(35, 39, 47);"> 和 </font><div><font style="color:rgb(35, 39, 47);">）仅支持 </font>[<font style="color:#117CEE;">浏览器事件名称</font>](https://zh-hans.react.dev/reference/react-dom/components/common#common-props)<font style="color:rgb(35, 39, 47);">，例如 </font>onClick<font style="color:rgb(35, 39, 47);">。但是，当你构建自己的组件时，你可以按你个人喜好命名事件处理函数的 prop。</font>

<font style="color:rgb(35, 39, 47);">按照惯例，事件处理函数 props 应该以 </font>on<font style="color:rgb(35, 39, 47);"> 开头，后跟一个大写字母。</font>

```javascript
export default function App() {
  return (
    <Toolbar
      onPlayMovie={() => alert('正在播放！')}
      onUploadImage={() => alert('正在上传！')}
    />
  );
}

function Toolbar({ onPlayMovie, onUploadImage }) {
  return (
    <div>
      <Button onClick={onPlayMovie}>
        播放电影
      </Button>
      <Button onClick={onUploadImage}>
        上传图片
      </Button>
    </div>
  );
}

function Button({ onClick, children }) {
  return (
    <button onClick={onClick}>
      {children}
    </button>
  );
}
```

**事件处理函数命名总结：**

+ 组件内定义-handle开头
+ 作为props传递的-on开头



**事件传播：**<font style="color:rgb(35, 39, 47);">事件会沿着树向上“冒泡”或“传播”，它从事件发生的地方开始，然后沿着树向上传播。</font>

**<font style="color:rgb(35, 39, 47);">点击子组件时，也会触发父组件的点击</font>**

<font style="color:rgb(35, 39, 47);">事件处理函数接收一个 </font>**<font style="color:rgb(35, 39, 47);">事件对象</font>**<font style="color:rgb(35, 39, 47);"> 作为唯一的参数。按照惯例，它通常被称为 </font>e<font style="color:rgb(35, 39, 47);"> ，代表 “event”（事件）。你可以使用此对象来读取有关事件的信息。</font>

<font style="color:rgb(35, 39, 47);">这个事件对象还允许你阻止传播。</font>**<font style="color:rgb(35, 39, 47);">在</font>**_**<font style="color:rgb(35, 39, 47);">子组件</font>**_**<font style="color:rgb(35, 39, 47);">的事件处理函数里调用</font>**_**<font style="color:rgb(35, 39, 47);"> </font>**__**e.stopPropagation()**_**，**_**<font style="color:rgb(35, 39, 47);">阻止事件传播到父组件</font>**_

```javascript
function Button({ onClick, children }) {
  return (
    <button onClick={e => {
      e.stopPropagation(); //去掉本条代码，点击播放电影，会先弹窗“正在播放！”，然后弹窗“点击了toolbar”
      onClick();
    }}>
      {children}
    </button>
  );
}

export default function Toolbar() {
  return (
    <div className="Toolbar" onClick={() => {
      alert('你点击了 toolbar ！');
    }}>
      <Button onClick={() => alert('正在播放！')}>
        播放电影
      </Button>
      <Button onClick={() => alert('正在上传！')}>
        上传图片
      </Button>
    </div>
  );
}
```

### state
<font style="color:rgb(18, 18, 18);">随时间变化的数据被称为状态（state），</font>**<font style="color:rgb(18, 18, 18);">当你希望组件在多次渲染间能记住变量的值，并且变量值改变时重新渲染->使用state</font>**

+ <font style="color:rgb(18, 18, 18);">普通的局部变量：</font><font style="color:rgb(35, 39, 47);">当 React 再次渲染这个组件时，它会从头开始渲染——</font>**<font style="color:rgb(35, 39, 47);">不会考虑</font>**<font style="color:rgb(35, 39, 47);">之前对局部变量的任何更改；更改局部变量</font>**<font style="color:rgb(35, 39, 47);">不会触发渲染</font>**<font style="color:rgb(35, 39, 47);">。</font>

<font style="color:rgb(18, 18, 18);"></font>

<font style="color:rgb(18, 18, 18);">Hooks ——</font>**<font style="color:rgb(18, 18, 18);">以 use 开头的函数</font>**<font style="color:rgb(18, 18, 18);">——只能在组件或</font>[<font style="color:#117CEE;">自定义 Hook</font>](https://zh-hans.react.dev/learn/reusing-logic-with-custom-hooks)<font style="color:rgb(18, 18, 18);"> 的最顶层调用。 你不能在条件语句、循环语句或其他嵌套函数内调用 Hook。</font>**<font style="color:rgb(18, 18, 18);">Hook可以处理很多特性</font>**<font style="color:rgb(18, 18, 18);">，state是其中一个（别的，例如useEffect）</font>

<font style="color:rgb(18, 18, 18);"></font>

<font style="color:rgb(18, 18, 18);">使用  </font>**<font style="color:rgb(18, 18, 18);">const [stateA，setStateA]=useState(初始值)  </font>**<font style="color:rgb(18, 18, 18);">来声明state</font>

<font style="color:rgb(18, 18, 18);"></font>

#### <font style="color:rgb(18, 18, 18);">在组件间共享state</font>
把state设置在父组件，将state和set state函数作为prop传入子组件

[https://zh-hans.react.dev/learn#sharing-data-between-components](https://zh-hans.react.dev/learn#sharing-data-between-components)

<font style="color:rgb(18, 18, 18);"></font>

**<font style="color:rgb(18, 18, 18);">state是隔离的 & 私有的</font>**

+ <font style="color:rgb(18, 18, 18);">渲染同一个组件两次，每个副本都会有完全隔离的 state（他们是分别存储的）</font>
+ <font style="color:rgb(35, 39, 47);">state 完全私有于声明它的组件。父组件无法更改它</font>
+ <font style="color:rgb(35, 39, 47);">可以向任何组件添加或删除 state，而不会影响其他组件</font>

### <font style="color:rgb(35, 39, 47);">在屏幕上显示组件的步骤</font>
1. **<font style="color:rgb(35, 39, 47);">触发</font>**<font style="color:rgb(35, 39, 47);"> 一次渲染</font>
    1. <font style="color:rgb(35, 39, 47);">两种原因会导致组件的渲染:</font>
        1. <font style="color:rgb(35, 39, 47);">组件的</font><font style="color:rgb(35, 39, 47);"> </font>**<font style="color:rgb(35, 39, 47);">初次渲染。</font>**
        2. <font style="color:rgb(35, 39, 47);">组件（或者其祖先之一）的 </font>**<font style="color:rgb(35, 39, 47);">状态发生了改变。</font>**
2. **<font style="color:rgb(35, 39, 47);">渲染</font>**<font style="color:rgb(35, 39, 47);"> 组件</font>
    1. <font style="color:rgb(35, 39, 47);">非初次渲染，react只会重渲染更新了的组件</font>
    2. <font style="color:rgb(35, 39, 47);">每次渲染时执行组件函数</font>
3. **<font style="color:rgb(35, 39, 47);">提交</font>**<font style="color:rgb(35, 39, 47);"> 到 DOM（</font><font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">Document Object Model，文档对象模型。是针对HTML和XML文档的一个编程接口，它表示了文档中的对象（比如元素、属性和文本），并提供了访问和操作这些对象的能力。浏览器环境下</font><font style="color:rgb(35, 39, 47);">）</font>
    1. <font style="color:rgb(35, 39, 47);">非初次渲染，react只会更改需要更新的DOM节点</font>
    2. <font style="color:rgb(35, 39, 47);">useEffect的函数体在提交阶段后执行，所以可以操作DOM节点</font>
4. <font style="color:rgb(35, 39, 47);">浏览器绘制</font>
    1. <font style="color:rgb(35, 39, 47);">在渲染完成并且 React 更新 DOM 之后，浏览器就会重新绘制屏幕</font>

<font style="color:rgb(35, 39, 47);"></font>

**<font style="color:rgb(35, 39, 47);">每次渲染时会完整的执行一遍组件函数</font>**<font style="color:rgb(35, 39, 47);">，如果说这其中有不必要的“开销较大的计算”（本次更新的数据不会影响这个计算，则实际上不需要再计算一次），可以用</font>**<font style="color:rgb(35, 39, 47);">useMemo函数（仅当依赖项变化时重新执行函数）</font>**<font style="color:rgb(35, 39, 47);">：</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725248245838-547a08bd-3bfc-4d02-bcc1-2b95ccedec0c.png" width="805.6" title="" crop="0,0,1,1" id="uf1e4cfc3" class="ne-image">

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725248275186-a97803d0-3d81-491e-8880-4eb6112ea182.png" width="883.2" title="" crop="0,0,1,1" id="u4888f51c" class="ne-image"><img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725248298467-22419fc8-e526-4dce-9fb3-8b5519b2d996.png" width="886.4" title="" crop="0,0,1,1" id="u91d40dd9" class="ne-image">

## 状态管理
### State
state就像快照，**每次渲染中有一张state的快照**  
state**初始化只在挂载（初次渲染）时执行，后续重新渲染不会重新初始化**



**setState需要传入一个新的对象（新的引用）**

+ <font style="color:rgb(51, 51, 51);background-color:rgb(249, 250, 255);">React 依赖对象引用的变化来检测state更新，所以相同的引用不会触发重新渲染</font>

```javascript
const [dotParams, setDotParams] = useState(
  {
    aimColor: '#00D994',
    aimSize: 0,
    aimTransparent: 0,
  }
);

<div className='dot' style={{ 
  opacity: dotParams.aimTransparent / 100,
  width: dotParams.aimSize,
  height: dotParams.aimSize,
}}></div>

// 这样更新，dot不会实时渲染
let tmp = dotParams;
tmp.aimColor = xxx;
setDotParams(tmp);

// 这样更新才是对的，需要创建一个新的对象
setDotParams({...dotParams, [key]: value});
```



什么数据应该是state：

+ state需要是绝对精简的
    - 考虑一些state的情况**组合**，是否会存在**没有意义**的情况。若存在，则表示**还能优化**
    - 考虑一些state是不是可以合并到一个state里表示，例如<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1727080797506-58753c1a-2765-4ab0-a5d0-17e79424a9a8.png" width="577.6" title="" crop="0,0,1,1" id="ub75f931d" class="ne-image">
    - 合并关联的state为一个对象类型的state
        * 当state们总是一起更新时，则合并他们到一个对象里
        * <img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1727091155976-5b4dd88b-c39c-4244-a968-79533991bd95.png" width="730.4" title="" crop="0,0,1,1" id="uc0a176db" class="ne-image">
        * 也应当尽量避免对象属性的深层嵌套，尽量扁平化，少一些层数
    - 考虑两个state是否描述的同样的信息，可以删除掉一个
+ <font style="color:rgb(35, 39, 47);">随时间推移保持不变 的不是state</font>
+ <font style="color:rgb(35, 39, 47);">通过 props 从父组件传递 的不是state</font>
+ <font style="color:rgb(35, 39, 47);">对于选择某个item这种的 UI 模式，请在 state 中保存 ID 或索引而不是对象本身。</font>
+ **<font style="color:rgb(35, 39, 47);">可基于现有 state 或者 props 进行计算 的不是state</font>**
    - <img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725246695770-59b7612e-dc02-4238-b9bb-f3f7e9c9e0b9.png" width="716.8" title="" crop="0,0,1,1" id="u0cbc6609" class="ne-image"><img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725246709741-b4e621e6-f45e-41fb-a241-84f975cf8749.png" width="704.8" title="" crop="0,0,1,1" id="u464e17e2" class="ne-image">

****

**setState后无法立刻取到最新值，**如果需要立刻获取最新值，应当在setState(newVal,()=>{})传入第二个参数，这个**回调函数**会在state真的更新后执行**，可以获取到最新state。**

+ <font style="color:rgb(51, 51, 51);background-color:rgb(249, 250, 255);">React会批量更新state：状态更新是异步的，意味着不会立即更新state，而是将更新操作放入一个队列中，稍后批量处理</font>
+ <font style="color:rgb(35, 39, 47);">执行顺序：</font>**<font style="color:rgb(35, 39, 47);">事件处理函数中的 所有 代码都运行完毕->更新state->引起重新渲染</font>**
+ 详见 [https://zh-hans.react.dev/learn/queueing-a-series-of-state-updates](https://zh-hans.react.dev/learn/queueing-a-series-of-state-updates)
+ 可参考 [https://juejin.cn/post/7066423854259765279](https://juejin.cn/post/7066423854259765279)



在组件间共享状态->状态提升：

+ 在父组件设置state，通过props传递给子组件
+ <font style="color:rgb(35, 39, 47);">考虑该将子组件视为“受控”（由 prop 驱动）或是“不受控”（由 state 驱动）是十分有益的。</font>



State的保存：

+ <font style="color:rgb(35, 39, 47);">状态是由 React 保存的。React</font>**<font style="color:rgb(35, 39, 47);"> 根据</font>**<font style="color:rgb(35, 39, 47);">组件在 </font>**<font style="color:rgb(35, 39, 47);">dom树形结构</font>**<font style="color:rgb(35, 39, 47);">中的位置，来跟踪哪些 state 属于哪个组件</font>
+ <font style="color:rgb(35, 39, 47);">当组件被删除时，他的state也会被删掉。在同一位置重新渲染该组件的话，该组件是从头被挂载，state 也是重新被初始化，不会保留之前的值。</font>
    - <img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1727580262707-752c594d-438d-4244-86c6-2726697458fb.png" width="226.4" title="" crop="0,0,1,1" id="u440c54f7" class="ne-image">这种写法，当show=false时，组件就被删除了，再次show的时候是重新挂载
+ 相同位置的相同组件，state会被保留
    - 见[https://zh-hans.react.dev/learn/preserving-and-resetting-state#same-component-at-the-same-position-preserves-state](https://zh-hans.react.dev/learn/preserving-and-resetting-state#same-component-at-the-same-position-preserves-state)
    - react理解的时候按最终ui树的样子（而不是编写代码时候的结构），若同位置还是相同的组件，那么他不用重新删除、挂载该组件，更新该组件的props就行
+ <font style="color:rgb(35, 39, 47);">相同位置对 不同 的组件类型进行切换，state会重置</font>
    - <font style="color:rgb(35, 39, 47);">因为react删除、重新挂载了组件</font>
+ **<font style="color:rgb(35, 39, 47);">总结：判断state会不会被保留->通过dom树形结构，看组件是否有被删除。删除了则也删除了state</font>**
+ **<font style="color:rgb(35, 39, 47);">当同一位置的同一组件在key不同时，数据需要相互独立时，则可以声明key来区分state。声明key后，react会根据key来匹配对应的state，位置变化了，state也不会重置。</font>**
    - <font style="color:rgb(35, 39, 47);">例子：</font>[https://zh-hans.react.dev/learn/preserving-and-resetting-state#option-2-resetting-state-with-a-key](https://zh-hans.react.dev/learn/preserving-and-resetting-state#option-2-resetting-state-with-a-key)

### 管理状态逻辑-Reducer
更系统、避免重复代码的管理状态更新->reducer

状态更新多时可以考虑用useReducer替换useState



如何使用reducer：

```javascript
import { useReducer } from 'react';

// reducer：用来更新state的纯函数
// initState：state的初始值
// dispatch：用于更新 state 并触发组件的重新渲染。需要传入一个 action 作为参数。没有返回值
const [state, dispatch] = useReducer(reducer, initState)

function handleClick() {
  dispatch({ type: 'xxx' });
  // ...
}
// reducer入参为当前state和dispatch使用时传递的action
// 通常 action 是一个对象，其中 type 属性标识类型，其它属性携带更新所需的额外信息
// return state的新值
function reducer(state, action) {
  switch (action.type) {
    case 'added': {
      return newState;
    }
    // ...more action type
    default: {
      throw Error('未知 action: ' + action.type);
    }
  }
}

```



注意，和setState一样，dispatch更新state后，立刻读取state并不会拿到最新值

+ 详见前面篇章



example：

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1728454823487-bb26d1bb-dd31-4eae-99d6-5f03cc6fcc94.png" width="397.6" title="" crop="0,0,1,1" id="u2b8bbdd1" class="ne-image">

```javascript
import { useReducer } from 'react';
import AddTask from './AddTask.js';
import TaskList from './TaskList.js';

export default function TaskApp() {
  const [tasks, dispatch] = useReducer(tasksReducer, initialTasks);

  function handleAddTask(text) {
    dispatch({
      type: 'added',
      id: nextId++,
      text: text,
    });
  }

  function handleChangeTask(task) {
    dispatch({
      type: 'changed',
      task: task,
    });
  }

  function handleDeleteTask(taskId) {
    dispatch({
      type: 'deleted',
      id: taskId,
    });
  }

  return (
    <>
      <h1>布拉格的行程安排</h1>
      <AddTask onAddTask={handleAddTask} />
      <TaskList
        tasks={tasks}
        onChangeTask={handleChangeTask}
        onDeleteTask={handleDeleteTask}
      />
    </>
  );
}

function tasksReducer(tasks, action) {
  switch (action.type) {
    case 'added': {
      return [
        ...tasks,
        {
          id: action.id,
          text: action.text,
          done: false,
        },
      ];
    }
    case 'changed': {
      return tasks.map((t) => {
        if (t.id === action.task.id) {
          return action.task;
        } else {
          return t;
        }
      });
    }
    case 'deleted': {
      return tasks.filter((t) => t.id !== action.id);
    }
    default: {
      throw Error('未知 action: ' + action.type);
    }
  }
}

let nextId = 3;
const initialTasks = [
  {id: 0, text: '参观卡夫卡博物馆', done: true},
  {id: 1, text: '看木偶戏', done: false},
  {id: 2, text: '打卡列侬墙', done: false}
];

```

### 组件间共享参数-context
Context 允许父组件向其下层无论多深的任何组件提供信息，而无需通过 props 显式传递

+ 如果有多个组件都需要共享数据，使用父组件一层层传递props给子组件的方法会很麻烦，这时候，便可以使用context

使用过程：

+ 在一个单独的文件里创建context，用createContext，入参为context默认值<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1733302204338-efa5aa49-850b-4d5d-8685-6cd3b1561811.png" width="420.8" title="" crop="0,0,1,1" id="uf17f4777" class="ne-image">
+ 在需要向下提供context的父组件里，提供context<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1733302294939-98726988-4c7b-4eb0-a5dc-b3383cefb2b0.png" width="503.2" title="" crop="0,0,1,1" id="u63de3d03" class="ne-image">
+ 在要用到context的子组件里，<font style="color:rgb(111, 66, 193);background-color:rgb(255, 251, 221);">useContext</font><img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1733302363302-3c71a0f9-647c-48c1-8f39-c81e0b5072c8.png" width="430.4" title="" crop="0,0,1,1" id="u30244802" class="ne-image">
    - context的值为最近的父组件提供的context

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1733302496539-af41930c-942c-42cd-85ec-bcf5f01d623b.png" width="832.8" title="" crop="0,0,1,1" id="u9235ec16" class="ne-image">

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1733302517936-196c268c-84bf-46f4-abdc-9cb444692016.png" width="835.2" title="" crop="0,0,1,1" id="u6bb96899" class="ne-image">



## 脱围机制
### Effect
+ event事件：由**交互事件**引起的逻辑操作
+ effect：由**渲染**引起的逻辑操作，每次渲染后，会依据依赖项相较于上次渲染是否有变化来判断要不要执行effect（如果没有依赖项，那么每次渲染后都会执行）



依赖项

+ 在linter检查下，effect中用到的组件函数中声明的**对象、函数（包括props和state）、和由props/state计算得到的变量**，**都**需要作为依赖项
    - props/state及其计算得到的值，和组件函数中声明的**对象和函数都是**_**响应式值**__（响应式值：重新渲染可能变化）_
    - props和state变化时会引发重新渲染
        * **若props为对象，则最好把用到的属性（原始值）提出来作为依赖。**因为父组件重渲染时，props里的对象就变化了，会引发子组件依赖该对象的effect
    - 组件函数中声明的**原始值变量（string、boolean、number、undefined、null）不是响应的**，因为他们使用时用的是**值**，多次渲染时，执行同样的声明代码，值不变
    - 组件函数中声明的**对象和函数**，重新渲染时都会被重新创建，**引用变了**
        * <font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">当这些对象或函数被用来作为React的</font>`<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">useEffect</font>`<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">等Hook的依赖项时。因为每次渲染时它们的引用都会改变，即使它们的内容没有变化，也会触发effect重新执行。就相当于每次渲染都会执行effect了</font>
        * <font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">为了避免“每次渲染都会重新声明”这个问题，可以用</font>`<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">useMemo</font>`<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">（用于记忆变量）或</font>`<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">useCallback</font>`<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">（用于记忆函数）这两个Hook来缓存这些值，确保在依赖项没有变化时，返回的是同一个对象或函数引用</font>
            + <font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">依赖项为空时，表示只在组件挂载时创建一次</font>
        * **<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">总结：当普通对象&普通函数需要作为effect的依赖项时，通过以下方法减少effect执行 或 避免依赖对象和函数</font>**
            + **<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">若依赖于props和state，需要用</font>**`**<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">useMemo</font>**`**<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">（用于记忆变量）或</font>**`**<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">useCallback</font>**`**<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">（用于记忆函数）来缓存；或者把他移到effect里面，把他的依赖项添加到effect的依赖项中。</font>**
            + **<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">若是静态的，则将其移到组件函数外面（只会在import组件时执行一次）</font>**
+ **<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">依赖描述了你用到的响应值，这不是可选择的。如果要改变依赖，则要改变effect的代码或者响应值的声明方式</font>**
    - **<font style="color:rgb(51, 51, 51);background-color:rgb(247, 249, 253);">务必遵守要求！声明所有的依赖。否则，可能会有难以发现的bug</font>**
+ 无论依赖项是什么，都会在挂载的时候执行一次effect
+ []仅挂载时执行effect（若卸载了一个组件，再展示他，那么就是再次挂载）



example:

[移除 Effect 依赖 – React 中文文档](https://zh-hans.react.dev/learn/removing-effect-dependencies) 的 <font style="color:rgb(35, 39, 47);background-color:rgb(243, 244, 253);">为什么抑制 linter 对依赖的检查如此危险？ </font>

本例中，没有加上onTick的依赖，导致每1s后运行onTick时都是用的是初次渲染的，使用的count和increment是初次渲染的数据。

直接把onTick的依赖加上也可以实现功能，但每次渲染都会执行一次effect：清除上次的interval，创建新的interval。

我们考虑，onTick需要每次渲染都更新吗？他本质上是需要最新的count和increment，可以用usecallback来声明，依赖于这两个。

同时，可以用setState(state => ....)来获取最新的state，所以，只需要依赖increment了

```javascript
import { useCallback, useState, useEffect } from 'react';

export default function Timer() {
  const [count, setCount] = useState(0);
  const [increment, setIncrement] = useState(1);

  const onTick = useCallback(() => {
    setCount(count => count + increment);
  }, [increment]);

  useEffect(() => {
    const id = setInterval(onTick, 1000);
    return () => clearInterval(id);
  }, [onTick]);

  return (
    <>
      <h1>
        计数器：{count}
        <button onClick={() => setCount(0)}>重制</button>
      </h1>
      <hr />
      <p>
        每秒递增：
        <button disabled={increment === 0} onClick={() => {
          setIncrement(i => i - 1);
        }}>–</button>
        <b>{increment}</b>
        <button onClick={() => {
          setIncrement(i => i + 1);
        }}>+</button>
      </p>
    </>
  );
}

```



example：

**为了在effect中获取最新的state，**可以**向setState传参state的更新函数。**

这样就**不用把state作为依赖项**，不会引起不必要的effect执行

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725364068047-0a8a3142-fd87-44e1-b91b-5d6eb09da9a5.png" width="422.4" title="" crop="0,0,1,1" id="uf69b09c4" class="ne-image">

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725364088950-4fd09687-66c8-47e8-ad3a-1c3e99bad546.png" width="718.4" title="" crop="0,0,1,1" id="ua116a1f3" class="ne-image">



effect不能是异步函数为了防止冲突

<font style="color:rgb(35, 39, 47);background-color:rgb(246, 247, 249);">如果 Effect 需要异步获取某些数据，它通常需要清理函数。</font>

改变state的时候会重新渲染  
给useEffect指定依赖项来跳过不必要的执行（不指定的话，每次渲染都会执行）,依赖项没有变化时，不会执行effect  
在函数体内用到的变量，应当作为依赖项声明

**<font style="color:rgb(35, 39, 47);">React 总是在执行下一轮渲染的 Effect 之前清理上一轮渲染的 Effect。</font>**<font style="color:rgb(35, 39, 47);">每次重新执行 Effect 之前，React 都会调用清理函数；组件被卸载时，也会调用清理函数。</font>

+ 连接；断联
+ 订阅；退订
+ 触发动画；重置动画
+ 开始计时；结束计时

<font style="color:rgb(35, 39, 47);">example:</font>

<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725267924784-ccfe5d53-6e15-4cd9-b750-280d146432bd.png" width="614.4" title="" crop="0,0,1,1" id="u6775edbc" class="ne-image"><img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725267941968-516ac26a-2457-41f8-ad46-c951133e941c.png" width="670.4" title="" crop="0,0,1,1" id="u657d57e3" class="ne-image">  
**快速切换&异步导致竞争的问题->通过设置ignore变量来标记是否该effect已被清理需要忽略**



<font style="color:rgb(35, 39, 47);">函数组件之外代码->只会在应用程序启动时运行一次，不会渲染一次执行一次（组件内的代码会渲染一次执行一次）</font>

+ <font style="color:rgb(35, 39, 47);">某些逻辑应该只在应用程序启动时运行一次。比如，验证登陆状态和加载本地程序数据</font>

<font style="color:rgb(35, 39, 47);"></font>

<font style="color:rgb(35, 39, 47);">不必要的effect：</font>

+ **可以依据state/props计算出来的数据**，state/props变化时会再次执行组件函数，所以**普通的声明这个数据就行**
    - 若把这个数据作为state，依赖基于计算的state/props在effect更新他。那么，执行过程会是：基于计算的state/props更新了->渲染->提交阶段执行effect->这个数据的state更新了->渲染。这样会执行两次渲染，而普通的声明只用执行一次
+ **当props变化时，重置所有的state**：**对子组件设置key属性，这样react会通过key知道这是两个不同的子组件**，每次key变化时，会**删除原来的子组件并重新创建**。所以之前的state全部会清空并重建（ps. key再变回去，state也是初始态（因为又清空重建了））<img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725258170366-51e74492-9aac-4fd3-aa6d-8ce25e8be84e.png" width="636" title="" crop="0,0,1,1" id="u3a7300fb" class="ne-image">
    - 如果用effect来重置，会有上面二次渲染的问题
+ **当props变化时，需要重置部分state：**尝试调整逻辑，使用1、依据props/state计算出来的数据；2、添加key来重置所有state，来解决。用effect来重置是下策
+ 判断需要执行的逻辑是交互事件引起的还是渲染引起的（呈现给用户的视觉需要改变）
    - 由交互事件引起的逻辑->事件处理函数
    - 由渲染（视觉）引起的逻辑->effect
+ 在应用加载时执行一次的逻辑：
    - <img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725260634755-399a0f01-4006-4029-a67b-51ef3b258329.png" width="580.8" title="" crop="0,0,1,1" id="u1b822331" class="ne-image">
    - <img src="https://intranetproxy.alipay.com/skylark/lark/0/2024/png/88656377/1725260644068-18db4909-e28b-4a2e-b652-3aee1f337214.png" width="646.4" title="" crop="0,0,1,1" id="u48e6b4aa" class="ne-image">ps.<font style="color:rgb(35, 39, 47);">顶层代码会在组件被导入时执行一次——即使它最终并没有被渲染。所以只在app入口处使用顶层代码这种方法</font>

_**总结：**_

+ _**避免在effect中使用setState，尝试用1、依据props/state计算出来的数据；2、添加key来重置所有state；3、把该放到事件处理函数里的放进去。来解决**_
+ _**应用加载时执行一次的逻辑，可以放在app入口的顶层代码里**_

_****_

事件处理函数 vs Effect：

+ 事件处理函数->事件处理函数只在响应特定的 _交互操作 _时运行
+ effect->effect用于 _保持同步_
    - 每个effect代表一个独立的同步过程。同步不同的事情，应该分别写effect









_****_






