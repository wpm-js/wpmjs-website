# Wpmjs 

链接 web 世界里的每一段代码 [To Englinsh Vesion](./README.en.md)

# Why

Wpm 全称 “Web Program Module” 是一种基于 web 的模块读写格式，和 NPM 不同 Wpm 模块完全在运行时加载和使用，不需要在本地安装因此也没有臃肿的 node_modules, Wpm 使用特定的 api 来读写模块，因此也不依赖任何构建工具，无论你是 webpack 还是 vite 又或者是 rollup 构建的代码都可以很简单的转换成 Wpm 模块，通过 CDN 分发给任何一个人。

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
