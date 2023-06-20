<template>
<SideBar />
<div class="flex justify-center mt-10">
  <div>
    <Item />
  </div>
</div>
</template>

<script>
import Item from './components/Item.vue';
import SideBar from './components/SideBar.vue';

export default {
components :{
  Item,
  SideBar,
},
}
</script>