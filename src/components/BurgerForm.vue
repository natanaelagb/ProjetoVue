<template>
  <Message :msg="msg" v-show="msg"/>
  <form method="POST" id="form-burger" @submit="createBurger">
    <div class="input-container">
      <label for="client">Nome do cliente: </label>
      <input type="text" id="client" name="clinet" v-model="nome">
    </div>
    <div class="input-container">
      <label for="bread">Escolha o pão do seu Burger:</label>
      <select name="bread" id="bread" v-model="pao" >
        <option value="">Escolha o pão</option>
        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
      </select>
    </div>
    <div class="input-container">
      <label for="meat">Escolha a carne do seu Burger:</label>
      <select name="meat" id="meat" v-model="carne">
        <option value="">Escolha a carne</option>
        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
      </select>
    </div>
    <label>Ingredientes extras:</label>
    <div class="input-container" id="options-container">
      <div class="checkbox-container" v-for="opcoes in opcionaisdata" :key="opcoes.id">
        <input type="checkbox" id="salame" v-model="opcionais" :value="opcoes.tipo">
        <span>{{ opcoes.tipo }}</span>
      </div>
    </div>
    <div class="input-container">
      <button type="submit">Montar Meu Burger!</button>
    </div>

  </form>
</template>

<script>
import Message from './Message.vue'

export default {
  components: { 
    Message 
  },
  name: "BurgerForm",
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: null, 
      carne: null,
      opcionais: [],
      status: "Solicitado",
      msg: null
    }
  },
  methods:{
    
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes")
      const data = await req.json()

      this.paes = data.paes
      this.carnes = data.carnes
      this.opcionaisdata = data.opcionais
    },
    async createBurger(event) {
      event.preventDefault()
      
      const data = {
        nome: this.nome,
        pao: this.pao,
        carne: this.carne,
        opcionais: Array.from(this.opcionais),
        status: this.status
      }

      const dataJson = JSON.stringify(data)

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: dataJson
      })

      const res = await req.json()
      
      this.nome = "";
      this.pao = "";
      this.carne = "";
      this.opcionais = "";
      this.msg = `Pedido N° ${res.id} realizado com sucesso!`

      setTimeout(() => {
        this.msg = ""
      }, 2000);
    }
  },
  mounted() {
    this.getIngredientes()
  }
}
</script>

<style scoped>
  #form-burger{
    width: 100%;
    max-width: 400px;
    margin: 0 auto;
  }

  .input-container{
    margin: 20px 0;
    display: flex;
    flex-direction: column;
  }

  label{
    color: black;
    font-weight: bold;
    border-left: 4px solid #fcba03;
    padding: 5px;
    margin-bottom: 10px;
  }

  input[type="text"], select{
    padding: 3px 10px;
    font-size: 16px;
  }

  input[type="text"]{
    cursor: text;
  }

  select{
    cursor: pointer;
  }

  #options-container{
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
  }

  .checkbox-container{
    align-items: baseline;
    margin-bottom: 10px;
    font-weight: bold;
    flex-basis: 50%;
  }

  input[type="checkbox"] {
    cursor: pointer;
    margin-right: 5px;
  }

  button{
    margin: 0 auto;
    width: 60%;
    background-color: #222;
    padding: 7px 0;
    border: 2px solid #222;
    border-radius: 5px;
    color: #fcba03;
    cursor: pointer;
    font-weight: bold;
    font-size: 15px;
  }

  button:hover{
    background-color: transparent;

  }
</style>