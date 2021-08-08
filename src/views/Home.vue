<template>
  <Banner />
  <div class="main-container">
    <h1>Monte seu Burger:</h1>
    <BurgerForm />

  </div>
</template>

<script>
import Banner from "../components/Banner.vue"
import BurgerForm from "../components/BurgerForm.vue"
export default {
  name: 'Home',
  components: {
    Banner,
    BurgerForm
  }
}
</script>

<style scoped>
  .main-container{
    padding: 30px 20px 40px 20px;
    display: flex;
    flex-direction: column;
  }

  h1{
    text-align: center;
    margin-bottom: 15px;
  }

</style>
