<template>
    <header>
        <Navbar :logo="logo_src" :alt="app_name"/>
    </header>
    
</template>
<script>
import Navbar from './Navbar.vue';
import Banner from './Banner.vue';


export default {
    name: 'Header',
    components: {
        Navbar,
        Banner
    },
    data () {
    return {
      logo_src: '/img/logo.png',
      app_name: "Make Your Burger"
    }
  }
}
</script>

<style>
    header {
        grid-area: header;
    }
</style>