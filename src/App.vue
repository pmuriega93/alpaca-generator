<template>
 <div class="container">
    <h1 class="main-title">Alpaca Avatar Generator</h1>
    <main class="alpaca">
      
      <AlpacaImg :selectedOption="selected"/>
       
      <AlpacaSelector @setImage="setImage"/>
     
    </main>
 </div>
</template>

<script>
import AlpacaSelector from '@/components/AlpacaSelector.vue'
import AlpacaImg from '@/components/AlpacaImg.vue'

export default {
  name: 'App',
  components: {
    AlpacaSelector,
    AlpacaImg,
  },
  data() {
    return {
      selected: null,
    }
  },
  methods: {
    setImage(option) {
      this.selected = option
    }
  }
}
</script>

<style>
  *,
  *::before,
  *::after {
    margin: 0;
    padding: 0;
  }

  html {
    box-sizing: inherit;
    font-size: 62.5%;
    font-family: 'Karma', serif;
  }

  body {
    box-sizing: border-box;
    background-color: #FAF9F9;
    color: #555B6E;
    margin: 2rem;
    text-align: center;
  }

  .main-title {
      font-size: 4.5rem;
  }
  .alpaca {
      width: 100vw;
      display: grid;
      height: 90rem;
      grid-template-columns: repeat(2, 1fr)
  }

</style>
