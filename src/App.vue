<template lang="pug">
  #app
    h1 {{titulo}}
    input(type='text' v-model='nuevoItem' @keyup.enter='addItem')
    button(@click='addItem') Agregar item
    ul
      li(v-for="(item, key) in items" v-bind:key="key")
        button(@click='item.cantidad++') +
        button(@click='item.cantidad--') -
        input(type='text' v-model.number='item.cantidad')
        span {{ item.nombre }}
        span(v-if='item.cantidad === 0') - Sin stock

    h3 Total : {{sumarItems}}
        
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      titulo: 'Lista de mercado',
      items: [
        {cantidad: 2, nombre: 'Tomate'},
        {cantidad: 5, nombre: 'Pimienta'},
        {cantidad: 0, nombre: 'Lulo'}
      ],
      nuevoItem: '',
      total: 0
    }
  },
  methods: {
    addItem () {
      this.items.push({cantidad: 1, nombre: this.nuevoItem})
      this.nuevoItem = ''
    }
  },
  computed: {
    sumarItems () {
      this.total = 0
      this.items.forEach(item => {
        this.total = this.total + item.cantidad
      })
      return this.total
    }
  }
}
</script>

<style lang="scss">
  li {
    margin-bottom: 5px;
  }
  li input {
    width: 25px;
    text-align: center;
    margin: 0 10px;
  }
</style>
