<template>
  <div class="todo-header">
      <input type="text" placeholder="请输入任务，回车键确认" @keyup.enter="add"/>
  </div>
</template>

<script>
import { nanoid } from 'nanoid'
export default {
    name:'MyHeader',
    methods: {
        add(e){
            //输入空值检测
            if(!e.target.value.trim()) return alert('请输入内容') 
                //将用户输入包装成todo对象
                const todoObj = {id:nanoid(),title:e.target.value,done:false}
                //将对象传给addTodo函数
                this.$emit('addTodo',todoObj)
                // this.addTodo(todoObj)
                //重置输入框
                e.target.value=''
        }
    }
}
</script>

<style scoped>
    .todo-header input{
        width: 560px;
        height: 28px;
        font-size: 14px;
        border: 1px solid #ccc;
        border-radius: 4px;
        padding: 4px 7px;
    }

    .todo-header input:focus{
        outline: none;
        border-color: rgba(82, 168, 236, 0.8);
        box-shadow: inset 0 1px 1px rgba(0,0,0, 0.075), 0 0 8px rgba(82, 168, 236, 0.8);
    }
</style>