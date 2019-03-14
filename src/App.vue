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

    div(class='container computadas')
      h4
        b Mensaje:&nbsp;&nbsp;
        span {{mensaje}}
      h4
        b Invertido:&nbsp;&nbsp;
        span {{invertido}}
      input(class='form-control' type='text' v-model='mensaje')
      hr
      button(class='btn btn-danger' @click='contador === 0 ? contador=0 : contador--') -
      button(class='btn btn-primary' @click='contador === 100 ? contador=100 : contador++') +
      h4 {{contador}} %

      .progress
        .progress-bar(role='progressbar', :style="{'width': contador+'%'}",
        aria-valuemin='0', aria-valuemax='100', :class="colorBar") {{contador}} %

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
      color: false,
      mensaje: 'Mi primer app Vue',
      contador: 0
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
    },
    invertido () {
      return this.mensaje.split('').reverse().join('')
    },
    colorBar () {
      return {
        'bg-success': this.contador < 26,
        'bg-info': this.contador > 25  && this.contador < 51,
        'bg-warning': this.contador > 50 && this.contador < 76,
        'bg-danger': this.contador > 75
      }
    }
  }
}
</script>

<style lang="scss" scoped>
  #app {
    padding: 20px; 
  }
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
  .computadas {
    margin-top: 50px;
  }
</style>
