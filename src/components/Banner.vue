
<template>
  
  <div id="main-banner">
    <h1>Make Your burger</h1>
  </div>

</template>

<script>

export default {

  name: "Banner"
}

</script>

<style scoped>

#main-banner {

  background-image: url("/public/img/burger.jpg");
  background-repeat: no-repeat;
  background-position: 0%;
  background-size: cover;
  width: 100%;
  height:500px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

#main-banner h1{

  color: #fff;
  text-align: center;
  font-size: 60px;
  background-color: #222;
  padding:20px 40px;
}

</style>
