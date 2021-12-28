<template>
    <transition name="todo" appear>
        <li>
            <label>
                <input type="checkbox" :checked="todo.done" @change="handleCheck(todo.id)">
                <span v-show="!todo.isEdit">{{todo.title}}</span>
                <input
                    type="text"
                    v-show="todo.isEdit"
                    :value="todo.title"
                    @blur="handleBlur(todo,$event)"
                    ref="inputTitle"
                >
            </label>
        
            <button class="btn btn-danger" @click="handleDelete(todo.id)">删除</button>
            <button class="btn btn-edit" @click="handleEdit(todo)" v-show="!todo.isEdit">编辑</button>
        </li>
    </transition>
</template>

<script>
export default {
    name:'MyItem',
    props:['todo'],
    methods: {
        handleCheck(id){
            // this.checkTodo(id)
            this.$bus.$emit('checkTodo',id)
        },
        handleDelete(id){
            if(confirm('确定要删除吗？')){
            //    this.deleteTodo(id) 
            this.$bus.$emit('deleteTodo',id)
            }
           
        },
        handleEdit(todo){
            if(Object.prototype.hasOwnProperty.call(todo,'isEdit')){
               todo.isEdit = true 
            }else{
                this.$set(todo,'isEdit',true)
            console.log(123);}
            this.$nextTick(()=>{
                this.$refs.inputTitle.focus()
            }
            )
        },
        //失去焦点
        handleBlur(todo,e){
            //切换显示类型
            todo.isEdit=false
            //输入不能为空
            if(!e.target.value.trim()){
                return alert('输入不能为空')
            }
            //触发总线修改的函数
            this.$bus.$emit('updateTodo',todo.id,e.target.value)
            // this.$set(todo,'title',e.target.value)
        }
    },
}
</script>

<style scoped>
    li{
        list-style: none;
        height: 36px;
        line-height: 36px;
        padding: 0 5px;
        border-bottom: 1px solid #ddd;
    }

    li label{
        float: left;
        cursor: pointer;
    }

    li label li input {
        vertical-align: middle;
        margin-right: 6px;
        position: relative;
        top:-1px;
    }

    li button{
        float: right;
        display: none;
        margin-top: 3px;
    }

    li:before{
        content: initial;
    }

    li:last-child {
        border-bottom:none;
    }

    li:hover{
        background-color: #ddd;
    }

    li:hover button{
        display: block;
    }

    /* 动画效果 */
    .todo-enter-active{
        animation: animat 0.5s ease;
    }
    .todo-leave-active{
        animation: animat 0.5s ease reverse;
    }

    @keyframes animat{
        from{
            transform: translateX(-100%);
        }
        to{
            transform: translateX(0);
        }
    }
</style>