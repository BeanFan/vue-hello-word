<template>
<div>
    <ToDoHeader :addtask="addtask"/>
    <ToDoList :tasks="tasks" :deleteSelectTask="deleteSelectTask"
    :checkTask="checkTask"/>
    <ToDoFooter :checkAll="checkAll" :tasks = "tasks"/>
</div>
</template>

<script>
import ToDoFooter from './componets/ToDoFooter';
import ToDoHeader from './componets/ToDoHeader';

import ToDoList from './componets/ToDoList';
// import ToDo from '@/componets/ToDo'

export default {
    data(){
        return{
            tasks:JSON.parse((localStorage.getItem("todo_task")||"[]"))
        };
    },
    components:{
        ToDoFooter,ToDoList,ToDoHeader
    },
    methods:{
        addtask(task){
            this.tasks.unshift(task);
        },
        deleteDoneTask(){
            
            this.tasks = this.tasks.filter(item=>{
                return item.isDone == false;
            })
            console.log(this.tasks)
        },
        deleteSelectTask(id){
            this.tasks = this.tasks.filter(item=>{
                return item.id!=id;
            })
        },
        
        checkTask(id){
            this.tasks.find(item=>item.id==id).isDone=!this.tasks.find(item=>item.id==id).isDone;
           
        },
        checkAll(value){
            this.tasks.forEach(item=>{
                item.isDone = value;
            });
        }
        
        
    },
    mounted(){
        this.$bus.$on("deleteDoneTask",this.deleteDoneTask); //绑定全局时间
    },
    beforeDestroy(){
        this.$bus.$off("deleteDoneTask");//关闭绑定全局事件
    },
    watch:{
        tasks:{
            deep:true,
            handler:function(value1,value2)
            {
                console.log(value1,value2);
                localStorage.setItem("todo_task",JSON.stringify(value1));
            }
            
        }   
    }
}
</script>

<style>

</style>