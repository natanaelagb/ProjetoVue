<template>
  <Navbar :logo="logo_src" :alt="app_name" />
  <main>
   <router-view />
  </main>
  <Footer />
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Footer from "./components/Footer.vue";
export default {
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Make Your Burguer",
    };
  },
  components: {
    Navbar,
    Footer,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  font-family: Helvetica;
  box-sizing: border-box;
}

body {
  position: relative;
  min-height: 100vh;
  padding-bottom: 58px;
}

main {
  padding-top: 58px;
}
.center {
  display: inherit; 
  flex-direction: inherit;
  flex-wrap: inherit;
  justify-content: inherit;
  width: 100%;
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 15px;
}
</style>
