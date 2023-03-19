<template>
<div class="to_do_footer">
    <done-to-do></done-to-do>
    
    <span>
        <label> 
			<!-- <input type="checkbox" :checked="isAll" @change="checkAll"/> -->
        <input type="checkbox" v-model="isAll"/>
    </label>
        <span>已完成{{doneTotal}}</span> / 全部{{total}}
    </span>
</div>
</template>

<script>
import DoneToDo from './DoneToDo.vue';
export default {
  props:["tasks","checkAll"],
  components: { DoneToDo},
    computed:{
    total(){
		return this.tasks.length
    },
    //已完成数
    doneTotal(){
        return this.tasks.reduce((pre,todo)=> pre + (todo.isDone ? 1 : 0) ,0)
    },
    isAll:{
        set(value){
           this.checkAll(value)
        },
        get(){
            return this.total == this.doneTotal && this.doneTotal>0;
        }
    }
    
  },

}
</script>

<style>
.to_do_footer{
    display:flex;
    justify-content: space-between;

}
</style>