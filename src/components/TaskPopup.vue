<template>
  <div class="flex justify-center items-center fixed top-0 left-0 w-screen h-screen bg-black">
    <div class="bg-white p-6 rounded-lg w-3/6	h-3/6">
      <CloseIcon @click="closePopup" class="text-red-500 cursor-pointer" />
      <div class="p-2">
        <h2 class="block w-full py-2.5 px-3 text-gray-900 border border-gray-300 rounded-lg">{{ task.name }}</h2>
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
  methods: {
    closePopup() {
      this.$emit("close");
    },
  },
};
</script>
