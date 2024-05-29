# Notepad：
用vue框架实现的可以列出任务清单
## 一、功能总结：
### ① 列表渲染：
**v-for key** 的设置 {{ }} 插值表达式
### ② 删除功能：
**v-on** 调用传参 **filter** 过滤 覆盖修改原数组  
```javascript
this.list = this.list.filter(item => item.id !== id)
```
### ③ 添加功能：
**v-model** 绑定 **push** 修改原数组从最后面添加新的
### ④ 底部统计 和 清空：
数组.length累计长度 list.length
覆盖数组清空列表this.list = []
**v-show** 控制隐藏  
```javascript
v-show="list.length > 0"
```
### ⑤ 按下回车键 Enter 键触发：
**v-on** 调用传参 **e** 中使得按下Enter键触发
e.key === 'Enter'
再调用添加任务add()方法
## 示意图：
[![notepad](https://img.17carat.cn/2024/04/github/notepad.png "notepad")](https://img.17carat.cn/2024/04/github/notepad.png "notepad")

## 二、组件通信方法：
### 渲染功能：
1.提供数据 -> 提供在公共的父组件 App.vue
2. 通过父传子传递给TodoMain
3.利用v-for渲染

### 2.添加功能：
1.收集表单数据 -> v-model
2.监听事件(回车 + 点击 都要进行添加)
3.子传父，将任务名称传递给父组件App.vue
4.进行添加push(自己的数据自己负责)

### 删除功能：
1. 监听事件(监听删除的点击)携带
2. 子传父，将删除的id传递给父组件App.vue
3.进行删除filter

### 底部合计：父传子传list -> 渲染:
### 清空功能：子传父 通知到父组件 -> 父组件进行清空操作:
### 持久化存储：watch深度监视list的变化 -> 往本地存储 -> 进入页面优先读取本地 -> 如果取不到就用默认值:
