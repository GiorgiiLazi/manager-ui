<template>
  <div class="container">
    <div class="title">
      <div class="title-img">
        <img src="/assets/logo.svg" alt="Logo" />
      </div>
    </div>

    <div class="light-mode">
      <span 
      v-if="lightMode" 
      @click="changeMode"
      class="material-symbols-outlined">
        light_mode
      </span>
      <span 
      v-else
      @click="changeMode"
      class="material-symbols-outlined"
      >
        dark_mode
      </span>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['changeMode'])
const lightMode = ref(false)

const changeMode = () =>{
  lightMode.value =! lightMode.value
  
  emit('changeMode', lightMode.value)
}

</script>

<style>
.container{
  background: rgba(204, 204, 204, 0.5);
  color: white;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 0 50px;
  border-radius: 8px;
  font-size: 1.2em
}
.title{
  max-width: 500px;
}
.title >*{
  color: white;
  margin: 0 10px;
  padding: 20px;
}
.light-mode span{
  cursor: pointer;
  margin: 0 10px;
  padding: 20px;
}
</style>