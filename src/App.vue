<template>
  <div class="fondo">
    <!-- Barra de navegación -->
    <Navbar />
    <AppConvertidor />
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import AppConvertidor from './components/Convertidor.vue';

export default {
  name: 'App',
  components: {
    Navbar,
    AppConvertidor
  }
};
</script>

<style>
/* Estilos generales opcionales */
body {
  background-color: #f8f9fa;
  font-family: Arial, Helvetica, sans-serif;
  margin: 0;
  padding: 0;
}

#app {
  text-align: center;
  padding: 20px;
}

.fondo{
  background-image: url('./assets/fondo1.jpg');
  height: 100vh;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}
</style>
