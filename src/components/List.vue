<template>
  <header class="header-title">
    <h2>Extensions List</h2>
    <div class="buttons">
        <button @click="handleAll" class="btns">All</button>
        <button @click="handleActive" class="btns">Active</button>
        <button @click="handleinactive" class="btns">Inactive</button>
    </div>
  </header>

  <main class="list">
    <div v-if="showAll" class="cards" v-for="card in cards" :key="card">
        <div class="uper-row">
            <div class="img-container">
                <img :src="card.logo" :alt="card.logo">
            </div>
            <div class="card-desc">
                <h3 class="card-title">
                    {{ card.name }}
                </h3>
                <p class="card-text">
                    {{ card.description }}
                </p>
            </div>
        </div>
        <div class="bottom-row">
            <button class="remove-btn">
                Remove
            </button>
            <div>
                <label class="switch">
                    <input type="checkbox" v-model="card.isActive">
                    <span class="slider round"></span>
                </label>
            </div>
            
        </div>
    </div>

    <div v-else-if="showActive" class="cards" v-for="card in activeCards" :key="card.name">
        <div class="uper-row">
            <div class="img-container">
                <img :src="card.logo" :alt="card.logo">
            </div>
            <div class="card-desc">
                <h3 class="card-title">
                    {{ card.name }}
                </h3>
                <p class="card-text">
                    {{ card.description }}
                </p>
            </div>
        </div>
        <div class="bottom-row">
            <button class="remove-btn">
                Remove
            </button>
            <div>
                <label class="switch">
                    <input type="checkbox" v-model="card.isActive">
                    <span class="slider round"></span>
                </label>
            </div>
            
        </div>
    </div>

    <div v-else-if="showInActive" class="cards" v-for="card in inactiveCards" :key="card.name">
        <div class="uper-row">
            <div class="img-container">
                <img :src="card.logo" :alt="card.logo">
            </div>
            <div class="card-desc">
                <h3 class="card-title">
                    {{ card.name }}
                </h3>
                <p class="card-text">
                    {{ card.description }}
                </p>
            </div>
        </div>
        <div class="bottom-row">
            <button class="remove-btn">
                Remove
            </button>
            <div>
                <label class="switch">
                    <input type="checkbox" v-model="card.isActive">
                    <span class="slider round"></span>
                </label>
            </div>
            
        </div>
    </div>

  </main>
</template>

<script setup>
import { onMounted, computed, ref } from 'vue';

const showAll = ref(true)
const showActive = ref(false)
const showInActive = ref(false)
const cards = ref([])


const handleActive = () =>{
    showAll.value = false
    showActive.value = true
    showInActive.value = false
}
const handleinactive = () =>{
    showAll.value = false
    showActive.value = false
    showInActive.value = true
}
const handleAll = () =>{
    showAll.value = true
    showActive.value = false
    showInActive.value = false
}

onMounted(async()=>{
    const res = await fetch("/data/data.json")
    const data =  await res.json()
    cards.value = data
    console.log(cards.value)
})

const activeCards = computed(() =>
  cards.value.filter(card => card.isActive === true)
)

const inactiveCards = computed(() =>
  cards.value.filter(card => card.isActive === false)
)

</script>

<style scoped>
.header-title{
    color: white;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 20px;
}
.btns{
    background: rgba(204, 204, 204, 0.5);
    color: white;
    padding: 5px 15px;
    border-radius: 8px;
    margin: 0 10px;
    border: none;
}
.uper-row {
  display: flex;
  align-items: center; /* vertically center items */
  gap: 1rem; /* space between image and text */
}
.card-desc {
  flex: 1; /* let the description take remaining space */
}

.img-container img {
  width: 60px; /* or whatever size you want */
  height: auto;
  object-fit: contain;
}

.list{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    justify-items: center;
    align-items: center;
    flex-wrap: wrap;
    margin: 1em;
}
.cards{
    display: flex;
    flex: 1 1 300px;
    height: 200px;
    padding: 5px;
    border-radius: 8px;
    background: rgba(204, 204, 204, 0.5);
    display: inline-block;
    min-width: 30%;
    max-width: 400px;
    color: white;
}
.upper-row, .bottom-row{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
    /* The switch - the box around the slider */
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}
.card-desc{
    display: inline-block;
}
/* Hide default HTML checkbox */
.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}
.remove-btn{
    background: rgba(204, 204, 204, 0.5);
    color: white;
    border: none;
    padding: 5px;
    border-radius: 8px;
    cursor: pointer;
}
/* The slider */
.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>