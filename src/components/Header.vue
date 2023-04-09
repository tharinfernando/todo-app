<template>
    <header class="bg-black h-12">
        <h1 class="text-lg text-gray-400 ml-10 pt-2">
            {{ title }}
        </h1>
    </header>
</template>

<script>
export default{
    name: "TopHeader",
    props: {
      title: String,
    },
}
</script>