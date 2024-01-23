<template>
<Header />
<div class="flex justify-center mt-10">
  <div>
    <Item />
  </div>
</div>
</template>

<script>
import Header from './components/Header.vue';
import Item from './components/Item.vue';

export default {
components :{
    Item,
    Header
},
}
</script>