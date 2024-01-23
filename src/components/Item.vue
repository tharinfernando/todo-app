<template>
  <div>
    <div class="flex mx-16 mt-8 mb-10">
      <input type="text" v-model="newTaskName" class="border border-gray-300 text-gray-900 rounded block w-full h-10 p-2.5 outline-none" placeholder=" + Add a task" @keydown.enter="addTask" />
      <AddButton @click="addTask" text="add" />
      <AddButton @click="callAPI" text="API" />
      <DeleteButton @click="deleteAll" text="Delete All" />
    </div>
    <ul v-for="(task, index) in tasks" :key="task.name" class="mb-3">
      <li class="relative flex items-center p-4 rounded-lg border hover:bg-gray-50 shadow-lg">
        <input type="checkbox" v-model="task.completed" class="cursor-pointer" @change="completeTask(task, index)" />
        <label :for="'task-'" class="px-10" :class="{ 'line-through text-gray-500': task.completed }">{{ task.name }}</label>
        <DeleteIcon @click="removeTask(task, index)" class="absolute right-10 cursor-pointer hover:stroke-black" />
        <EditIcon @click="openTaskPopup(task)" class="absolute right-20 cursor-pointer hover:stroke-blue-600" />
      </li>
    </ul>
    <div v-if="completeTasks.length > 0">
      <hr class="my-5">
      <h2 class="text-2xl font-bold mb-2">Completed</h2>
      <ul v-for="(task, index) in completeTasks" :key="task.name" class="mb-3">
        <li class="relative flex items-center p-4 rounded-lg border hover:bg-gray-50 shadow-lg">
          <input type="checkbox" v-model="task.completed" class="cursor-pointer" @change="completeTask(task, index, true)" />
          <label :for="'done-task-'" class="px-10 line-through text-gray-500">{{ task.name }}</label>
          <DeleteIcon @click="removeTask(task, index, true)" class="absolute right-10 cursor-pointer hover:stroke-black " />
          <EditIcon @click="openTaskPopup(task)" class="absolute right-20 cursor-pointer hover:stroke-blue-600" />
        </li>
      </ul>
    </div>
    <TaskPopup v-if="showTaskPopup" :task="selectedTask" @close="closeTaskPopup" @update-task-name="updateTaskName" />
  </div>
</template>

<script>
import DeleteIcon from './Icons/DeleteIcon.vue';
import AddButton from './Button.vue';
import DeleteButton from './DeleteButton.vue';
import TaskPopup from './TaskPopup.vue';
import EditIcon from './Icons/EditIcon.vue';

export default {
  name: "ItemTask",
  props: {
    taskname: String,
  },
  components: { 
    DeleteIcon,
    AddButton,
    DeleteButton,
    TaskPopup,
    EditIcon,
  },
    
  data() {
    return {
      newTaskName: '',
      tasks: [],
      completeTasks: [],
      showTaskPopup: false,
      selectedTask: null
    };
  },
  
  methods: {
    addTask() {
      if (this.newTaskName !== '') {
        const newTask = {
          name: this.newTaskName,
          completed: false,
        };
        this.tasks.unshift(newTask);
        this.newTaskName = '';
      }
    },
    
    completeTask(task, index, fromCompleteList = false) {
      if (fromCompleteList) {
        if (!task.completed) {
          this.tasks.unshift(task);
          this.completeTasks.splice(index, 1);
        }
      } else {
        if (task.completed) {
          this.completeTasks.unshift(task);
          this.tasks.splice(index, 1);
        }
      }
    },
    
    removeTask(task, index, fromCompleteList = false) {
      if (fromCompleteList) {
        this.completeTasks.splice(index, 1);
      } else {
        this.tasks.splice(index, 1);
        if (task.completed) {
          const completeIndex = this.completeTasks.findIndex(completeTask => completeTask.name === task.name);
          if (completeIndex !== -1) {
            this.completeTasks.splice(completeIndex, 1);
          }
        }
      }
    },
    
    deleteAll() {
      this.tasks = [];
      this.completeTasks = [];
    },
    
    callAPI() {
      fetch('https://jsonplaceholder.typicode.com/posts')
        .then(response => response.json())
        .then(json => {
         this.tasks = json.map(task => ({
            name: task.title,
           completed: false,
         }));
        });
     },

    openTaskPopup(task) {
      this.selectedTask = task;
      this.showTaskPopup = true;
    },

    closeTaskPopup() {
      this.selectedTask = null;
      this.showTaskPopup = false;
    },

    updateTaskName(updatedTaskName) {
      const index = this.tasks.findIndex(task => task === this.selectedTask);
      if (index !== -1) {
        this.tasks[index].name = updatedTaskName;
      }

      const completeIndex = this.completeTasks.findIndex(task => task === this.selectedTask);
      if (completeIndex !== -1) {
        this.completeTasks[completeIndex].name = updatedTaskName;
      }
    },
  },
};
</script>
