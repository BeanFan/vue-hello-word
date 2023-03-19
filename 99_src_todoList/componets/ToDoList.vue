@<template>
    <ul class="ul_padding">
      <TransitionGroup name="todo">
      
        <ToDoItem
         v-for="taskItem in tasks" 
         :taskItem="taskItem" 
         :checkTask="checkTask" 
         :deleteSelectTask = "deleteSelectTask"
         :key="taskItem.id"></ToDoItem>   </TransitionGroup>
    </ul>
 
</template>

<script>
import ToDoItem from './ToDoItem.vue';
export default {
  data () {
    return {
    }
  },
  methods: {
  },
  components:{
    ToDoItem
  },
 name:"ToDoList",
props:["tasks","checkTask","deleteSelectTask"]
}
</script>

<style scoped lang="less">
    .ul_padding{
    padding:0px;
    .flex-space{
        display:flex;
        justify-content:space-between;
            background-color:coral;
            border:1px soid blue;
        
        
    }
}
    
	.todo-enter-active{
		animation: atguigu 0.5s linear;
	}

	.todo-leave-active{
		animation: atguigu 0.5s linear reverse;
	}

	@keyframes atguigu {
		from{
			transform: translateX(-100%);
		}
		to{
			transform: translateX(0px);
		}
	}
</style>
