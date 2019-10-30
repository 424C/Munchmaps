<template>
  <section class="container">
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
          <!-- <img :src="current.src" class ="rounded-borders"/> -->
          <img v-bind:src="current.image_url" class="rounded-borders"/>
          <div class="text">
            <h2>{{current.name}}</h2>
          </div>
        </div>
      </Vue2InteractDraggable>
    </div>
    <div
      v-if="next"
      class="rounded-borders card card--two fixed fixed--center"
      style="z-index: 2">
      <div style="height: 100%">
        <!-- <img :src="require(`../assets/${next.src}`)" class ="rounded-borders"/> -->
        <img v-bind:src="next.image_url" class="rounded-borders"/>
        <div class="text">
          <h2>{{next.name}}</h2>
        </div>
      </div>
    </div>

    <!--hidden cards beneath-->
    <div
      v-if="index + 2 < cards.length"
      class="rounded-borders card card--three fixed fixed--center"
      style="z-index: 1">
      <div class="flex flex--center" style="height: 100%">
        <h1>test</h1>
      </div>
    </div>
  </section>
</template>


//SCRIPT


<script>
import { Vue2InteractDraggable, InteractEventBus } from 'vue2-interact'
import axios from "axios";
// const EVENTS = {
//   ACCEPT: 'accept',
//   REJECT: 'reject'
// }

export default {
  name: 'SwipeableCards',
  components: { Vue2InteractDraggable },
  data() {
    return {
      myJson: [],
      isVisible: true,
      index: 0,
      cards: [
        //we will need to redirect the yelp image url to the src variables
        //and populate the name field
        { src: 'hamburger.jpg', name: 'hamburger'},
        { src: 'ramen.jpg', name: 'ramen'},
        { src: 'salmon-sushi.jpg', name: 'Sushi'}
      ]
    }
  },
  mounted(){
      axios.get(`${'https://cors-anywhere.herokuapp.com/'}https://api.yelp.com/v3/businesses/search`, {
      headers: {
        Authorization: 'Bearer uK5jXy6Dqs7d0YzLK_2tV0DT1bQK5Q-PihFW13vzdmQ7cU4gIkXBuzhtMpyEPhq3d7kLo-RhCw_Kx4GiEMHQDB7ZrbCy3EQP5zZW_HDNkQ6O1n0E_U6CJMXUUtykXXYx'
      },
      params:{
        term: 'restaurants',
        location: 92869,
        distance: 1600
      }
    })
    .then((response) => {
      this.myJson = response.data;
    })
    .catch((error) => {
      console.log ('Error')
    })
  },
  computed: {
    current() {
      return this.myJson.businesses[this.index]
    },
    next() {
      return this.myJson.businesses[this.index + 1]
    }
  },
  methods: {
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
    }
  }
}
</script>

//START CSS

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
