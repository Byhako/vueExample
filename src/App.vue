<template lang="pug">
  #app
    h1 {{titulo}}
    p(v-for="(nombre, key) in nombres" v-bind:key="key") {{nombre}}
    input(type='text' v-model='nuevoNombre')
    button(@click='addName') Agregar nombre
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      titulo: 'Hola Selene',
      nombres: ['Tito', 'Pepe', 'Lilu'],
      nuevoNombre: ''
    }
  },
  methods: {
    addName () {
      this.nombres.push(this.nuevoNombre)
    }
  }
}
</script>

<style lang="scss">

</style>
