<template>
    <div id="app">
      <Juego msg="Bienvenido a Asesino de monstruos Vue-cli App"/>
    </div>
</template>


<script>
import Juego from './components/Juego.vue'

export default {
  name: 'App',
  components: {
    Juego
  }
}
</script>

<style>
#app {

}

.controls {
      margin-top: 30px;
      text-align: center;
      padding: 10px;
      border: 1px solid #ccc;
      box-shadow: 0px 3px 6px #ccc;
}


</style>
