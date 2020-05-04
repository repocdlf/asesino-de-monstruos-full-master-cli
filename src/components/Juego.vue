<template>
  <section class="src-components-juego">

    <div class="row controls ">
        <div class="small-10 columns">
            <h1><i>{{msg}}</i></h1>
        </div>
        <div class="small-2 columns">
            <img src="../assets/imgs/mounstro.png" width="75" alt="">
        </div>
    </div>
    
    <section class="row">
        <div class="small-6 columns">
            <Barra :salud="saludJugador" icono="fa-angry" color="goldenrod" />
        </div>
        <div class="small-6 columns">
            <Barra :salud="saludMonstruo" icono="fa-pastafarianism" color="rgb(3, 110, 12)"/>
        </div>
    </section>

    <Botones 
        :hayUnaPartidaEnJuego="hayUnaPartidaEnJuego"
        :empezarPartida="empezarPartida"
        :atacar="atacar"
        :ataqueEspecial="ataqueEspecial"
        :curar="curar"
        :terminarPartida="terminarPartida" />

    <Logs :turnos="turnos" />

  </section>
</template>

<script>

import Barra from './Barra.vue'
import Botones from './Botones.vue'
import Logs from './Logs.vue'

export default {
  name: 'Juego',
  components: {
      Barra,
      Botones,
      Logs
  },
  props: {
      msg: String
  },
  data() {
    return {
        saludJugador: 100,
        saludMonstruo: 100,
        hayUnaPartidaEnJuego: false,
        turnos: [],
        esJugador: false,
        rangoAtaque: [3, 10],
        rangoAtaqueEspecial: [10, 20],
        rangoAtaqueDelMonstruo: [5, 12],
    }    
  }, 
  methods: {
      empezarPartida: function () {
          this.hayUnaPartidaEnJuego = true;
          this.saludJugador = 100;
          this.saludMonstruo = 100;
          this.turnos = [];
      },
      atacar: function () {
          var heridas = this.calcularHeridas(this.rangoAtaque);
          this.saludMonstruo -= heridas;
          this.turnos.unshift({
              esJugador: true,
              text: 'Golpeaste al monstruo en ' + heridas + '%'
          });
          if (this.verificarGanador()) {
              return;
          }
          this.ataqueDelMonstruo();
      },

      ataqueEspecial: function () {
          var heridas = this.calcularHeridas(this.rangoAtaqueEspecial);
          this.saludMonstruo -= heridas;
          let evento = {
              esJugador: true,
              text: 'Golpeaste duro al monstruo por ' + heridas + '%'
          }
          this.registrarEvento(evento)
          if (this.verificarGanador()) {
              return;
          }
          this.ataqueDelMonstruo();

      },

      curar: function () {
          const PORCENTAJE_CURACION = 10;
          let saludDelJugadorAntesDelAtaque = this.saludJugador
          //Esto lo hacemos para primero descontar el ataque inevitable del monstruo y despues curarnos.
          this.ataqueDelMonstruo();

          if (saludDelJugadorAntesDelAtaque <= 90) {
              this.saludJugador += PORCENTAJE_CURACION;
              let evento = {
                  esJugador: true,
                  text: 'Te curaste en un ' + PORCENTAJE_CURACION + '%',
              }
  
              this.registrarEvento(evento)
          }
          
      },

      registrarEvento(evento) {
          this.turnos.unshift(evento);
      },
      terminarPartida: function () {
          this.hayUnaPartidaEnJuego = false;
      },

      ataqueDelMonstruo: function () {
          let heridas = this.calcularHeridas(this.rangoAtaqueDelMonstruo);
          this.saludJugador -= heridas;
          let evento = {
              esJugador: false,
              text: 'El monstruo golpea por  ' + heridas + '%'
          }

          this.registrarEvento(evento)
          this.verificarGanador();
      },

      calcularHeridas: function (rango) {
          let min = rango[0]
          let max = rango[1]
          return Math.max(Math.floor(Math.random() * max) + 1, min);

      },
      verificarGanador: function () {
          if (this.saludMonstruo <= 0) {
              if (confirm('Ganaste! Jugar de nuevo?')) {
                  this.empezarPartida();
              } else {
                  this.saludMonstruo = 0;
                  this.hayUnaPartidaEnJuego = false;
              }
              return true;
          } else if (this.saludJugador <= 0) {
              if (confirm('Perdiste! Jugar de nuevo?')) {
                  this.empezarPartida();
              } else {
                  this.saludJugador = 0;
                  this.terminarPartida()
              }
              return true;
          }
          return false;
      }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.src-components-juego {

}

h1 {
  color: blueviolet;
  text-shadow: 2px 2px 2px rgba(0, 0, 0, 0.5);
}

img {
    border-radius: 10px;
    box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.5);
}

</style>
