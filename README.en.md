
# Wpmjs 

Link every piece of code in the web world. [中文版](./README.en.md)

# Why

Wpm, whose full name is "Web Program Module", is a web based module read and write format. Different from NPM, Wpm module is completely loaded and used at runtime. Wpm uses a specific api to read and write modules, so it doesn't rely on any build tools. Any code you build from webpack, vite, or rollup can be easily converted into Wpm modules. Distribute to anyone through a CDN.

# 快速开始

## 安装
```
npm i wpmjs-cli wpmjs-core
```

## 编写一个 wpm 模块
```js
import wpm from 'wpmjs-core'

const MyModule = {
  getName(){
    
  }
}

const getName(){
  return 'called'
}

wpm.create({
  name:'@MyScope/MyModule',
  exports:{
    default: MyModule,
    api:{
      getName
    }
  }
})

```


## 引用别人编写好的 wpm 模块
```js
import wpm from 'wpmjs-core'

const OtherModule = wpm.require('@OtherScope/OtherModule')
// or
const OtherHttpModule = wpm.require('https://mycdn....')

//需要开启 Top async/await 语法解析
const default = await OtherModule.defualt

OtherModule.getName() // called
```
## 上传模块

```bash
wpm upload [构建结果目录, 例如 dist]
```

> 默认通过 surge.sh 上传，surge.sh 是一个免费的 cdn 静态资源托管服务

## .wpmrc

Wpm 配置文件

- source: 默认的模块源，可以指定为私有的或者其他公有的静态托管服务 default: surge.sh
- target: 指定上传的目标目录 default: null
