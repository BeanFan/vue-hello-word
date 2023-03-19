<template>
    <li>
            <div class="flex-space">
                <label>
                    <input type="checkbox" v-bind:checked="taskItem.isDone" @change="checkTask(taskItem.id)" />
                    <input ref="editInputRef" @blur="commitEdit(taskItem, $event)" class="input_edit" v-if="taskItem.isEdit"
                        :value="taskItem.task" />
                </label>
                <div v-show="!taskItem.isEdit">{{ taskItem.task }}</div>
                <div>
                    <button class="btn_delete" @click="deleteSelectTask(taskItem.id)"> 删除</button>
                    <button ckass="btn_edit" v-show="!taskItem.isEdit" @click="handleEdit(taskItem)"> 编辑</button>
                </div>
            </div>
    </li>
</template>
<script>
export default {
    name: "ToDoItem",
    props: ["checkTask", "taskItem", "deleteSelectTask"],
    methods: {
        handleEdit(task) {
            if (task.isEdit === undefined) {
                this.$set(task, "isEdit", true)
            } else {
                task.isEdit = true;
            }
            // setTimeout(() => {
            //     this.$refs.editInputRef.focus();
            // }, 0); //获取焦点
            this.$nextTick(function () {
                this.$refs.editInputRef.focus();
            })
        },
        commitEdit(task, event) {
            if (event.target.value.trim() == "") {
                task.isEdit = false;
                return alert("输入不能为空");

            } else {
                task.task = event.target.value;
                task.isEdit = false;
            }
        }
    }
}
</script>

<style>
.flex-space {

    display: flex;
    background-color: rgb(90, 53, 132);
    justify-content: space-between;

}

.btn_edit {
    background-color: rgb(39, 108, 154);
}

.btn_delete {
    background-color: brown;
}

.input_edit {
    min-width: 300px;
}



</style>