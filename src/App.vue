<template lang="pug">
  #app
    h1 {{titulo}}
    input(id='input1' type='text' v-model='nuevoItem' @keyup.enter='addItem')
    button(@click='addItem') Agregar item
    ul
      li(v-for="(item, key) in items" v-bind:key="key")
        button(@click='item.cantidad++') +
        button(@click='item.cantidad--') -
        input(type='text' v-model.number='item.cantidad')
        span {{ item.nombre }}
        span(v-if='item.cantidad < 1') - Sin stock

    h3 Total : {{sumarItems}}

    div(class='container mt-5')
      p(:class="['p-3', 'text-white', fondo]")
        |Lorem Ipsum is simply dummy text of the printing and typesetting
        |industry. Lorem Ipsum has been the industry's standard dummy text
        |ever since the 1500s, when an unknown printer took a galley of type
      
      input(class='form-control my-3' v-model='fondo')

      p(class='text-white p-3' :class="{'bg-info': color, 'bg-success': !color}")
        |Lorem Ipsum is simply dummy text of the printing and typesetting
        |industry. Lorem Ipsum has been the industry's standard dummy text
        |ever since the 1500s, when an unknown printer took a galley of type
      button(class='btn btn-primary' @click='color = !color') cambiar fondo
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
      total: 0,
      fondo: 'bg-dark',
      color: false
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
  #input1 {
    margin-bottom: 10px;
  }
  li {
    margin-bottom: 5px;
  }
  li input {
    width: 25px;
    text-align: center;
    margin: 0 10px;
  }
</style>
