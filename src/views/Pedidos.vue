<template>
  <main>
    <div class="main-container">
      <h1>Gerenciar Pedidos</h1>
      <Dashboard />
    </div>
  </main>
  
</template>
<script>
import { defineComponent } from 'vue';
import Dashboard from '../components/Dashboard.vue';

export default defineComponent({
  name: 'Pedidos',
  components: {
    Dashboard
  }
})
</script>

<style>

</style>