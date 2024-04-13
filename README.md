# Notepad
用vue框架实现的可以列出任务清单
## 功能总结：
### ① 列表渲染：
**v-for key** 的设置 {{ }} 插值表达式
### ② 删除功能
**v-on** 调用传参 **filter** 过滤 覆盖修改原数组  this.list = this.list.filter(item => item.id !== id)
### ③ 添加功能
**v-model** 绑定 **push** 修改原数组从最后面添加新的
### ④ 底部统计 和 清空
数组.length累计长度 list.length
覆盖数组清空列表this.list = []
**v-show** 控制隐藏  v-show="list.length > 0"
### ⑤ 按下回车键 Enter 键触发
**v-on** 调用传参 **e** 中使得按下Enter键触发
e.key === 'Enter'
再调用添加任务add()方法
