
<template>
  <div>

    <!--message-->
    <Message :msg="msg" v-show="msg"/>

    <!--container of the form-->
    <div>

      <form id="burger-form" @submit="createBurger">

        <!--container of the input-->
        <div class="input-container">

          <label for="name">Nome do Cliente:</label>
          <input type="text" name="name" id="name" placeholder="Digite seu Nome" v-model="name" />

        </div>

        <!--container of the input-->
        <div class="input-container">

          <label for="bread-type">Escolha o Pão:</label>
          <select name="bread-type" id="bread-type" v-model="breadType">

            <option value="">Selecione o seu pão</option>
            <option v-for="bread in breadsType" 
              :key="bread.id" 
              :value="bread.tipo">
              {{ bread.tipo }}
            </option>

          </select>

        </div>

        <!--container of the input-->
        <div class="input-container">

          <label for="meat-type">Escolha a Carne do Seu Burger:</label>
          <select name="meat-type" id="meat-type" v-model="meatType">

            <option value="">Selecione o tipo de carne</option>
            <option v-for="meat in meatsType" 
              :key="meat.id" 
              :value="meat.tipo">
              {{ meat.tipo }}
            </option>

          </select>

        </div>

        <!--container of the input-->
        <div class="input-container" id="optionals-container">

          <label id="optionals-title" for="optionals">Selecione os opcionais:</label>

          <div class="flexbox-container" 
          v-for="optional in optionalsData" 
          :key="optional.id">

            <input type="checkbox"
            name="optionals"
            v-model="optionals"
            :value="optional.tipo" />

            <span>{{ optional.tipo }}</span>

          </div>

        </div>

        <!--container of the input-->
        <div class="input-container">

          <input type="submit" class="btn-submit" value="Criar Meu Burger" />

        </div>

      </form>

    </div>

  </div>
</template>

<script>

import Message from "./Message.vue"

export default {

  name: "BurgerForm",

  components: {
    Message
  },

  data() {

    return {

      breadsType:null,
      meatsType: null,
      optionalsData: null,
      name: null,
      breadType: null,
      meatType: null,
      optionals: [],
      msg: null
    }
  },

  methods: {

    async getMakings(){

      const req = await fetch("http://localhost:3000/Ingredientes")
      const data = await req.json()

      //get datas
      this.breadsType = data.paes
      this.meatsType = data.carnes
      this.optionalsData = data.opcionais

    },

    async createBurger(e){

      e.preventDefault()

      const data = {
        nome: this.name,
        pao: this.breadType,
        carne: this.meatType,
        opcionais: Array.from(this.optionals),
        status: "Solicitado"
      }

      const dataJson = JSON.stringify(data)

      const req = await fetch("http://localhost:3000/burgers",{
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: dataJson
      })

      const res = await req.json()

      //put the message of the system
      this.msg = `Pedido N° ${res.id} realizado com sucesso!`

      //clear message
      setTimeout(()=> this.msg="", 3000)

      //clear inputs
      this.name = ""
      this.carne = ""
      this.breadType = ""
      this.optionals = ""

    }

  },

  mounted() {
    this.getMakings()
  }


}

</script>

<style scoped>
#burger-form {

  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {

  font-weight: bold;
  margin-bottom: 15px;
  color: #000;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}

input,
select {

  padding: 5px 10px;
  width: 300px;
}

#optionals-container {
  flex-direction: row;
  flex-wrap: wrap;
}

#optionals-title {
  width: 100%;
}

.flexbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}

.flexbox-container span,
.flexbox-container input {
  width: auto;
}

.flexbox-container span {
  margin-left: 6px;
  font-weight: bold;
}

.btn-submit {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: .5s;
}

.btn-submit:hover {
  background-color: transparent;
  color: #222;
}
</style>
