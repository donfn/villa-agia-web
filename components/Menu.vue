<template>
    <div class="grid grid-cols-3 pt-4 menu">
        <Logo/>
        <div class="flex nav items-center justify-end">
            <div v-for="menuItem in menu" :key="menuItem" class="item">
                <a class="link text-black text-lg font-regular" :href="menuItem.href">{{menuItem.title}}</a>
            </div>
        </div>
        <div class="flex items-center justify-end action pr-4 md:pr-80">
            <button class="bg-white hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded inline-flex items-center">
              <span>Action</span>
            </button>
        </div>
    </div>
</template>
<script>
export default {
    props:["menu"]
}
</script>
<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display&display=swap');
</style>
