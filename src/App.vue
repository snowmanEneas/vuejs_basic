<template>
  <div id="app">
    <h3>Cadastro: </h3>
    <small id="nomeErro" v-show="deuErro">O nome é inválido!</small><br>
    <input type="text" placeholder="nome" v-model="nomeField"><br>
    <input type="email" placeholder="email" v-model="emailField"><br>
    <input type="number" placeholder="idade" v-model="idadeField"><br>
    <button @click="cadastrarUsuario">Cadastrar</button>
    <div v-for="(cliente,index) in orderClientes" :key="cliente.id">
      <h5>{{index + 1}}</h5>
      <Cliente :cliente="cliente" @meDelete="deletarUsuario($event)"/>
    </div>
  </div>
</template>

<script>
import _ from 'lodash';
import Cliente from './components/Cliente';
export default {
  name: 'App',
  data(){
    return {
      deuErro: false,
      nomeField: "",
      emailField: "",
      idadeField: 0,
      clientes: [
        {
          id: "7",
          nome: "Jacare",
          email: "lacoste@gmail.com",
          idade: "900"
        },
        {
          id: "2",
          nome: "Ursula",
          email: "bruxona@gmail.com",
          idade: "15"
        }
      ]
    }
  },
  components: {
    Cliente
  },
  methods: {
    cadastrarUsuario: function(){
      if(this.nomeField === "" || this.nomeField === " " || this.nomeField.length < 2){
        this.deuErro = true;
      }else{
        this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now()})
        this.nomeField = "";
        this.emailField = "";
        this.idadeField = 0;
        this.deuErro = false;
      }
    },
    deletarUsuario: function($event){
      console.log("Recebendo evento!");
      var id = $event.idDoCliente;
      var novoArray = this.clientes.filter(cliente => cliente.id != id);
      this.clientes = novoArray;
    }     
  },
  computed: {
    orderClientes: function(){
      return _.orderBy(this.clientes, ['nome'],['asc']);
    }
  }
}
</script>
<style scoped>
  #nomeErro{
    color: red;
  }
</style>>
  


