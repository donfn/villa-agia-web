<template>
  <div class="">
    <div class="welcome w-full">
      <div class="hero w-full flex justify-center items-center py-10 p-3 md:p-10 absolute top-0 left-0 right-0">
      <span class="bg-hero"/>
        <div class="absolute top-0 md:bottom-0 -bottom-4 md:pb-4 w-full flex justify-center items-end px-0" style="">
          <div class="w-auto rounded-none  bg-white">
            <div class="w-auto py-10 px-24 flex flex-col md:flex-row items-center gap-3">
              <!--            <Icon color="black" class=" -ml-24"/>-->
              <span class="p-2 flex flex-col justify-between">
              <label class="pb-2">Day of Arrival</label>
              <BFormDatepicker v-model="customer.dateOfArrival" id="example-datepicker" class="w-full"></BFormDatepicker>
            </span>
              <span class="p-2 flex flex-col justify-between">
            <label class="pb-2">People</label>
              <BFormSpinbutton v-model="customer.people" min="1" max="100"></BFormSpinbutton>
            </span>
              <span class="p-2 flex flex-col">
              <label class="pb-2">Nights</label>
              <BFormSpinbutton v-model="customer.nights" min="1" max="100"></BFormSpinbutton>
            </span>
            </div>
            <button class="hover:tracking-wider transition-all duration-200 border border-black p-3 w-full text-black rounded-b-md md:rounded-none text-sm tracking-widest">
              REQUEST BOOKING <BIcon icon="arrow-right"></BIcon>
            </button>
          </div>
        </div>
    </div>


<!--      <div class="px-60 flex items-end justify-items-end pt-96">-->
<!--        <h1 class="text-5xl pt-28 w-1/2">A picturesque villa in Agia Village, Crete.</h1>-->
<!--      </div>-->
    </div>

    <div class="details w-full h-96 mt-20 px-4">
      <div class="px-10 flex justify-center flex-col items-center border border-1 py-10">
          <Icon color="black" class="-ml-10"/>
          <h1>Peace. Beauty. Tradition.</h1>
          <p class="text-center md:w-1/2 mt-10 tracking-wider">Et sunt esse esse dolores quo. Impedit aut repellat quia. Provident porro quia autem.<br>Dolorem cum quia totam totam. Et cum cum ut et accusantium sunt enim. Incidunt laborum harum accusantium. Velit quam optio quo harum eius fuga.<br>Rerum magni perspiciatis optio. Ut nisi aspernatur omnis nihil adipisci error nemo. Consequatur a sint aut hic.</p>
        <div class="features w-full h-96 mt-20 md:mt-10 p-3">
          <div class="px-10 flex justify-center gap-5 items-center">
        <span v-for="feature in info" class="flex flex-col items-center">
          <BIcon :icon="feature.icon" class="mb-4 text-3xl"></BIcon>
          <h3 class="tracking-wide font-thin text-center">{{feature.content}}</h3>
          <label class="uppercase text-xs text-center">{{feature.title}}</label>

        </span>
          </div>
        </div>
      </div>
    </div>

    <div v-swiper="{
      loop:true,
      slidesPerView: 4,
              breakpoints: {
          1024: {
          slidesPerView: 4,
          spaceBetween: 10
          },
          768: {
          slidesPerView: 2,
          spaceBetween: 0
          },
          640: {
          slidesPerView: 1,
          spaceBetween: 10
          },
          320: {
          slidesPerView: 1,
          spaceBetween: 10
          }
        }
      }" class="w-full ml-auto mt-48 relative overflow-x-hidden" :loadtheme="false">
      <div class="highlights swiper-wrapper flex testimonials p-5 cursor-move">
        <div class="swiper-slide lg:rounded p-10 w-screen md:w-1/4" v-for="highlight in highlights"
             :style="`background-image: url(${highlight.photo})`">
        <span>
          <h3
            class="p-0 h-96 w-96 flex justify-content-end items-end text-3xl text-wrap text-white tracking-wider">{{ highlight.title }}</h3>
        </span>
        </div>
      </div>
    </div>
    <div class="flex flex-col justify-center items-center">
      <h2 class="text-center pb-4">Features</h2>
      <p class="text-center w-96">Here are our villa's highlights. Click on each one to learn more or view more pictures.</p>
      <div class="grid grid-cols-2 md:grid-cols-3 gap-3 p-3">
        <div v-for="feature in features">
          <BIcon icon="check"></BIcon> {{feature}}
        </div>
      </div>
    </div>
    <GMap
      ref="gMap"
      language="en"
      :center="{lat: 35.3648132, lng: 24.7652742}"
      :zoom="10"
    >
      <GMapMarker
        :position="{lat: 35.3648132, lng: 24.7652742}"
        @click="currentLocation = location">
      </GMapMarker>
    </GMap>
    <span class="p-96"></span>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
