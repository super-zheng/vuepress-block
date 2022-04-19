---
title: vue中install方法
date: 2022-04-19
author: huo
sidebar: 'auto'
tags:
- vue
categories:
- vue.js
---

::: tip 介绍
vue提供install可供我们开发新的插件及全局注册组件等install方法第一个参数是vue的构造器，
第二个参数是可选的选项对象
:::

```javascript
export default {
	install(Vue,option){
		组件
		指令
		混入
		挂载vue原型
	}
}
```
## 全局注册组件

```javascript
import PageTools from '@/components/PageTools/pageTools.vue'
import update from './update/index.vue'
import ImageUpload from './ImageUpload/ImageUpload.vue'
import ScreenFull from './ScreenFull'
import ThemePicker from './ThemePicker'
import TagsView from './TagsView'
export default {
  install(Vue) {
    Vue.component('PageTools', PageTools)
    Vue.component('update', update)
    Vue.component('ImageUpload', ImageUpload)
    Vue.component('ScreenFull', ScreenFull)
    Vue.component('ThemePicker', ThemePicker)
    Vue.component('TagsView', TagsView)
  }
}
```
### 在main.js中直接用引用并Vue.use进行注册
```javascript
import Component from '@/components'
Vue.use(Component)
```

## 自定义指令
```javascript
export default{
	install(Vue){
		Vue.directive('pre',{
			inserted(button,bind){
				button.addEventListener('click',()=>{
					if(!button.disabled){
						button.disabled = true;
						setTimeout(()=>{
							button.disabled = false
						},1000)
					}
				})
			}
		})
	}
}
```
### 在main.js跟注册组件一样
```javascript
import pre from '@/aiqi'
Vue.use(pre)
```