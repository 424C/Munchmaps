<template>
  <section class="container">
    <div v-if="errorStr">
    Sorry, but the following error
    occurred: {{errorStr}}
  </div>
  <div v-if="!isHidden">
    <button v-on:click="callApi" class="bg-orange-500 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded">Let's Munch!</button>
    <img v-bind:src="require('./layout/burgerLogo.png')" class="fixed fixed--center" style="height: 300px; width: 300px;"/>
  </div>
  <div v-else>
    <img v-bind:src="require('../assets/loading.gif')" v-if='loading' class="fixed fixed--center"/>
    <div v-else>
    <div
      v-if="current"
      class="fixed fixed--center"
      style="z-index: 3">


      <Vue2InteractDraggable
        v-if="isVisible"
        :interact-out-of-sight-x-coordinate="500"
        :interact-max-rotation="15"
        :interact-x-threshold="200"
        :interact-y-threshold="200"

        @draggedRight="right"
        @draggedLeft="left"
        class="rounded-borders card card--one">

        <div style="height: 100%">
          <img v-bind:src="current.image_url" class="rounded-borders"/>
          <div class="text">
            <h2 class="text-3xl">{{current.name}}</h2>
            <i class="text-xl">Distance: {{(current.distance/1609).toFixed(2)}} (mi)</i>
            
          </div>
        </div>
      </Vue2InteractDraggable>
    </div>
    <div
      v-if="next"
      class="rounded-borders card card--two fixed fixed--center"
      style="z-index: 2">
      <div style="height: 100%">
        <img v-bind:src="next.image_url" class="rounded-borders"/>
        <div class="text">
          <h2 class="text-3xl">{{next.name}}</h2>
          <i class="text-xl">Distance: {{(next.distance/1609).toFixed(2)}} (mi)</i>
        </div>
      </div>
    </div>
    </div>
  </div>
  </section>
</template>

<script>
import { Vue2InteractDraggable, InteractEventBus } from 'vue2-interact'
import axios from "axios";

export default {
  name: 'SwipeableCards',
  components: { Vue2InteractDraggable },
  data() {
    return {
      myJson: [],
      loading: true,
      errored: true,
      isVisible: true,
      index: 0,
      location: null,
      gettingLocation: false,
      errorStr: null,
      isHidden: false,
    }
  },
  created()
  {
    //do we support geolocation
    if(!("geolocation" in navigator)) {
      this.errorStr = 'Geolocation is not available.';
      return;
    }

    this.gettingLocation = true;
    // get position
    navigator.geolocation.getCurrentPosition(pos => {
      this.gettingLocation = false;
      this.location = pos;
    }, err => {
      this.gettingLocation = false;
      this.errorStr = err.message;
    })
  },
  computed: {
    current() {
      return this.myJson.businesses[this.index]
    },
    next() {
      return this.myJson.businesses[this.index + 1]
    },
  },
  methods: {
    callApi(){
      this.isHidden = true;
      axios.get(`${'https://cors-anywhere.herokuapp.com/'}https://api.yelp.com/v3/businesses/search`, {
      headers: {
        Authorization: process.env.VUE_APP_YELP_KEY,
      },
      params:{
        term: 'restaurants',
        latitude: this.location.coords.latitude,
        longitude: this.location.coords.longitude,
        distance: 1600,
        offset: Math.floor(Math.random() * 300) // psuedo random retrieval from yelp. Selects from a list of resstaurants at a specified index
      }
    })
    .then((response) => {
      this.myJson = response.data;
    })
    .catch((error) => {
      console.log(error)
    })
    .finally(() => this.loading = false)
    },
    right() {
      setTimeout(() => this.isVisible = false, 200)
      setTimeout(() => {
        this.index++
        this.isVisible = true
      }, 300)
    },
    left() {
      setTimeout(() => this.isVisible = false, 200)
      setTimeout(() => {
        this.index++
        this.isVisible = true
      }, 300)
    },
  }
}
</script>

<style lang="scss" scoped>
.container {
  background:white;
  width: 100%;
  height: 100vh;
}

.flex {
  display: flex;
  &--center {
    margin-top: 35px;
    align-items: center;
    justify-items: center;
    justify-content: center;
  }
}

.fixed {
  position: fixed;
  &--center {
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  }
}
.rounded-borders {
  border-radius: 12px;
}

.card {
  width: 300px;
  height: 400px;
  color: white;

  img {
    object-fit: cover;
    display: block;
    width: 100%;
    height: 100%;
  }
  &--one {
    box-shadow: 0 1px 3px black;
  }
  &--two {
    box-shadow: 0 10px 15px black;
  }
  &--three {
    box-shadow: 0 20px 30px black;
  }

  .text {
    position: absolute;
    bottom: 0;
    width: 100%;
    background: white;
    color: black;
    span {
      font-weight: bolder;
    }
  }
}
</style>
