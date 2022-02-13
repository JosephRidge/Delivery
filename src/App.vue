<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from "./components/HelloWorld.vue";
import AddDeliveryDetail from "./components/AddDeliveryDetail.vue";
import Deliveries from "./components/Deliveries.vue";
</script>

<template>
   <div class="flex  h-3/4 ">
    <AddDeliveryDetail class="   "/>
    <div class=" overflow-y-auto "  style="height: 800px; scrollbar-width: none; overflow-x: auto"><Deliveries /></div>
  </div>
</template>

<style> 
</style>
