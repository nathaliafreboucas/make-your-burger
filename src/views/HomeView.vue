<template>
  <main>
    <Banner />
    <section class="main-container">
      <h1>Monte o seu burger:</h1>
      <Burgerform />
    </section>
  </main>
  
</template>

<script>
import Banner from '../components/Banner.vue';
import Burgerform from '../components/Burgerform.vue';

export default{
  name: 'HomeView',
  components:{
    Banner,
    Burgerform
  },
  
}

</script>
<style>
  main{
    grid-area: main;
    margin: 0;
  }
</style>
