<template>
  <div>
    <Banner />
    <FormBurguer />
  </div>
</template>

<script>
import Banner from "../components/Banner.vue"
import FormBurguer from "../components/FormBurguer.vue"
export default {
  name:"Home",
  components: {
    Banner,
    FormBurguer
  }
}
</script>



