<template>
  <q-page>
    <h1>hola quasar</h1>
    <input type="text" v-model="nombre"> <br>
    {{nombre}} <br>
    <input type="number" v-model="num1"> <br>
    <input type="number" v-model="num2"> <br>
    {{parseInt(num1)+parseInt(num2)}}
    <button @click="precionar">Precioname!!!!!</button>
    <hr>
    <q-input autofocus @keyup.enter.prevent="aumentar" v-model="numero" type="number" label="Numero" />
    <br>
    {{numeros}}
    <hr>

    <table border="1" style="width: 100%">
      <tr>
        <th>#</th>
        <th>Nombre</th>
        <th>Estado</th>
        <th>Sueldo</th>
        <th>Fechanac</th>
      </tr>
      <tr v-for="docente in docentes" :key="docente.id">
        <td>{{docente.id}}</td>
        <td>{{docente.nombre}}</td>
        <td>{{docente.activo}}</td>
        <td>{{docente.sueldo}}</td>
        <td>{{docente.fechanac}}</td>
      </tr>
    </table>
    <pre>{{docentes}}</pre>
  </q-page>
</template>
<script>
export default {
  data(){
    return{
      nombre:'juan perez',
      num1:4,
      num2:5,
      numero:0,
      numeros:[],
      docentes:[]
    }
  },
  methods:{
    precionar(){
      // alert(parseInt(this.num1)+parseInt(this.num2))
      this.numeros=[]
    },
    aumentar(){
      this.numeros.push(this.numero)
      this.numero=""
    }
  },
  created() {
    // console.log('Se esta creato el formulario')
    this.$api.get("http://127.0.0.1:8000/api/docente").then(res=>{
      // console.log(res.data)
      this.docentes=res.data
    })
  },
  mounted() {
    // console.log('Se a montando el formulario')
  }
}
</script>
