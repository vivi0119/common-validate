# [validator](https://github.com/yesixuan/common-validate)
[![](https://img.shields.io/badge/Powered%20by-yesixuan%20base-brightgreen.svg)](https://github.com/yesixuan/common-validate)
[![license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/yesixuan/common-validate/blob/master/LICENSE)
[![Build Status](https://travis-ci.org/yanhaijing/jslib-base.svg?branch=master)](https://travis-ci.org/yanhaijing/jslib-base)
[![Coveralls](https://img.shields.io/coveralls/yanhaijing/jslib-base.svg)](https://coveralls.io/github/yesixuan/common-validate)
[![npm](https://img.shields.io/badge/npm-0.1.0-orange.svg)](https://www.npmjs.com/package/@ignorance/common-validate)
[![NPM downloads](http://img.shields.io/npm/dm/jslib-base.svg?style=flat-square)](http://www.npmtrends.com/@ignorance/common-validate)
[![Percentage of issues still open](http://isitmaintained.com/badge/open/yanhaijing/jslib-base.svg)](http://isitmaintained.com/project/yanhaijing/jslib-base "Percentage of issues still open")

> JS 通用的响应式校验工具。适用 nodejs、vue、react、小程序、原生。数据变化自动触发校验


## Usage

```js
import Validator from '@ignorance/validator'

// 待校验数据
const formData = {
  name: 'lisa',
  age: '12'
}

// 校验规则 （默认支持 required min max） 同样支持正则表达式校验、检验函数（必须返回 true|false）
const ruleConfig = {
  name: [
    {
      validator: 'required',
      msg: '必填'
    },
    {
      validator: 'min:2 max:6',
      msg: '长度在 2 ~ 6 之间'
    }
  ],
  age: [
    {
      validator: 'required',
      msg: '必填'
    },
    {
      validator: val => +val >= 20,
      msg: '长度在 2 ~ 6 之间'
    }
  ]
}

const validator = new Validator(formData, ruleConfig)
// 单个字段校验是否通过
validator.isError('age') // true | false
// 单个字段校验 (不传要校验的字段则默认校验全部)
validator.verify('age')
// 整体校验
validator.verify()
```

## 扩展默认规则

```js
import Validator, { rules } from '@ignorance/validator'

rules.extendRegexp({
  onlyNumber: /^\d+$/,
  // ...
})

rules.extendValidator({
  lessThanTen: val => {
    val = +val
    return val < 10
  },
  // ...
})
```


