---
title: fussion 公共方法
date: 2022-04-25
sidebar: 'auto'
tags:
- 文档
---

# 公共方法

## 数据格式化千分位保留小数

#### 实现代码

```ts
//格式化千分位保留小数
import numeral from 'numeral'

/**
 * 格式化数值保留两位小数并格式化千分位
 * @param v 需要格式化的数值
 * @param t 是否需要格式化千分位
 * @returns
 */
export const formatData = (v: string | number, t = -1) => {
  const str = t == 2 ? '0.00' : '0,0.00'
  return v ? numeral(v).format(str) : v != 0 ? '-' : v
}
```

#### 调用方式

```ts
//目前代码再dip模块如果其它项目需要提到公共地方就可以
import { formatData } from '@/utils'
//具体使用方式
const columns = ref<any>([
  {
    title: '科室',
    key: 'cykb',
    width: '200px',
    render(row: any) {
      return formatData(row.cykb)
    }
  },
  {
    title: '百分比',
    key: 'percent',
    width: '200px',
    render(row: any) {
      return formatData(row.percent, 2)
    }
  }
])
```

## 初始化日期方法

#### 常规日期方法

```ts
import dayjs from 'dayjs'

/**
 * 获取当前月份
 * 格式 YYYY-MM
 * @returns 当前月份
 */
export const currentMonth = () => {
  return dayjs(Date.now()).format('YYYY-MM')
}

/**
 * 获取当前月份第n个月的月份
 * @param num number 间隔月份数 正数 是当前月之后的月份 负数 当前月之前的月份
 * @returns String 当前月份n个月的月份
 */
export const currentDynamicMonth = (num: number) => {
  return dayjs(Date.now()).add(num, 'month').format('YYYY-MM')
}

/**
 * 获取当前月份后n个月的月份 默认当前月到前3个月
 * @param num number 间隔月份数
 * @returns Array 当前到n个月的区间
 */
export const currentDynamicMonths = (num?: number) => {
  const nums = num ? -num : -3
  return [dayjs(Date.now()).add(nums, 'month').format('YYYY-MM'), dayjs(Date.now()).format('YYYY-MM')]
}

/**
 * 验证区间日期开始日期不能大于结束日期
 * @param arr Array<string>
 * @returns Boolean
 */
export const isBeforeDates = (arr: Array<string>) => {
  const isBeforeValue = arr.length > 1 ? dayjs(arr[0]).isBefore(dayjs(arr[1])) : false
  return isBeforeValue
}

/**
 * 间隔月份
 * @param arr 数据集
 * @returns -1 数据源不合法 返回间隔月份数
 */
export const spaceMonths = (arr: Array<string>) => {
  return arr.length > 1 ? dayjs(arr[1]).diff(dayjs(arr[0]), 'month') : -1
}

/**
 * 间隔天数
 * @param arr 数据集
 * @returns -1 数据源不合法 返回间隔天数
 */
export const spaceDays = (arr: Array<string>) => {
  return arr.length > 1 ? dayjs(arr[1]).diff(dayjs(arr[0]), 'day') : -1
}

/**
 * 获取近多少天
 * @param num number 间隔天数 正 当前天到之后的多少天 负 当前天到之前的多少天
 * @returns Array 当前到n天时间间隔
 */
export const dynamicDays = (num?: number) => {
  const nums = num ? num : -30
  return nums > 0
    ? [dayjs(Date.now()).format('YYYY-MM-DD'), dayjs(Date.now()).add(nums, 'day').format('YYYY-MM-DD')]
    : [dayjs(Date.now()).add(nums, 'day').format('YYYY-MM-DD'), dayjs(Date.now()).format('YYYY-MM-DD')]
}

/**
 * 获取当月的第一天和最后一天
 * @returns Array 第一天和最后一天
 */
export const currentMonthDaySpace = () => {
  return [dayjs().startOf('month').format('YYYY-MM-DD'), dayjs().endOf('month').format('YYYY-MM-DD')]
}
```

#### 调用方式

```ts
//全局公共方法
import { currentDynamicMonths } from 'peace-library'
// 返回数据格式['2022-01,2022-04']
const dates = currentDynamicMonths()
```
