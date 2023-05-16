
<template>

  <div id="burger-table">

    <div>

      <div id="burger-table-heading">

        <div id="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      
      </div>

    </div>

    <div id="burger-table-rows">

      <div class="burger-table-row">

        <div class="order-number">1</div>
        <div>Nome</div>
        <div>Pão</div>
        <div>Carne</div>
        <div>
          <ul>
            <li>Salame</li>
            <li>Tomate</li>
          </ul>
        </div>
        <div>
          <select name="status" class="status">

            <option>Selecione</option>

          </select>
          <button class="btn-delete">Cancelar pedido</button>
        </div>

      </div>

    </div>

  </div>

</template>

<script>

export default {
  name: "DashBoard"
}

</script>

<style scoped>

#burger-table {
  max-width: 100%;
  margin:0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row{
 display: flex;
}

#burger-table-heading{
  font-weight: bold;
  padding:12px;
  border-bottom: 3px solid #333;
}

#burger-table-heading div,
.burger-table-row div {
  flex:1;
}

.burger-table-row {
  width:100%;
  padding:12px;
  border-bottom: 1px solid #ccc;
}

select {
  padding:12px 6px;
  margin-right:12px;
}

.btn-delete {
  background-color: #222;
  color: #fcba03;
  font-weight: bold;
  border: 2px solid #222;
  padding:10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: .5s;
}

.btn-delete:hover {
  background: transparent;
  color: #222;
}


</style>