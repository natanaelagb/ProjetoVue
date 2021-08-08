<template>
  <div id="main-banner">
    <div class="center">
      <h1>Make Your Burguer </h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "Banner"
}
</script>

<style scoped>
  #main-banner{
    display: flex;
    background-image: url("/img/burger.jpg");
    background-position: center;
    background-size: cover;
    height: 500px;
    align-items: center;
  }

  h1{
    color: #fcba03;
    margin-left: 10px;
  }
</style>