<template>
  <div>
    <Menu :menu="menu"/>
    <Nuxt />
  </div>
</template>

<style lang="scss">
//@font-face {
//  font-family: "Averta";
//  src: url("~assets/averta.woff")  format('woff');
//}
//@import url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,200&display=swap');
$primary-font: "Vollkorn";
$secondary-font: "Open Sans";

h1,h2,h3,h4,h5,h6{
  font-family: $primary-font;
}

html, a{
    font-family: $secondary-font;
}

a{
  text-decoration: none;
}
</style>

<script>
export default {
  data(){
    return{
      menu: [
          {
              title: "FACILITIES",
              href: "#contact"
          },
        {
          title: "AREA",
          href: "#contact"
        },
        {
          title: "PHOTOS",
          href: "#contact"
        },
        {
          title: "CONTACT",
          href: "#contact"
        }
      ]
    }

  }
}
</script>
