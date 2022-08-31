<template>
    <header>
      <nav class="nav">
        <div>
          <RouterLink to="/">
          <img :src="logo" :alt="alt" class="img">
        </RouterLink>
        </div>
        <div>
          <RouterLink class="nav-link" to="/">Home</RouterLink>
          <RouterLink class="nav-link" to="/pedidos">Pedidos</RouterLink>
        </div>
      </nav>
  </header>
</template>

<script>
export default {
    name: "Navbar",
    props:["logo", "alt"]
}
</script>

<style scoped>
  .nav{
    display: flex;
    height: 10vh;
    width: 100%;
    justify-content: space-between;
    align-items: center;
    background-color: rgb(26, 26, 26);
  }
  .img{
    width: 40px;
    margin-left: 50px;
  }

  .nav-link{
    margin-right: 50px;
    color: rgb(226, 210, 65);
    font-size: 15px;

  }

</style>