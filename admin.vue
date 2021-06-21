<template>
<div>
    <form @submit.prevent="submeterFormulario" action="form" style="padding:10px">

    <div class="input-control">
      <label>Imagem</label>
      <input type="text" v-model="novoProduto.imagem">
    </div>

    <div class="input-control">
      <label>Nome</label>
      <input type="text" v-model="novoProduto.nome">
    </div>

    <div class="input-control">
      <label>Status</label>
      <input type="text" v-model="novoProduto.status">
    </div>

    <div class="input-control">
      <label>Espécie</label>
      <input type="text" v-model="novoProduto.especie">
    </div>
    
    <div class="input-control">
      <label>Género</label>
      <input type="text" v-model="novoProduto.genero">
    </div>
    

  <br>
  <button type="submit" class="button" >
    Enviar
  </button>
  </form>

  <div v-if="mostraAviso">
    Insere os dados.
  </div>

  <div v-for="(item,id) in info" :key="id">
      {{item.nomegenero}} 
      <img width="20%" :src="item.imagem">
  </div>


</div>
</template>
<script>
import axios from 'axios';
export default {
  data () {
    return {
      novoProduto:{
        imagem:'',
        nome:'',
        status:'',
        especie:'',
        genero:'',
      },
      mostraAviso: false,
      info: []
    }
  },
   mounted() {
    axios
     .get("https://rickandmortyapi.com/api/location/")
     .then(response => (this.info = response.data.generos));
  },
  methods:{
    submeterFormulario() {
      
      if(this.novoProduto.imagem != '' && this.novoProduto.nome != '' && this.novoProduto.status != '' && this.novoProduto.especie != '' && this.novoProduto.genero != ''){
        this.mostraAviso= false;
        return axios.post('https://rickandmortyapi.com/api/location/', this.novoProduto);
      } 
      else {
        alert("Campos Vazios");
        this.mostraAviso= true;    
        }
  },

  
}
}
</script>
<style scoped>
.form{
  max-width: 550px;
  box-sizing: border-box;
  margin: 30px;
  margin-top: 60px;
  padding: 30px;
  text-align: justify;
  box-shadow: 0 0 24px rgba(0, 0, 0, 0.3);
  width: 100%;
}

.button{
  font: inherit;
  cursor: pointer;
  border-radius: 4px;
  border: 1px solid #FFA500;
  background-color: white;
  color: #FFA500;
  text-decoration: none;
  padding: 10px 30px;
}
.button:hover,
.button:active {
  color: #fff;
  background-color: #FFA500;
}

.input-control {
  margin: 10px 0;
}
.input-control label {
  display: block;
  font-weight: bold;
  color: #FFA500;
}
.input-control input{
  display: block;
  width: 100%;
  box-sizing: border-box;
  font: inherit;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 5px; 
}
.input-control input:focus{
  background-color: #eee;
  outline: none;
}
</style>
