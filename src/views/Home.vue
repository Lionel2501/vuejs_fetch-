<template>
    <div v-show="showAddTask">
      <AddTask @add_task="addTask"/>
    </div>

    <Tasks 
      @toggle_task="toggle_task"
      @delete_task="onDelete" 
      :tasks="tasks" />
</template>

<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'

export default {
    name:'Home',
    props: {
        showAddTask:Boolean
    },
    components:{Tasks, AddTask},
    data(){
        return{
          tasks:[]
        }
    },
    async created(){
        this.tasks = await this.fetchTasks()
    },

    methods:{
        async fetchTasks(){
        const res = await fetch("http://localhost:5000/tasks")

        const data = await res.json()

        return data
        },

        async fetchTask(id){
        const res = await fetch(`http://localhost:5000/tasks/${id}`)

        const data = await res.json()

        return data
        },

        async addTask(task){
        const res = await fetch("http://localhost:5000/tasks",{
            method: 'POST',
            headers:{
            'Content-type': 'application/json'
            },
            body: JSON.stringify(task)
        })
        
        const data = await res.json()

        this.tasks = [...this.tasks, data]
        },

        async onDelete(id){
        if(confirm('Are you sure ?')){
            const res = await fetch(`http://localhost:5000/tasks/${id}`, {
            method: 'DELETE' })

            res.status === 200 ? 
            (this.tasks = this.tasks.filter((task) => task.id !== id))
            : alert('Error deleting task')
        }
        },

        async toggle_task(id){
        const taskToToggle = await this.fetchTask(id)
        const updTask = {...taskToToggle, reminder : !taskToToggle.reminder}

        const res = await fetch(`http://localhost:5000/tasks/${id}`, {
            method: 'PUT',
            headers:{
                'Content-type': 'application/json'
            },
            body: JSON.stringify(updTask)
            })

        const data = await res.json()

        this.tasks = this.tasks.map((task) => 
        task.id === id ? {...task, reminder: data.reminder} : task
        )
        },
    }
}
</script>