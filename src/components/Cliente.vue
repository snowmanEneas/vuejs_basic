<template>
    <div :class="{'cliente': !isPremium,'cliente-premium': isPremium}">
        <h3 id="cliente-nome">Nome: {{cliente.nome}} </h3>
        <hr>
        <p>Email: {{cliente.email | processarEmail}} </p>
        <p v-if="showIdade === true ">Idade: {{cliente.idade}} </p>
        <p v-else>O usuário escondeu a idade!!</p>
        <button @click="mudarCor($event)">Mudar cor!</button>
        <button @click="emitirEventoDelete">Deletar</button>
        <h4>Id Especial: {{idEspecial}}</h4>
    </div>
</template>

<script>
export default {
    data(){
        return{
            isPremium: false
        }
    },
        props: {
            cliente: Object,
            showIdade: Boolean
    },
        methods: {
            mudarCor: function($event){
                console.log($event);
                this.isPremium = !this.isPremium;
        },
            emitirEventoDelete: function(){
                console.log("Emitindo do filho!");
                this.$emit("meDelete",{idDoCliente: this.cliente.id, component: this});
        },
            testar: function(){
                console.log("Testando!");
                alert("Isso é um alert!");
        }
    },
        filters: {
            processarEmail: function(value){
                return value.toUpperCase();
        }
    },
        computed: {
            idEspecial: function(){
                return (this.cliente.email + this.cliente.nome + this.cliente.id).toUpperCase();
        }
    }
}
</script>

<style scoped>
    .cliente{
        color: black;
        background-color:#E6E6FA;
        max-width: 2000px;
        height: 200px;
        padding: 2%;
        margin-top: 2%;
    }
    .cliente-premium{
        color: gold;
        background-color:black;
        max-width: 2000px;
        height: 200px;
        padding: 2%;
        margin-top: 2%;
    }


</style>