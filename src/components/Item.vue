<template>
  <div>
    <h2 class="text-3xl font-bold mb-2">ToDo List</h2>
    <div class="flex mx-16 mt-8 mb-10">
      <input type="text" v-model="newTaskName" class="border border-gray-300 text-gray-900 rounded block w-full h-10 p-2.5" placeholder="New Task" @keydown.enter="addTask" />
      <AddButton @click="addTask" text="add" />
    </div>
    <ul v-for="(task, index) in tasks" :key="task.name" class="mb-3">
      <li class="relative flex items-center p-8 rounded-lg border hover:bg-gray-50">
        <input type="checkbox" v-model="task.completed" class="cursor-pointer" @change="completeTask(task, index)" />
        <label :for="'task-'" class="px-10" :class="{ 'line-through text-gray-500': task.completed }">{{ task.name }}</label>
        <DeleteIcon @click="removeTask(task, index)" class="absolute right-10 cursor-pointer hover:stroke-black " />
      </li>
    </ul>
    
    <hr class="my-5">
    
    <h2 class="text-2xl font-bold mb-2">Completed</h2>
    <ul v-for="(task, index) in completeTasks" :key="task.name" class="mb-3">
      <li class="relative flex items-center p-8 rounded-lg border hover:bg-gray-50">
        <input type="checkbox" v-model="task.completed" class="cursor-pointer"/>
        <label :for="'done-task-'" class="px-10 line-through text-gray-500">{{ task.name }}</label>
        <DeleteIcon @click="removeTask(task, index, true)" class="absolute right-10 cursor-pointer hover:stroke-black " />
      </li>
    </ul>
  </div>
</template>

<script>
import DeleteIcon from './Icons/DeleteIcon.vue';
import AddButton from './Button.vue';

export default {
  name: "ItemTask",
  props: {
    taskname: String,
  },
  components: { 
    DeleteIcon,
    AddButton,
  },
    
  data() {
    return {
      newTaskName: '',
      tasks: [
        { name: 'Task 1', completed: false },
        { name: 'Task 2', completed: false },
        { name: 'Task 3', completed: false },
      ],
      completeTasks: [
        { name: 'Task 01', completed: true },
      ],
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
    
    completeTask(task, index) {
      if (task.completed) {
        this.completeTasks.unshift(task);
        this.tasks.splice(index, 1);
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
  },
}
</script>
