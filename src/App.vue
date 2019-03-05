<template lang="pug">
  #app
    h1 {{titulo}}
    p(v-for="(nombre, key) in nombres" v-bind:key="key") {{nombre}}
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      titulo: 'Hola Selene',
      nombres: ['Tito', 'Pepe', 'Lilu']
    }
  }
}
</script>

<style lang="scss">

</style>
