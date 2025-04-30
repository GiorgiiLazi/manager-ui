<template>
  <Mode @changeMode = 'handleLightMode' />
  <List/>
</template>

<script>
import List from './components/List.vue';
import Mode from './components/Mode.vue';

export default {
  name: 'App',
  components: {
    Mode, List
  },
  methods:{
    handleLightMode(data){
      console.log(data)
      if(data === true){
        document.documentElement.classList.remove('dark')
        document.documentElement.classList.add('light')
      }
      else{
        document.documentElement.classList.add('dark')
        document.documentElement.classList.remove('light')
      }
    }
  },

}
</script>

<style>

html {
  background: rgb(9, 15, 45);
  font-family: "Oswald";
  width: 100%;
  box-sizing: border-box;
}
.light{
  background: rgb(109, 129, 211);
}
.dark{
  background: rgb(9, 15, 45);
}

</style>
