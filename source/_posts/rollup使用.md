---
title: rollup使用
date: 2021-11-10 16:47:41
tags:
---
# 安装rollup
```javascript
    npm i --save rollup
```
# 配置rollup.config.js
```javascript
import {uglify} from 'rollup-plugin-uglify';
import babel from 'rollup-plugin-babel';
import resolve from 'rollup-plugin-node-resolve';
import commonjs from 'rollup-plugin-commonjs';
 
export default {
  input: 'index.js',
  output: {
      file: './dist/bundle.js', //打包后的文件
      format:'iife',
      name:'velocity'//iife格式输出的方法名
  },
  plugins: [
    resolve({
      jsnext: true,
      main: true,
      browser: true,
    }),
    commonjs(),
    uglify(),
    babel({
      exclude: 'node_modules/**',
    }),
  ],
};
```
# 引入babel
```javascript
    npm install --save rollup-plugin-babel@latest @babel/core @babel/preset-env
```
新建.babelrc文件，写入如下配置，在rollup.config.js的plugins中加入bable()
```javascript
{
    "presets": [
      [
        "@babel/preset-env",
        {
          "modules": false
        }
      ]
    ]
}
```
部分语法（for of,Object.assign等）babel不会主动转，需要babel引入插件
在.babelrc中加入插件plugins
```javascript
    "plugins": [
      "@babel/plugin-proposal-object-rest-spread",
      "transform-object-assign"
    ]
```
安装依赖：
```javascript
    "@babel/plugin-proposal-object-rest-spread": "^7.0.0",
    "babel-plugin-transform-object-assign": "^6.22.0",
```
# 引入uglify压缩代码
```javascript
    npm install --save rollup-plugin-uglify
```
plugins中加入uglify()
# 引入common js支持，兼容commonsjs规范
```javascript
    npm install --save-dev rollup-plugin-commonjs rollup-plugin-node-resolve
```