<template>
  <Header title="ToDo List" class="text-center"/>
  <div class="mx-52 mt-10">
    <div class="mt-10 mb-10">
      <Item />
    </div>
  </div>
</template>

<script>
import Item from './components/Item.vue';
import Header from './components/Header.vue';

export default {
components :{
  Item,
  Header,
},
}
</script>