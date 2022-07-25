# package.json

## name 
如果项目是需要发版为npm包的，则name字段是必须的
### 命名规范
- 字符串长度小于等于214个字符
- 同一作用域内的包，可以用 `.`或`_`作为开始字符
- 不能使用大写字母命名
- 不能带任何不安全的url字符
  - 空格 " "
  - 大于小于号 `<>`
  - 方括号 `[]`
  - 花括号 `{}`
  - 竖线   `|`
  - 反斜杠 `\`
  - 插入号 `^`
  - 百分比 `%`  

- 私源npm包命名 `@[scope]/[name]`

## version
用于定义版本号

## description
描述当前项目的概况

## keywords
标记当前项目的重点词汇，同时作为搜索关键词，提供给资源平台使用，进行索引

## homepage
项目的官网主页地址

## repository
项目的源码地址

## license
项目的协议类型，这个项目涉及到知识产权方面的知识

## author
作者信息

## contributors
协作者信息

## files
声明有哪些文件，是需要作为依赖项，保留下来,否则，执行npm publish进行发布时，这些文件是会自动屏蔽上传的

## main
使用npm包时，需要进行require(..)的操作。这个操作，会查看main字段，找到程序的主入口

## bin
工具性质的npm包，一定有bin字段，对外暴露脚本命令

## scripts
项目脚本命令

## dependencies
生产环境中使用到的依赖

## devDependencies
运行时使用依赖，生产环境不需要使用的依赖，都需要安装在devDependencies下

## peerDependencies
同等依赖，用于指定当前包兼容的宿主版本，解决插件与所依赖包不一致的问题。一般在进行插件开发的时候使用

- 插件正确运行的前提是，核心依赖库必须先下载安装，不能脱离核心依赖库而被单独依赖并引用
- 插件入口 api 的设计必须要符合核心依赖库的规范
- 插件的核心逻辑运行在依赖库的调用中

## types
项目如果是用TypeScript写的，则需要types字段，对外暴露相关的类型定义

## module
性质等同于main字段。module用于ES6规范的模块，只要支持ES6，会优先使用module入口。
这样，代码也可以启用tree shaking机制

## sideEffects
格式：`boolean | string[]`

- sideEffects: false用于告知打包工具（webpack），当前项目无副作用，可以使用tree shaking优化
- sideEffects的值，也可以是一个文件路径组成的数组。告知哪些文件无副作用，可以使用tree shaking优化
- "import xxx;"语句，只引入未使用，如果声明了sideEffects，则会被tree shaking删除掉,由于tree shaking只在production模式生效，所以本地开发会一切正常，生产环境很难及时发现这个问题