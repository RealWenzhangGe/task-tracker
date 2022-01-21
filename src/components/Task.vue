<template>
<div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3> 
        {{task.text}}
        <button class="delete-button" @click="$emit('delete-task', task.id)">
            <i class="fas fa-times"></i>
        </button>
    </h3>
    <p> {{task.day}} </p>
</div>
    
</template>

<script>
export default {
    name: 'Task', 
    props: {
        task: Object
    }
}
</script>

<style scoped>
.delete-button {
    border: hidden;
    color: red;
}

.delete-button :hover {
    cursor: pointer;
    transform: scale(1.12);
}

.task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
}

.task.reminder {
    border-left: 5px solid green;
}

.task h3 {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>
