<template>
    <form @submit="saveTask" class="add-form" action="" method="">
        <div class="form-control">
            <label class="form-control label" for="">Task Name</label>
            <input v-model="text" name="text" class="form-control input" type="text">
        </div>
        <div class="form-control">
            <label class="form-control label"  for="">Date</label>
            <input v-model="day" name="day" class="form-control input" type="text">
        </div>
        <div class="form-control-check">
            <label class="form-control-check label" for="">Reminder</label>
            <input v-model="reminder" name="reminder" class="form-control-check input" type="checkbox">
        </div>
        <input class="btn" type="submit" value="Save Task">
    </form>
</template>

<script>
export default {
    name:'AddTask',
    data(){
        return {
            text: '',
            day: '',
            reminder:false
        }
    },
    methods:{
        saveTask(e){
            e.preventDefault()
            if(!this.text){
                alert('please add new task')
                return
            }
            const newTask = {
                id : Math.floor(Math.random * 10000),
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }

            this.$emit('add_task', newTask)

            this.text = ''
            this.day = ''
            this.reminder = false
        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
.btn{
    margin-top: 30px;
    width: 100%;
    padding: 10px;
    background-color: darkslategray;
}
</style>