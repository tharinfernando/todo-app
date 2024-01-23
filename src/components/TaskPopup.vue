<template>
  <div class="flex justify-center items-center fixed top-0 left-0 w-screen h-screen bg-white/50">
    <div class="bg-white p-6 rounded-lg w-3/6 h-3/6 shadow-lg">
      <CloseIcon @click="closePopup" class="text-red-500 cursor-pointer" />
      <div class="p-2">
        <!-- Conditionally render editable input or display-only text -->
        <h2 v-if="!editing" @click="toggleEditing" class="block w-full py-2.5 px-3 text-gray-900 border border-gray-300 rounded-lg">{{ task.name }}</h2>
        <div v-else>
          <input v-model="editedTaskName" class="block w-full py-2.5 px-3 text-gray-900 border border-gray-300 rounded-lg" />
          <button @click="saveChanges" class="mt-2 bg-blue-500 text-white py-2 px-4 rounded">Save</button>
        </div>
      </div>
      <div class="p-2">
        <textarea rows="4" class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 outline-none" placeholder="Add note"></textarea>
      </div>
    </div>
  </div>
</template>

<script>
import CloseIcon from './Icons/CloseIcon.vue';

export default {
  name: "TaskPopup",

  props: {
    task: Object,
  },

  components: {
    CloseIcon,
  },

  data() {
    return {
      editing: false,
      editedTaskName: this.task.name,
    };
  },

  methods: {
    closePopup() {
      this.$emit("close");
    },
    toggleEditing() {
      if (this.editing) {
        this.editing = false;
        this.$emit("update-task-name", this.editedTaskName);
      } else {
        this.editing = true;
      }
    },
    saveChanges() {
      // Call toggleEditing to handle both starting and stopping editing
      this.toggleEditing();
    },
  },
};
</script>
