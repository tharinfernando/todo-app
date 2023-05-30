<template>
    <div class="ml-10">
        <button class="bg-blue-700 hover:bg-blue-600 w-16 h-10 text-white rounded active:bg-blue-700 shadow-md">
            {{ text }}
        </button>
    </div>
</template>

<script>
export default {
    name: "AddButton",
    props: {
        text: String,
    },
}
</script>