<template>
    <div>
        <div class="flex mx-16 mt-8 mb-10">
            <input type="text" v-model="newTaskName" class="border border-gray-300 text-gray-900 rounded block w-full h-10 p-2.5" placeholder="New Task"/>
            <AddButton @click="addTask(index)" text="add"/>
        </div>
        <ul v-for="(task, index) in tasks" :key="task.id">
            <li class="relative flex items-center p-8 rounded-lg border">
                <input type="checkbox" :id="'task-' + task.id" v-model="task.completed"/>
                <label :for="'task-' + task.id" class="px-10" :class="{ 'line-through': task.completed }">{{ task.name }}</label>
                <DeleteIcon @click="removeTask(index)" class="absolute right-10 cursor-pointer hover:stroke-black" />
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
      tasks: [
        { name: 'Task 1'},
        { name: 'Task 2'},
        { name: 'Task 3'},
      ],
      newTaskName: '',
    };
  },
  methods: {
    addTask() {
      if (this.newTaskName.trim() !== '') {
        const newTask = {
          id: Date.now(),
          name: this.newTaskName.trim(),
        };
        this.tasks.push(newTask);
        this.newTaskName = '';
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
  },
}
</script>