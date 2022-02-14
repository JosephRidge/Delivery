<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from "./components/HelloWorld.vue";
import AddDeliveryDetail from "./components/AddDeliveryDetail.vue";
import Deliveries from "./components/Deliveries.vue";
</script>

<template>
<div class="flex flex-col  ">
  <div class="bg-amber-900 sticky h-4"></div>
  <div class="flex bg-amber-100 "> 
<span> <img src="src/assets/logo.png" 
alt="Company Logo" srcset="" class="h-36 rounded mx-28 my-6  ">
  </span>
    <div class="mt-20 text-3xl text-amber-800 font-bold capitalize underline "> Welcome to JayAfrique Delivery Dashboard</div>
   
  </div>
   <div class="flex justify-center bg-amber-50 pt-5">
  <div>
    <div class="mx-10 text-amber-800 font-bold text-center ">Current Deliveries</div>
<AddDeliveryDetail class="  "/>
  </div>
    
    
    <div class="overflow-y-auto pb-28" 
     style="height: 800px; scrollbar-width: none; overflow-x: auto">
        <div class="mx-10 text-amber-800 font-bold text-center sticky">Current Deliveries</div>
     <Deliveries /></div>
   
  </div>
</div>
</template>

<style> 
</style>
