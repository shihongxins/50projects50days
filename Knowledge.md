### [01-Expanding-Cards](/50projects50days/01-Expanding-Cards/)
+ CSS 计数器用法
  + 初始化 `counter-reset: <custom-ident> <integer>?;`
    + `<custom-ident>` 必须符合 `/[a-z][a-z-_1-9]/i`
    + `<integer>` 缺省值为 0
    + 可同时初始化多个计数器 `counter-reset: page 1 section 1 article;`
  + 设置增量 `counter-increment: <custom-ident> <integer>?;`
    + `<integer>` 正值表递增，负值表递减，缺省值为 1
    + 可同时设置多个计数器增量 `counter-increment: page section article 2;`
  + 显示计数值
    + `counter(<counter-ident>, <counter-style>?);` 不包含父级上下文，仅同级嵌套内容编号
    + `counters(<counter-ident>, <string>, <counter-style>?);` 包含父级上下文和父子级嵌套级内容编号
    + `<counter-style>` 支持几乎所有的 [`list-style-type`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/list-style-type)
    + 将获取到的编号通过 `content` 属性显示

### [02-Progress-Steps](/50projects50days/02-Progress-Steps/)
+ CSS 变量
  + 声明：通过 `--<custom-property-name>: <declaration-value>;` 格式的 **属性** 可自定义 CSS 变量
  + 使用：通过 `var(--<custom-property-name>, <declaration-value>?);` 获取 CSS 变量值，此处 `<declaration-value>` 为默认值

### [03-Rotating-Navigation](/50projects50days/03-Rotating-Navigation/)
+ CSS 文字镂空
  + 设置颜色为透明： `color: transparent;`
  + 设置文字描边：`-webkit-text-stroke: <-webkit-text-stroke-width> <-webkit-text-stroke-color>;`
  + 填充可用伪元素 `::after + width` 的变化设置过渡
+ 模拟光标可使用伪元素 `::before` （此时最好不设置 `padding` 值，方便光标计算位置）

