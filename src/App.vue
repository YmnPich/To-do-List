<template>
  <div class="input-container" style="width: 600px; height: 400px; margin: auto; background-color: #121212; margin-top: 100px; padding: 20px 30px; border-radius: 20px;"> 
    <div style="font-size: 22px; font-family: Robotic; margin-bottom: 20px;">To-do List</div>
    <v-text-field
      flat
      class="pill-input"
      placeholder="Enter task"
      v-model="newTask"
      append-inner
    >
      <template #append>
        <v-btn
          color="primary"
          class="pill-button"
          rounded
          small
          @click="addTask"
        >
          Add Task
        </v-btn>
      </template>
    </v-text-field>
    <div>
      <ul style="margin-left: 40px;">
        <li v-for="(task, index) in tasks" :key="index" :class="{ checked: task.checked }">
          <div class="circle-icon" @click.stop="toggleTask(index)"></div>
          <span v-if="!task.editMode"style = "padding-left: 10px;">{{ task.text }}</span>
          <input v-else v-model="task.text" @keyup.enter="updateTask(index)" @blur="updateTask(index)" />
          <img class="edit-icon" src="./assets/edit.png" @click.stop="editTask(index)">
          <img src="./assets/close.png" @click.stop="deleteTask(index)" class="delete-icon">
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ text: this.newTask, checked: false, editMode: false });
        this.newTask = '';
      }
    },
    toggleTask(index) {
      this.tasks[index].checked = !this.tasks[index].checked;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.tasks[index].editMode = true;
    },
    updateTask(index) {
      this.tasks[index].editMode = false;
    },
  },
};
</script>

<style>
ul li {
  list-style: none;
  font-size: 18px;
  padding: 10px 0;
  user-select: none;
  display: flex;
  align-items: center;
  position: relative;
  
}

.circle-icon {
  height: 28px;
  width: 28px;
  border-radius: 50%;
  background-image: url('./assets/unchecked.png');
  background-size: contain;
  background-position: center;
  cursor: pointer;
  /* margin-right: 10px; */
  margin-left: -35px;
}

ul li.checked .circle-icon {
  background-image: url('./assets/checked.png');
}

ul li.checked {
  color: #555;
  text-decoration: line-through;
}

.delete-icon {
  width: 20px;
  height: 20px;
  margin-left: 10px;
  cursor: pointer;
}
.edit-icon {
  margin-left: auto;
  cursor: pointer;
  width: 20px;
  height: 20px;
  background-size: contain;
}
</style>
