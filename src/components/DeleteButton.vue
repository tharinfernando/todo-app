<template>
    <div class="ml-10">
        <button class="bg-red-500 hover:bg-red-600 w-24 h-10 text-white rounded active:bg-red-700 ">
            {{ text }}
        </button>
    </div>
</template>

<script>
export default {
    name: "DeleteButton",
    props: {
        text: String,
    },
}
</script>