<template>
  <!-- 主体区域 -->
  <section id="app">
    <TodoHeader @add="handleAdd"></TodoHeader>
    <TodoMain :list="list" @del="handleDel"></TodoMain>
    <TodoFooter :list="list" @clear="handleClear"></TodoFooter>
  </section>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
// 渲染功能
// 1.提供数据 -> 提供在公共的父组件 App.vue
//2. 通过父传子传递给TodoMain
//3.利用v-for渲染

// 2.添加功能
// 1.收集表单数据 -> v-model
// 2.监听事件(回车 + 点击 都要进行添加)
// 3.子传父，将任务名称传递给父组件App.vue
// 4.进行添加push(自己的数据自己负责)

//删除功能：
//1. 监听事件(监听删除的点击)携带
// 2.子传父，将删除的id传递给父组件App.vue
//3.进行删除filter

//底部合计：父传子传list -> 渲染
//清空功能：子传父 通知到父组件 -> 父组件进行清空操作
//持久化存储：watch深度监视list的变化 -> 往本地存储 -> 进入页面优先读取本地 -> 如果取不到就用默认值
export default {
  data () {
    return {
      list: JSON.parse(localStorage.getItem('list')) || [
        {id: 1, name: '打篮球'},
        {id: 2, name: '看电影'},
        {id: 3, name: '逛街'}
      ]
    }
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter
  },
  methods: {
    handleAdd(todoName){
      // console.log(todoName);
      this.list.push({
        id: +new Date(),
        name: todoName
      })
    },
    handleDel(id){
      // console.log('老爹接收到了', id);
      //不等于的保留下来
      this.list = this.list.filter(item => item.id !==id)
    },
    handleClear(){
      this.list = []
    }
  },
  watch: {
    list: {
      deep: true,
      handler (newValue){
        localStorage.setItem('list', JSON.stringify(newValue))
      }
    }
  }

}
</script>

<style>

</style>
