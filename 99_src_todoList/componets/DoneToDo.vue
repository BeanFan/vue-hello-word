@<template>
    <div><button @click="deleteDoneTask">delete done task</button></div>
</template>

<script>
export default {
    name:"DoneToDo",
    methods:{
        deleteDoneTask(){
            this.$bus.$emit("deleteDoneTask");
        }
    }
}
</script>

<style>

</style>