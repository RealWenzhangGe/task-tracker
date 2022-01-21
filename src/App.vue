<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
  <div v-show="showAddTask">
    <AddTask @add-task="addTask" />
  </div>
    
    <Tasks 
       @toggle-reminder="toggleReminder"
       @delete-task="deleteTask"
       :tasks="tasks" 
    />
  </div>
  
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    Header, 
    Tasks,
    AddTask
  }, 
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {    
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },    
    deleteTask(id) {
      if(confirm('Are you sure to delete that?')) {
        this.tasks = this.tasks.filter( (task) => task.id !== id ) //Because we want to delete the task, whose id is exactly what we passed in here, so we filter the tasks and keep those tasks whose id differs from the id passed in here
      }
    },
    toggleReminder(id){
        this.tasks = this.tasks.map( (task) => task.id === id ? {...task, reminder: !task.reminder} : task) //If the task.id equals to the id passed in here, then change its task.reminder to the opposite, otherwise keep it as it is
    },
    async fetchTasks() {
      const res = await fetch()

      const data = await res.json()

      return data
    },
    async created() {
      this.tasks = await this.fetchTasks()
    }
  }    
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid black;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000; 
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
