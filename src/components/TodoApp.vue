<template>
  <div class="container">
    <h2 class="text-center mt-6 red">My Todo App</h2>
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter your task" class="form-control">
    </div>
    <div>
      <button @click="submitTask" class="btn btn-success mt-3 rounded-0">Add task</button>
    </div>
    <!-- UNFINISHED TASKS -->
    <h4 class="text-center mt-3">Not finished tasks</h4>
    <ul class="list-group" v-for="(task, index) in tasks">
      <li v-if="task.status === 'todo'" class="list-group-item mt-2 shadow rounded">
        <input @click="changeStatus(index)" class="form-check-input me-1 " type="checkbox" value="" aria-label="...">
        {{task.name}}
        <button @click="deleteTask(index)" class="btn-close"></button>
      </li>
    </ul>
    <!-- FINISHED TASKS -->
    <h4 class="text-center mt-3">Finished tasks</h4>

    <ul class="list-group" v-for="(task, index) in tasks">
      <li v-if="task.status === 'done'" class="list-group-item mt-2 shadow rounded">
        <input @click="changeStatus(index)" class="form-check-input me-1" type="checkbox" checked="checked" value="" aria-label="...">
        <del>{{task.name}}</del>
        <button @click="deleteTask(index)" class="btn-close "></button>

      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  data(){
    return {
      task: '',
      tasks: [
        {
          name: 'Create a frontend app',
          status: 'done'
        },
        {
          name: 'Get a job',
          status: 'todo'
        }
      ]
    }
  },
  methods: {
    submitTask() {
      if (this.task.length > 0) {
        this.tasks.push({
          name: this.task,
          status: "todo"
        })
        this.task = ''
      }
    },
    deleteTask(index){
        this.tasks.splice(index, 1)
    },
    changeStatus(index){
        let currentStatus = this.tasks[index].status
        if(currentStatus === "done"){
          this.tasks[index].status = "todo"
        }else{
          this.tasks[index].status = "done"
        }
    }
  }
}
</script>

<style scoped>

</style>