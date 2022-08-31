<template>
<div>
  <Navbar :logo="logo" :alt="alt"/>
  <div class="main-container">
    <RouterView />
  </div>
  <Footer />
</div>
</template>

<script>
  import Navbar from "./components/Navbar.vue"
  import Footer from "./components/Footer.vue"
  export default {
    name: "App",
    components: {
      Navbar,
      Footer
    },
    data(){
      return {
        logo: "../public/img/logo.png",
        alt: "Make your burguer"
      }    
    }
  }
</script>

<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    text-decoration: none;
    list-style: none;
  }
  .main-container{
    height: 90vh;
  }
</style>
