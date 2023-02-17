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