import {BFormDatepicker, BFormSpinbutton, BInputGroup, BInputGroupPrepend, BInputGroupText, BootstrapVueIcons} from "bootstrap-vue";

Vue.use(BootstrapVueIcons)

export default Vue.extend({
  components:{
    BFormDatepicker,
    BFormSpinbutton,
    BInputGroup,
    BInputGroupPrepend,
    BInputGroupText,
  },
  data(){
    return{
      customer:{
        dateOfArrival: new Date(),
        people: 1,
        nights: 1
      },
      info:[
        {
          icon: "arrows-angle-expand",
          title: "Area",
          content: "50 sqm."
        },
        {
          icon: "people",
          title: "Perfect for",
          content: "7 people"
        },
        {
          icon: "geo",
          title: "Distance from THE city center",
          content: "50 km"
        },
        {
          icon: "house",
          title: "Neighborhood",
          content: "Traditional village"
        },

      ],
      highlights:[
        {
          title: "Accomodation",
          description: "Et sunt esse esse dolores quo. Impedit aut repellat quia. Provident porro quia autem.\n" +
            "Dolorem cum quia totam totam. Et cum cum ut et accusantium sunt enim. Incidunt laborum harum accusantium.",
          photo:"https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1051&q=80"
        },
        {
          title: "Kitchen",
          description: "Et sunt esse esse dolores quo. Impedit aut repellat quia. Provident porro quia autem.\n" +
            "Dolorem cum quia totam totam. Et cum cum ut et accusantium sunt enim. Incidunt laborum harum accusantium.",
          photo:"https://images.unsplash.com/photo-1484154218962-a197022b5858?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8a2l0Y2hlbnxlbnwwfHwwfHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
        },
        {
          title: "Pool",
          description: "Et sunt esse esse dolores quo. Impedit aut repellat quia. Provident porro quia autem.\n" +
            "Dolorem cum quia totam totam. Et cum cum ut et accusantium sunt enim. Incidunt laborum harum accusantium.",
          photo:"https://images.unsplash.com/photo-1591285713698-598d587de63e?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=675&q=80"
        },
        {
          title: "Accomodation",
          description: "Et sunt esse esse dolores quo. Impedit aut repellat quia. Provident porro quia autem.\n" +
            "Dolorem cum quia totam totam. Et cum cum ut et accusantium sunt enim. Incidunt laborum harum accusantium.",
          photo:"https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1051&q=80"
        },
        {
          title: "Kitchen",
          description: "Et sunt esse esse dolores quo. Impedit aut repellat quia. Provident porro quia autem.\n" +
            "Dolorem cum quia totam totam. Et cum cum ut et accusantium sunt enim. Incidunt laborum harum accusantium.",
          photo:"https://images.unsplash.com/photo-1484154218962-a197022b5858?ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8a2l0Y2hlbnxlbnwwfHwwfHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
        },
        {
          title: "Pool",
          description: "Et sunt esse esse dolores quo. Impedit aut repellat quia. Provident porro quia autem.\n" +
            "Dolorem cum quia totam totam. Et cum cum ut et accusantium sunt enim. Incidunt laborum harum accusantium.",
          photo:"https://images.unsplash.com/photo-1591285713698-598d587de63e?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=675&q=80"
        }],
      features: [
        'Air Conditioning',
        'Pool',
        'Fully-Equiped Kitchen',
        'Personal Chef (upon request)',
        'Air Conditioning',
        'Pool',
        'Fully-Equiped Kitchen',
        'Personal Chef (upon request)',
        'Air Conditioning',
        'Pool',
        'Fully-Equiped Kitchen',
        'Personal Chef (upon request)',
        'Air Conditioning',
        'Pool',
        'Fully-Equiped Kitchen',
        'Personal Chef (upon request)',
        'Air Conditioning',
        'Pool',
        'Fully-Equiped Kitchen',
        'Personal Chef (upon request)',
      ]
    }
  }
})
</script>

<style lang="scss">
.hero{
  z-index: 10;
  height: 100vh;
  background: white;
  //background: url(/hero-bg.jpg) no-repeat center center;
  .bg-hero{
    filter: brightness(0.75) contrast(0.8);
    height: 100%;
    background: url(/hero-bg.jpg) no-repeat center center fixed;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
    width: 97.5vw;
    height: 100%;
    content: " ";
    //z-index: -1;
  }
}


.glass{
      background-color: rgba(255, 255, 255, .2);
    -webkit-backdrop-filter: blur(0.5em);
    backdrop-filter: blur(0.5em);
}

.welcome{
  height: 100vh;
  z-index: 10;
}
.details{
  background: #fff;
  > div{
    border-color: #5f5c39 !important;
  }
}
.highlights{
  .swiper-slide {
    background-size: cover;
    p{
      //background: rgba(0,0,0,0.3);
      //backdrop-filter: blur(3px);

    }
  }


}
</style>
