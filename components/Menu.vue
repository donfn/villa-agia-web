<template>
  <div>
    <div class="sticky right-0 left-0 md:right-5 md:left-6 top sticky-menu flex rounded-bottom bg-white shadow-lg flex flex-col justify-center items-center">
      <div class="flex items-center justify-center w-full mr-10">
        <div class="md:flex nav items-center justify-between">
          <div v-for="menuItem of menuLeft" :key="menuItem" class="item px-4">
            <a class="link text-black text-sm font-regular" :href="menuItem.href">{{menuItem.title}}</a>
          </div>
        </div>

        <Icon color="black" class="-mt-5 -mb-5"/>

        <div class="flex nav items-center justify-between">
          <div v-for="menuItem of menuRight" :key="menuItem" class="item px-4">
            <a class="link text-black text-sm font-regular" :href="menuItem.href">{{menuItem.title}}</a>
          </div>
        </div>

      </div>
      <button class="-mb-5 mr-10 bg-brand px-5 hover:tracking-wider transition-all duration-200 p-2 text-white shadow-lg rounded text-sm tracking-widest" style="z-index:99999999">
        REQUEST BOOKING <BIcon icon="arrow-right"></BIcon>
      </button>
    </div>
    <div class="absolute top-0 menu flex items-center justify-center w-full">
      <div class="md:flex nav items-center justify-between">
        <div v-for="menuItem of menuLeft" :key="menuItem" class="item px-4">
          <a class="link text-white text-sm font-regular" :href="menuItem.href">{{menuItem.title}}</a>
        </div>
      </div>

      <Logo color="black" class="bg-white -mt-10 -mb-10 rounded"/>

      <div class="flex nav items-center justify-between">
        <div v-for="menuItem of menuRight" :key="menuItem" class="item px-4">
          <a class="link text-white text-sm font-regular" :href="menuItem.href">{{menuItem.title}}</a>
        </div>
      </div>
    </div>
  </div>

</template>
<script>
export default {
  props:["menu"],
  computed:{
      menuLeft(){
        let length = Math.ceil(this.menu.length/2)
        return this.menu.slice(0,length)
      },
    menuRight(){
      let length = Math.ceil(this.menu.length/2)
      return this.menu.slice(length,2*length)
    }
  }
}
</script>
<style lang="scss">
.menu{
  z-index: 9999999;
  .nav{
    font-family: Montserrat;
    letter-spacing: 2px;
    font-weight: 600;
    a{
      text-decoration: none;
    }
  }
}

.sticky-menu{
  z-index: 5;
  position: fixed;
  .nav{
    font-family: Montserrat;
    letter-spacing: 2px;
    font-weight: 600;
    a{
      text-decoration: none;
    }
  }
}
.bg-brand{
  background-color: #5f5c39;
}
</style>
