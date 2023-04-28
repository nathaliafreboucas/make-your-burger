<template>
  <Header />

  <router-view/>
  
  <Footer />
</template>

<script>
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
import { defineComponent } from 'vue';


export default defineComponent({
  name: 'App',
  components:{
    Header,
    Footer
  },
  
})
</script>

<style>
  * {
    font-family: Helvetica, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;

  }
  .main-container{
    margin: 50px;
    min-height: 250px;
  }
  h1{
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
  #app{
    height: 100vh;
    display: grid;
    grid-template-columns: 100%;
    grid-template-rows: 6rem auto 200px;
    grid-template-areas: 
    'header'
    'main'
    'footer'
    ;
  }

</style>
