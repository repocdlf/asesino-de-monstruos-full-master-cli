<template>

  <section class="src-components-logs">
    <section class="row log" v-if="turnos.length > 0">
        <div class="small-12 columns">
            <ul>
                <li v-for="(turno,index) in turnos"
                :key="index"
                :class="cssEvento(turno)"
                :style="{'text-align': turno.esJugador?'left':'right','opacity':index <=1?1:0.4}">
                    {{ turno.text }} 
                </li>
            </ul>
        </div>
    </section>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-components-logs',
    //props: ['turnos'],
    props: {
      turnos: Array
    },
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {
      cssEvento(turno) {
          //Este return de un objeto es prque vue asi lo requiere, pero ponerlo acá queda mucho mas entendible en el codigo HTML.
          return {
              'player-turno': turno.esJugador,
              'monster-turno': !turno.esJugador
          }
      }
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-logs {

  }

  .log {
      margin-top: 30px;
      text-align: center;
      padding: 10px;
      border: 1px solid #ccc;
      box-shadow: 0px 3px 6px #ccc;
  }

  .turno {
      margin-top: 20px;
      margin-bottom: 20px;
      font-weight: bold;
      font-size: 22px;
  }

  .log ul {
      list-style: none;
      font-weight: bold;
      text-transform: uppercase;
  }

  .log ul li {
      margin: 5px;
      text-align: right;
      padding:5px;
  }

  .log ul .player-turno {
      color: #eee;
      background-color: goldenrod;
  }

  .log ul .monster-turno {
      color: #eee;
      background-color:rgb(3, 110, 12);
  }

</style>
