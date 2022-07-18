# css

## position
- clip `clip: rect(top, right, bottom, left)` 定义一个裁剪矩形，只有矩形内的内容才可见

## layout
- overflow-x 或 overflow-y `overflow-x: xxx` `overflow-y: xxx`
  - visible 不裁剪内容，可能会显示在内容框之外
  - hidden 裁剪内容，不提供滚动机制
  - scroll 裁剪内容，提供滚动机制
  - auto 如果溢出框，则提供滚动机制

## background
- background-repeat 背景图像可以沿着水平轴，垂直轴，两个轴重复，或者根本不重复
  - repeat-x 水平位置重复
  - repeat-y 垂直位置重复
  - repeat 图像会按需重复来覆盖整个背景图片所在的区域。最后一个图像会被裁剪，如果它的大小不合适的话
  - no-repeat   不重复

- background-origin 相对于内容框来定位背景图像
  - border-box 背景图像相对于边框盒定位
  - padding-box 背景图像相对于内边距框来定位
  - content-box 背景图像相对于内容框来定位

-background-clip 设置元素的背景（背景图片或颜色）是否延伸到边框、内边距盒子、内容盒子下面
  - border-box 背景延伸至边框外沿（但是在边框下层）
  - padding-box 背景延伸至内边距（padding）外沿。不会绘制到边框处
  - content-box 背景被裁剪至内容区（content box）外沿
  - text 背景被裁剪成文字的前景色

## font
- font-family
- font-size-adjust 定义小写字母的大小，font-size*font-size-adjust

## text
- text-transform 
  - capitalize 强制每个单词的首字母大写，其他不变
  - uppercase 所有字符大写
  - lowercase 所有字符小写
  - none 阻止转换
- white-space  处理元素中的空白
  - normal 连续的空白符会被合并，换行符被当作空白符处理
  - nowrap 连续空白符合并，但文本内换行无效
  - pre 连续空白符保留，遇到换行符或者`<br>` 元素换行
  - pre-wrap 连续空白符保留，遇到换行符或者`<br>` 元素换行
  - pre-line 连续的空白符会被**合并**。在遇到换行符或者 `<br>`元素
- overflow-wrap  
  - normal 行只能在正常的单词断点处中断
  - break-word 如果行内没有多余的地方容纳该单词到结尾，则那些正常的不能被分割的单词会被强制分割换行

- tab-size 自定义制表符宽度
- work-break 怎样在单词内断行
  - normal 默认断行
  - break-all non-cjk文本，在任意字符见断行
  - keep-all CJK文本不断行，non-cjk文本表现同mormal（cjk值中文/日文/韩文）
- text-align-last 一段文本中最后一行在被强制换行之前的对齐规则
- text-justify 当文本的 text-align 属性被设置为 :justify 时的齐行方法。
- letter-spacing 设置文本字符的间距表现
- text-indent 一个块元素首行文本内容之前的缩进量
- vertical-align 指定行内元素（inline）或表格单元格（table-cell）元素的垂直对齐方式
- line-height 设置多行元素的空间量，对于块级元素，它指定元素行盒（line boxes）的最小高度
- text-size-adjust 控制将一些手机或平板设备上使用的文本溢出算法

## text decoration
- text-decoration 设置文本的修饰线外观， text-decoration-line, text-decoration-color, text-decoration-style, 和新出现的 text-decoration-thickness 属性的缩写
- text-decoration-line 设置元素中的文本的修饰类型
- text-decoration-color 设置文本修饰线的颜色
- text-decoration-style 设定的线的样式
- text-decoration-skip 元素哪些部分的内容需要被文本修饰所跳过
- text-underline-position 当 text-decoration属性的值设置为 underline 之后，可以用 text-underline-position 属性为其设置下划线的位置
- text-shadow 为文字添加阴影