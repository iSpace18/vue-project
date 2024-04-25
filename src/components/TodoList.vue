vue
<template>
  <div class="todo-list">
    <h1>To-Do List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task">
    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        {{ task }}
        <button @click="removeTask(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push(this.newTask);
        this.newTask = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style>
.todo-list {
  max-width: 600px;
text-align:center;
margin:0 auto;

  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 15px;
}

.task-item {
  margin-top: 10px;
  padding: 10px;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task-item button {
  background-color: #ff6347;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 3px;
    transition:0.5s ease;
  cursor: pointer;
}

.task-item button:hover {
  background-color: red;
  transition:0.5s ease;
}

ul {
  list-style-type: none;
  padding: 0;
}

input {
  width: 100%;
  padding: 5px;
  margin-top: 10px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

h1 {
  text-align: center;
  margin-bottom: 10px;
  color: #333;
}
li{
  color:black;
  font-weight:bold;
  font-size:15px;
}
</style>