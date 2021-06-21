<template>
    <header>
        <h1>{{title}}</h1>
        <Buttons 
            @toggleForm="$emit('toggleForm')"
            :text="showAddTask ? 'Close' : 'Add Task'" 
            :color="[showAddTask ? 'red' : 'green']"/>
    </header>
</template>

<script>
import Buttons from './Buttons'

export default {
    name:'Header',
    components:{ Buttons },
    props: {
        title: String,
        showAddTask: Boolean
    }
}
</script>

<style scoped>

    header{
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-bottom: 20px;
    }
    
</style>