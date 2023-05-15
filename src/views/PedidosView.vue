<template>
  <div class="main-container">
    <h1>Gerenciar Pedidos</h1>
    <!--Dashboard with all request of the user-->
    <DashBoard/>
  </div>
</template>

<script>

import DashBoard from "../components/DashBoard.vue"

export default {

  name: "PedidosView",

  components: {
    DashBoard
  }

}


</script>

