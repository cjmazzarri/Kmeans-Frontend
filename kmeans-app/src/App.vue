<template>
  <div class="container">
    <img src="./assets/UPC_logo_transparente.png" style="width: 5%">
    <p>Programación Concurrente y Distribuida - TA2<br>Dataset: Bonos y pensiones complementarias administradas por la ONP Agosto 2020</p>

    <div class="data">
      <table style="width: 100%; border: 2px solid black">
        <tr>
          <th>Cluster</th> <th>Id_Persona</th> <th>Prestacion</th><th>Tipotra</th><th>Tipoben</th><th>Beneficio</th>          
        </tr>
        <tr v-for="(dato, index) in datos" v-bind:key="index">  
          <td>{{dato.Cluster}} </td>            
          <td>{{dato.Id_persona}}</td>
          <td>{{dato.Prestacion}}</td>
          <td>{{dato.Tipotra}}</td>
          <td>{{dato.Tipoben}}</td>
          <td>{{dato.Beneficio}}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  data: () => {
    return {
      datos: [],
      errors: '',
      indices: []
    }
  },
  mounted() {
    axios.get("http://localhost:9000/").then(response =>{
      console.log(JSON.stringify(response.data))
      this.datos = response.data
      console.log(this.datos)  
    }).catch(error =>{
      console.log(error)
      this.errors = error
    })

    axios.get("http://localhost:9000/grupos").then(response =>{
      console.log(JSON.stringify(response.data))
      this.indices = response.data
      console.log(this.indices)
    }).catch(error =>{
      console.log(error)
      this.errors = error
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
