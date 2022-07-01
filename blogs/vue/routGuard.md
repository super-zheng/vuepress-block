---
title: vue3：路由守卫（全局守卫、路由独享守卫、组件内守卫）
date: 2022-07-01
author: huo
sidebar: 'auto'
tags:
- vue
categories:
- vue.js
---

::: tip 介绍
全局守卫、路由独享守卫、组件内守卫
:::


## router.js：全局守卫

```javascript
import {
	createRouter,
	createWebHashHistory
} from 'vue-router'

// 省略了routes 中的路由规则
const routes = [
	...
	...
]

const router = createRouter({
	history: createWebHashHistory(),
	routes
})

// 全局守卫：登录拦截 本地没有存token,请重新登录
router.beforeEach((to, from, next) => {
	// 判断有没有登录
	if (!localStorage.getItem('token')) {
		if (to.name == "login") {
			next();
		} else {
			router.push('login')
		}
	} else {
		next();
	}
});
export default router

```


## 路由独享守卫
```javascript
{
	path: '/admin',
	name: 'admin',
	component: () => import('../views/mine/admin.vue'),
	//beforeEnter(to,form.next)=>{判断是否登陆代码}，点击进入admin也面时，路由独享守卫启用
	beforeEnter:(to,form,next)=>{
		if (!localStorage.getItem('user')) {
			if (to.name == "login") {
				next();
			} else {
				router.push('login')
			}
		} else {
			next();
		}
	}
},

```
## 组件内守卫
有些时候我们需要知道是从那一个页面跳转过来的
然后做一些逻辑处理
比如说：
1、order.vue(订单) -> detail.vue(详情)
2、A.vue(商品详情) -> B.vue(确认订单) -> C.vue(支付成功后跳转订单详情) ->detail.vue(详情)
这个时候我们需要使用beforeRouteEnter 来解决页面返回问题

```javascript
<template>
	<div class="mine">
		<van-nav-bar
		  title="订单详情"
		  left-text="返回"
		  left-arrow
		  @click-left="goBack"
		/>
		<h1>从　{{data.routerIndex}}　页面来</h1>
	</div>
</template>
<script>
	import { useRouter } from 'vue-router'
	import { reactive } from 'vue'
	export default {
		// 组件内守卫
		beforeRouteEnter:(to,form,next)=>{
			//to 到哪里去
			//form 从哪里来
			next( vm => {
				vm.data.routerIndex = form.name;
			})
		},
		setup(){
			const router = useRouter();
			var data = reactive({
				routerIndex:''
			})
			let goBack = () =>{
				// 如果从C.vue来，则返回router.go(-3),回到A.vue，否则正常返回上级页面
				if(data.routerIndex == 'C'){
					router.go(-3);
				}else{
					router.go(-1);
				}
			}
			return{
				data,
				goBack
			}
		}
	}
</script>


```