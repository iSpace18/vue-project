<template>
  <div class="todo-list">
    <h1>To-Do List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task">
    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <span v-if="index !== editedIndex">{{ task }}</span>
        <input v-else v-model="editedTask" @keyup.enter="saveTask" @keyup.esc="cancelEdit">
        <button @click="editTask(index)">Edit</button>
        <button @click="removeTask(index)">Remove</button>
        <button @click="pinTask(index)" :class="{ 'pinned': index === pinnedIndex }">Pin</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      editedIndex: -1,
      editedTask: '',
      pinnedIndex: -1
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
    },
    editTask(index) {
      this.editedIndex = index;
      this.editedTask = this.tasks[index];
    },
    saveTask() {
      if (this.editedTask.trim() !== '') {
        this.tasks[this.editedIndex] = this.editedTask;
        this.editedIndex = -1;
        this.editedTask = '';
      }
    },
    cancelEdit() {
      this.editedIndex = -1;
      this.editedTask = '';
    },
    pinTask(index) {
      this.pinnedIndex = index;
      const pinnedTask = this.tasks.splice(index, 1);
      this.tasks.unshift(pinnedTask[0]);
    }
  }
};
</script>

<style>
.todo-list {
  max-width: 2600px;
  text-align: center;
  margin: 0 auto;
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
  transition: 0.5s ease;
  cursor: pointer;
}
.task-item button.pinned {
  background-color: #32CD32; /* Green color for pinned tasks */
}
.task-item button:hover {
  background-color: red;
  transition: 0.5s ease;
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
li {
  color: black;
  font-weight: bold;
  font-size: 15px;
}
button {
  margin-left: 10px;
}
</style>