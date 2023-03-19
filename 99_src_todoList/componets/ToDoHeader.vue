<template>
    <div>
        <input type="text" @keyup.enter="add"/> 
     </div>
</template>

<script>
export default {
    name:"ToDoHeader",
    methods:{
        add(e){
            let obj = {
                id:Math.random().toString(),
                task:e.target.value,
                isDone:false
            }
            this.addtask(obj);
        }
    },
    props:["addtask"]
}
</script>

<style>

</style>