<template>
    <div class="todo-footer" v-show="allTodo">
        <label>
            <input type="checkbox" v-model="isAll">
        </label>
        <span>
            <span>已完成{{doneTodo}}</span> /全部{{allTodo}}   
        </span>
        <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
    </div>
</template>

<script>
export default {
    name:'MyFooter',
    props:['todos'],
    computed:{
        allTodo(){
            return this.todos.length
        },
        doneTodo(){
            //return this.todos.filter(todo=>todo.done===true).length
           return this.todos.reduce((pre,current)=>pre + (current.done == true?1:0),0)
        },
        isAll:{
            get(){
                return this.doneTodo==this.allTodo && this.allTodo>0
            },
            set(value){
                // this.checkAllTodo(value)
                this.$emit('checkAllTodo',value)
            }
        }
    },
    methods: {
        clearAll(){
            // this.clearDoneTodo()
            this.$emit('clearDoneTodo')
        }
    },
}
</script>

<style scoped>
    .todo-footer{
        height: 40px;
        line-height: 40px;
        padding-left: 6px;
        margin-top: 5px;
    }

    .todo-footer label{
        display: inline-block;
        margin-right: 20px;
        cursor: pointer;
    }

    .todo-footer label input{
        position: relative;
        top: -1px;
        vertical-align: middle;
        margin-right: 5px;
    }

    .todo-footer button{
        float: right;
        margin-top: 5px;
    }

</style>