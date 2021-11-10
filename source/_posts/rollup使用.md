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
      dir: 'dist',
      format:'iife',
      entryFileNames:'bundle.js'
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
新建.babelrc文件，写入如下配置，在plugins中加入bable()
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
# 引入uglify压缩代码
```javascript
    npm install --save rollup-plugin-uglify
```
plugins中加入uglify()
# 引入common js支持，兼容commonsjs规范
```javascript
    npm install --save-dev rollup-plugin-commonjs rollup-plugin-node-resolve
```