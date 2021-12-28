<template>
    <ul class="todo-main">
        <my-item 
            v-for="todoObj in todos" 
            :key='todoObj.id' 
            :todo="todoObj"
        />            
    </ul>
</template>

<script>
import MyItem from './MyItem.vue'
export default {
    components: { MyItem },
    name:'MyList',
    props:['todos']
}
</script>

<style scoped>
    .todo-main {
        margin-left: 0px;
        border: 1px solid #ddd;
        border-radius: 2px;
        padding: 0px;
        overflow: hidden;
    }

    .todo-empty{
        height: 40px;
        line-height: 40px;
        border: 1px solid #ddd;
        border-radius: 2px;
        padding-left: 5px;
        margin-top: 10px;
    }

</style>