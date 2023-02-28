
# Wpmjs 

Link every piece of code in the web world. [中文版](./README.md)

# Why

Wpm, whose full name is "Web Program Module", is a web based module read and write format. Different from NPM, Wpm module is completely loaded and used at runtime. Wpm uses a specific api to read and write modules, so it doesn't rely on any build tools. Any code you build from webpack, vite, or rollup can be easily converted into Wpm modules. Distribute to anyone through a CDN.

# Quick start

## Installation
```
npm i wpmjs-cli wpmjs-core
```

## Writing a wpm module

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


## Using a wpm module written by others
```js
import wpm from 'wpmjs-core'

const OtherModule = wpm.require('@OtherScope/OtherModule')
// or
const OtherHttpModule = wpm.require('https://mycdn....')

//需要开启 Top async/await 语法解析
const default = await OtherModule.defualt

OtherModule.getName() // called
```
## Uploading modules


```bash
wpm upload [build result directory, such as dist]
```

> By default, it is uploaded through surge.sh, which is a free CDN static resource hosting service.



## .wpmrc

Wpm configuration file

source: Default module source, can be specified as private or other public static hosting services default: surge.sh
target: Specifies the target directory for uploading default: null

