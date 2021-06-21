<template>
    <div v-for="task in tasks" :key="task.id">
        <Task 
            @toggle_reminder="$emit('toggle_task', task.id)"
            @delete_task="$emit('delete_task', task.id)" 
            :task="task"/>
    </div>
</template>

<script>
import Task from './Task'

export default {
    name:'Tasks',
    components:{
        Task
    },
    props:{
        tasks:Array
    },
    emits:['delete_task', 'toggle_task']
}
</script>