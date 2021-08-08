<template>
  <div>
    <p>{{msg}}</p>
  </div>
</template>

<script>
export default {
  name: "Message",
  props: {
    msg: String,
  },
}
</script>

<style scoped>
div {
  width: 100%;
  max-width: 400px;
  padding: 8px 0;
  margin:10px auto;
  background-color: #95eeff;
  text-align: center;
  border-radius: 5px;
}

p {
  font-weight: bold;
}
</style>