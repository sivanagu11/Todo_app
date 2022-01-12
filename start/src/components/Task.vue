<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1>Todo Task List</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input type="text" placeholder="New Task"  v-model="newTask"/>
        <button @click="addTask"><i class="fas fa-plus"></i></button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <ul>
          <task-item v-bind:task="task" v-for="task in tasks" :key="task.id"
          @Remove="removeTask(index)">
          @complete="completeTask(task)"</task-item>
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click="clearcompleted">Clear completed</button>
        <button @click="clearAll">Clear all</button>
      </div>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{incomplete}} </span>
      </div>
    </div>
  </div>
</template>

<script>
import TaskItem from './task.item';
export default {
  name: "Task",
  props: ['tasks'],
  components: {
    TaskItem
  },
  data() {
    return{
         newTask:"",
    }   
  },
  computed: {
    incomplete() {
        return this.tasks.filter(this.inprogress).length;
    }
  },
  methods: {
    addTask() {
      if(this.newTask) {
          this.tasks.push({
            title: this.newTask,
            completed: false
          });
          this.newTask = "";
      }
    },
    inprogress(task){
      return !this.iscompleted(task);
    },
    iscompleted(task) {
         return task.completed;
    },
    clearcompleted(){
          this.tasks = this.tasks.filter(this.inprogress)
    },
    clearAll() {
      this.tasks = [];
    },
    removeTask(index) {
      this.tasks.splice(index,1)

    },
    completeTask(task) {
      task.completed = !task.completed
    }

  },

};
</script>