### [05-Blurry-Loading](/50projects50days/05-Blurry-Loading/)
+ 加载进度既要显示进度值文字，又要将进度值设置到其他属性上（如宽度，透明度等）
  + 不能使用 `attr(<attribute-name>);` 。因为它仅能作用于 `content` 属性用以显示进度值文字，而不能用于其他属性；
  + 使用 CSS 变量
    + 通过 `var` 获取 CSS 变量将其设置到其他属性上
    + 如果其他属性需要的是非字符型属性值，可通过 `calc()` 计算求值进行单位换算
    + 但 `content` 不能直接设置 CSS 变量显示值，可通过 CSS 计数器获取 CSS 变量作为初始值最终显示 CSS 计数器值到 `content` 上
    + 参考 [小tips: 如何借助content属性显示CSS var变量值](https://www.zhangxinxu.com/wordpress/2019/05/content-css-var/)
+ CSS 滤镜
  + 使用 `filter: <filter-function> | none;`
  + 常用的 `<filter-function>`
    + 透明度 `opacity(50%)`
    + 网站变灰 `grayscale(100%)`
    + 高斯模糊 `blur(5px)`
    + 不规则图形阴影 `drop-shadow(x, y, blur, color)`
    + 使用 SVG 提供的滤镜 `url(svg#element)`

### [06-Scroll-Animation](/50projects50days/06-Scroll-Animation/)
+ 移入移出过渡效果使用 `transform: translate(x, y);`
+ CSS Win7 Aero
```css
  selector {
    /* 👍 CSS Aero Effect */
    border: 1px solid rgba(0,0,0,0.3);
    border-radius: 4px;
    background: rgba(32,32,32,0.2);
    box-shadow: 
      0 2px 6px rgba(0,0,0,0.5),
      inset 0 1px rgba(0,0,0,0.3),
      inset 0 10px rgba(255,255,255,0.2),
      inset 0 10px 20px rgba(255,255,255,0.25),
      inset 0 -15px 30px rgba(0,0,0,0.3);
    backdrop-filter: blur(3px);
  }
```

### [07-Split-Landing-Page](/50projects50days/07-Split-Landing-Page/)
+ `backdrop-filter` 为元素 **覆盖的区域（不是元素本身）** 添加滤镜，常用于设置毛玻璃效果，由于滤镜效果生效于元素背后的覆盖区域，因此至少元素得有透明效果才能观察。
  + 语法 `backdrop-filter: blur(6px);`
  + 与 `filter: blur(6px)` 的区别， `filter` 滤镜生效于 **元素本身** ，会将元素及其内容（包括子代都模糊）。
  + 兼容模拟 `background-color: rgba(255, 255, 255, 0.6);`

### [08-Form-Wave](/50projects50days/08-Form-Wave/)
+ `transform` 对内联元素 `inline` ，表格列，表格列组无效
+ 不能通过 `input:not(:empty)` 判断 `input` 元素是否有值，因为它是替换元素始终为 `void` 而应该通过 `:valid` 判断

### [11-Event-Keycodes](/50projects50days/11-Event-Keycodes/)
+ `String.prototype.replace(substr|pattern, newSubstr|function)`
  + 第一个参数为 `substr: string` 时，仅替换第一个匹配项；
  + 第一个参数为 `pattern: RegExp` 时，如果不带全局标识 `g`, 也只替换第一个匹配项，当带有全局标识 `g` 后，替换所有匹配项；
  + 第二个参数为 `newSubstr: string` 时
    + 如果第一项为 `substr: string` 直接替换；
    + 如果第一项为 `pattern: RegExp` 时，可在 `newSubstr: string` 中通过*特殊变量*获取匹配字符串中的*特殊值*，如 `$$,$&,$n,$``,$',$name` 等；
  + 第二个参数为 `function` 时，可通过参数 `match, p1, p1, ..., offset, string` 更精确控制替换值；
+ `String.prototype.replaceAll(substr|pattern, newSubstr|function)`
  + 第一个参数为 `substr: string` 时，替换所有匹配项；
  + 第一个参数为 `pattern: RegExp` 时，*必须*带全局标识 `g`；
  + 第二个参数同 `String.prototype.replace(substr|pattern, newSubstr|function)`

+ `DocumentFragment` 文档片段可直接插入某节点，它继承于 `Node` ；
```js
  // const fragment = new DocumentFragment();
  const fragment = new DocumentFragment();
  fragment.append("1");
  fragment.appendChild(document.createTextNode("2"));
  document.body.appendChild(fragment);
```

+ 操作 DOM 时，注意区分 `Node, Element`
  + 大多数 DOM API 都会继承 `Node` ，如 `Element, Attr, CharacterData(Text, Comment, CDATAString), DocumentType, DocumentFragment` 等，因此它的属性和方法兼容性较好，但由于它的子节点类型众多，有可能通过某些属性获得非预期结果或 `null` ，或者抛出异常（如将某节点插入不支持子节点的节点）；
  + `Node` 的属性及方法数量和名称都较少且命名清晰，容易记忆，常用属性和方法大部分含有 node 或 child 字样；
  + `Element` 继承于 `Node` ，除了拥有 `Node` 的方法外，还扩展了其他方法，比较杂乱，且兼容性不一致，常用属性和方法大部分含有 children 或 element 字样，另外扩展的元素节点操作方法大部分仅含有操作方式单词如 `after(), append(), before(), prepend(), remove()`

### [13-Random-Choice-Picker](/50projects50days/13-Random-Choice-Picker/)
+ HTML 中给元素绑定事件的方法有
  + 方式一，直接在标签上设置属性如，`<button onclick="alert('Hello World')">Say</button>` ，注意值是**方法/代码的调用执行**，不能仅是事件句柄（方法名）；
  + 通过 API 给元素添加事件监听如
  ```js
    function say() {
      alert("Hello World");
    }
    const button = document.querySelector("button");
    // 方式二，直接给 DOM 元素的属性绑定事件句柄（方法名），此时不能为方法或代码的调用执行，否则在绑定时就立即执行了，后续手动无法触发；
    /*
    button.onclick = say;
    */
    // 方式三，通过 API 给元素添加事件监听
    button.addEventListener("click", say);
  ```
  + 三种方式的总结
    + 方式一： HTML 与 JavaScript 耦合严重，不利于方法复用；
    + 方式二：虽解耦了 HTML 与 JavaScript ，但同类事件仅能绑定一个方法，如都给 `onclick` 属性赋值为 `say1,say2` 方法，最后 `say2` 会覆盖 `say1` ；
    + 方法三：灵活的给元素添加事件监听，并能通过第三个参数 `useCapture|options` 方便的控制 DOM 事件；
      + `useCapture: boolean = false` 控制事件是否在捕获阶段响应；
      + `options: { capture: false, once: false, passive: false }` 根详细的控制事件捕获阶段响应、仅执行一次、是否*禁止*阻止默认事件
      + 能通过此 API 给同类事件绑定多个方法；
      + 能通过 `removeEventListener` 取消事件监听；

### [14-Animated-Navigation](/50projects50days/14-Animated-Navigation/)
+ 撞色背景
  ```css
    body {
      background-color: lightskyblue;
      background-image: linear-gradient(to bottom, lightskyblue 50%, lightgreen 50%);
    }
  ```
+ 宽度/高度的折叠/展开
  + 最外层为固定值变化，如 80~350
  + 中层为百分比变化，0%~100% ，并且变化后通过 `opacity/overflow` 隐藏内容
  + 最里层的项目可添加其他过渡效果
+ CSS 制作 ＝ 和 ✖ 
  ```css
    nav .nav-btn--close::before,
    nav .nav-btn--close::after {
      content: "";
      position: absolute;
      top: 10px;
      left: 5px;
      width: 20px;
      height: 2px;
      background-color: lightskyblue;
      transform: rotate(0deg) translateY(0);
      transition: transform 0.6s linear;
    }

    nav.open .nav-btn--close::before {
      transform: rotate(765deg) translateY(5.5px);
    }

    nav.open .nav-btn--close::after {
      transform: rotate(-765deg) translateY(-5.5px);
    }
  ```
