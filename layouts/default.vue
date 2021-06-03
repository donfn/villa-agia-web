<template>
  <div class="bg-blue-100">
    <Menu :menu="menu"/>
    <Nuxt />
  </div>
</template>

<style>

</style>

<script>
export default {
  data(){
    return{
      menu: [
          {
              title: "Home",
              href: "#contact"
          }
      ]
    }

  }
}
</script>