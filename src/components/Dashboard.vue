<template>
  <div class="main-container">
    <div class="center">
      <h1>Gerenciar Pedidos:</h1>
      <Message :msg="msg" v-show="msg"/>
      <div class="wrapper">
        <table>
          <tr>
            <th>#</th>
            <th>Cliente</th>
            <th>Pão</th>
            <th>Carnes</th>
            <th>Opcionais</th>
            <th>Ações</th>
          </tr>
          <tr v-for="burger in burgers" v-bind:key="burger.id">
            <td>{{ burger.id }}</td>
            <td>{{ burger.nome }}</td>
            <td>{{ burger.pao }}</td>
            <td>{{ burger.carne }}</td>
            <td>
              <ul>
                <li
                  v-for="(opcao, index) in burger.opcionais"
                  v-bind:key="index"
                >
                  {{ opcao }}
                </li>
              </ul>
            </td>
            <td>
              <select @change="updateOrder($event, burger.id)">
                <option value="">Status</option>
                <option
                  v-for="status in status"
                  v-bind:key="status.id"
                  :value="status.tipo"
                  :selected="status.tipo == burger.status"
                >
                  {{ status.tipo }}
                </option>
              </select>
              <button @click="deleteOrder(burger.id)">Cancelar</button>
            </td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue';
export default {
  components: { Message },
  name: "Dashboard",
  data() {
    return {
      burgers: null,
      status: null,
      msg: ""
    };
  },
  methods: {
    async getBurgers() {
      const req = await fetch("http://localhost:3000/burgers");
      const res = await req.json();

      this.burgers = res;
    },

    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      const res = await req.json();

      this.status = res;
    },

    async deleteOrder(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE"
      })
      const res = await req.json()

      this.msg = `Pedido cancelado com sucesso!`
      setTimeout(() => {
        this.msg = ""
      }, 2000);

      this.getBurgers()
    },

    async updateOrder(event, id) {
      const data = { status: event.target.value }
      const dataJson = JSON.stringify(data)

      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: {"Content-Type": "application/json"},
        body: dataJson
      })
      const res = await req.json()

      this.msg = `O status do pedido N° ${res.id} foi atualizado para: ${res.status}`
      setTimeout(() => {
        this.msg = ""
      }, 2000);
      
    }
  },
  mounted() {
    this.getBurgers(), this.getStatus();
  },
};
</script>

<style scoped>

.main-container {
  display: flex;
  flex-direction: column;
  padding-top: 20px;
}

h1 {
  margin: 0 auto;
}

.wrapper{
  overflow: auto;

}

table {
  width: 100%;
  min-width: 780px;
  margin: 20px auto;
  border-collapse: collapse;
}

tr {
  width: 100%;
  display: flex;
  border-bottom: 1px solid rgb(179, 179, 179);
  align-items: center;
}

tr:nth-of-type(1) {
  border-bottom: 2px solid black;
}

tr:nth-of-type(2n) {
  background-color: #f1f0f0;
}

th,
td {
  flex-basis: 18%;
  padding: 10px 10px;
}

th:nth-of-type(1) {
  flex-basis: 10%;
}

td:nth-of-type(6n + 1) {
  font-weight: bold;
  flex-basis: 10%;
}

ul {
  list-style-position: inside;
}
li {
  margin-bottom: 3px;
  text-align: left;
}

select,
button {
  padding: 5px 5px;
  cursor: pointer;
}

select {
  margin: 0 5px 5px 0;
  color: #212529;
  border: 1px solid #ced4da;
  line-height: 1.5;
}

button {
  border: 2px solid #111;
  border-radius: 3px;
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
}

button:hover {
  background-color: transparent;
}
</style>