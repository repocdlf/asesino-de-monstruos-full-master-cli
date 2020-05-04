<template>

  <section class="src-components-botones">
    <section class="row controls" v-if="!hayUnaPartidaEnJuego">
        <div class="small-12 columns">
            <button id="empezar-partida"  @click="empezarPartida">
                EMPEZAR JUEGO NUEVO</button>
        </div>
    </section>
    <section class="row controls" v-else>
        <div class="small-12 columns">
            <button id="atacar" @click="atacar">ATACAR</button>
            <button id="ataque-especial" @click="ataqueEspecial">ATAQUE ESPECIAL</button>
            <button id="curar" @click="curar">CURAR</button>
            <button id="rendirse" @click="terminarPartida">RENDIRSE</button>
        </div>
    </section>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-botones',
    //props: ['atacar','ataqueEspecial','curar','terminarPartida','hayUnaPartidaEnJuego','empezarPartida'],
    props: {
      hayUnaPartidaEnJuego: Boolean,
      empezarPartida: Function,
      atacar: Function,
      ataqueEspecial: Function,
      curar: Function,
      terminarPartida: Function,
    },
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-botones {

  }

  button {
      font-size: 20px;
      background-color: #eee;
      padding: 12px;
      box-shadow: 0 1px 1px black;
      margin: 10px;
  }

  #empezar-partida {
      background-color: #aaffb0;
  }

  #empezar-partida:hover {
      background-color: #76ff7e;
  }

  #atacar {
      background-color: #ff7367;
  }

  #atacar:hover {
      background-color: #ff3f43;
  }

  #ataque-especial {
      background-color: #ffaf4f;
  }

  #ataque-especial:hover {
      background-color: #ff9a2b;
  }

  #curar {
      background-color: #aaffb0;
  }

  #curar:hover {
      background-color: #76ff7e;
  }

  #rendirse {
      background-color: #ffffff;
  }

  #rendirse:hover {
      background-color: #c7c7c7;
  }


</style>
