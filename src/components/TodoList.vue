<template>
  <div class="todo-list">
    <h1>To-Do List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task">
    <ul>
      <li v-for="task in tasks" :key="task.id" class="task-item">
        <span v-if="task.id !== editedId">{{ task.text }}</span>
        <input v-else v-model="editedTask" @keyup.enter="saveTask" @keyup.esc="cancelEdit">
        <button @click="editTask(task.id)">Edit</button>
        <button @click="removeTask(task.id)">Remove</button>
        <button @click="pinTask(task.id)" :class="{ 'pinned': task.id === pinnedId }">Pin</button>
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
      editedId: -1,
      editedTask: '',
      pinnedId: -1,
      id: 0,
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({text:this.newTask, id:this.id});
        this.newTask = '';
        this.id++        
      }
    },
    removeTask(id) {
      const index = this.tasks.findIndex(el=>el.id==id)
      this.tasks.splice(index, 1)
    },
    editTask(id) {
      const editedIndex = this.tasks.findIndex(el=>el.id==id)
      this.editedId = id
      this.editedTask = this.tasks[editedIndex].text
    },
    saveTask() {
      if (this.editedTask.trim() !== '') {
        const editedIndex = this.tasks.findIndex(el=>el.id==this.editedId)
function twoSum(nums, target) {
    const sortedNums = nums.map((num, index) => [num, index]).sort((a, b) => a[0] - b[0]);
    let left = 0;
    let right = sortedNums.length - 1;
    
    while (left < right) {
        const sum = sortedNums[left][0] + sortedNums[right][0];
        if (sum === target) {
            return [sortedNums[left][1], sortedNums[right][1]];
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    
    return [];
}
        this.editedId = -1;
        this.editedTask = '';
      }
    },
    cancelEdit() {
      this.editedId = -1;
      this.editedTask = '';
    },
    pinTask(id) {
      if (this.pinnedId == id) {
        this.pinnedId = -1
        return
      }
      this.pinnedId = id;
      const index = this.tasks.findIndex(el=>el.id==id)
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