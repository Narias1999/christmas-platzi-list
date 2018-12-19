<template>
  <div id="app">
    <header>
      <h1>Lista de tareas de Platzi Navidad</h1>

      <div class="add-task-container">
        <input type="text" 
        @keyup.enter="addTask" 
        v-model="taskModel" 
        placeholder="Tarea..." 
        />
        <button class="btn" @click="addTask">Agendar</button>
      </div>
    </header>

    <section class="tasks-container">
      <div class="tasks" v-if="tasks.length">
        <h2>Tareas</h2>
        <list-item v-for="task in tasks" :key="JSON.stringify(task.date)" :task="task" 
        @check="setLocalStorage"
        @delete="deleteTask(task)"/>
      </div>
      <div class="no-tasks" v-else>
        <h2>Aún no hay tareas :)</h2>
      </div>
    </section>
  </div>
</template>
<script>
import ListItem from './components/ListItem.vue'
export default {
  name: 'app',
  components: { ListItem },
  data () {
    return {
      tasks: [],
      taskModel: ''
    }
  },
  methods: {
    addTask() {
      if (!this.taskModel) return

      const task = {
        text: this.taskModel,
        checked: false,
        date: new Date()
      }
      this.tasks.unshift(task)
      this.setLocalStorage()
      this.taskModel = ''
    },
    deleteTask (task) {
      this.tasks = this.tasks.filter(t => t.date != task.date)
      this.setLocalStorage()
    },
    setLocalStorage () {
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    }
  },
  mounted () {
    const tasks = localStorage.getItem('tasks')
    this.tasks = JSON.parse(tasks) || []
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Lato|Mountains+of+Christmas:700');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
/* global variables */
:root {
  --primary-text:#34495e;
  --primary-text-ligth:#3c536b;
  --white: #ecf0f1;
  --error: #cf3220;
  --error-ligth: #e74c3c;
  --green-one: #8cb513;
  --green-two: #a3c932;
}
body {
  background: var(--white);
  color: var(--primary-text);
  font-family: 'Lato', sans-serif;
}
header {
  background: linear-gradient(135deg, var(--green-one) 0%,var(--green-two) 100%);
  text-align: center;
  padding: 70px 0;
  color: #fff;
}
h1 {
  font-family: 'Mountains of Christmas', cursive;
  padding-bottom: 20px;
}
header .add-task-container {
  width: 400px;
  max-width: 90%;
  display: flex;
  justify-content: space-between;
  margin: 0 auto;
  color: var(--white);
}
header input::placeholder {
  color: var(--white);
}
header input {
    font-family: 'Lato', sans-serif;
    background: rgba(0, 0, 0, .17);
    border: 0;
    width: 90%;
    font-size: 16px;
    margin-right: 10px;
    border-radius: 3px;
    padding: 10px;
    outline: none;
    color: #fff;
}
.btn {
  outline: none;
  border: 0;
  background: var(--primary-text);
  font-weight: bold;
  cursor: pointer;
  color: var(--white);
  text-decoration: none;
  border-radius: 3px;
  padding: 0 15px;
  transition: .3s;
}
header .btn:hover {
  background: var(--primary-text-ligth);
}
.tasks-container {
  width: 500px;
  max-width: 90%;
  padding: 20px 0;
  margin: 0 auto;
}
.tasks-container .tasks > div:last-child {
  border: 0 !important;
}
h2 {
  padding-bottom: 10px;
  text-align: center;
}
</style>
