<template>
  <section class="src-components-barra">
        <h1 class="text-center"><i :class="['fas', icono, 'fa-2x']"></i></h1>
        <div class="curarthbar">
            <div class="curarthbar text-center" 
            :style="{'background-color': color, 'margin': 0, 'color': 'white', width: getSalud(salud)}" >
                {{ getSalud(salud) }}
            </div>
        </div>
    </section>
</template>

<script lang="js">

  export default  {
    name: 'src-components-barra',
    //props: ['salud','icono','color'],
    props: {
      salud: Number,
      icono: String,
      color: String
    },
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {
      getSalud(salud) {
          return `${salud}%`
      },
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-components-barra {

  }

  .text-center {
      text-align: center;
  }

  .curarthbar {
      width: 80%;
      height: 40px;
      background-color: #eee;
      margin: auto;
      transition: width 500ms;
      font-size: 22px;
  }

</style>
