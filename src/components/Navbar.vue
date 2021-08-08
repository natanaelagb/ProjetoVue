<template>
  <div id="nav">
    <div class="center">  
      <router-link to="/" id="logo-url">
        <img :src="logo" :alt="alt" />
      </router-link>
      <button type="button" id="nav-btn" @click="showLinks">
        <i class="bi bi-list"></i>
      </button>
      <div id="nav-links">
        <router-link to="/">Home</router-link>
        <router-link to="/pedidos">Pedidos</router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo", "alt"],
  methods: {
    showLinks() {
      const btn = document.getElementById("nav-btn");
      const links = document.getElementById("nav-links");

      if (!btn.classList.contains("active")) {
        links.style.maxHeight = "150px";
        btn.classList.toggle("active");
      } else {
        links.style.maxHeight = "";
        btn.classList.toggle("active");
      }
    },
  },
};
</script>

<style scoped>
#nav {
  position: fixed;
  display: flex;
  width: 100%;
  background-color: #222;
  border-bottom: 1px solid #111;
  justify-content: space-between;
  flex-wrap: wrap;
  box-shadow: 0 .5rem 1rem rgba(0,0,0,.15);
}

#logo-url {
  display: flex;
}

#logo-url img {
  margin: auto 0;
  width: 40px;
}

#nav-btn {
  background-color: transparent;
  color: #fcba03;
  border: 0;
  cursor: pointer;
  font-size: 35px;
  display: none;
  padding: 9px 0;
  margin-left: auto;
}

#nav-links {
  display: flex;
}

#nav-links a {
  text-decoration: none;
  color: #fcba03;
  padding: 20px 10px;
}

#nav-links a:hover {
  background-color: #6d6d6d;
}


@media screen and (max-width: 400px) {
  #nav-btn {
    display: block;
  }

  #nav-links {
    flex-basis: 100%;
    flex-direction: column;
    max-height: 0;
    overflow: hidden;
    transition: max-height 1s;
    margin: 0;
  }

  #nav-links a {
    text-align: center;
  }
}
</style>