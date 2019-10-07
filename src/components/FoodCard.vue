<template>
  <section class="container">
    <div class="fixed fixed--center" style="z-index: 3">
      <Vue2InteractDraggable
        v-if="isVisible"
        :interact-out-of-sight-x-coordinate="500"
        :interact-max-rotation="15"
        :interact-x-threshold="200"
        :interact-y-threshold="200"
        @draggedRight="right"
        class="rounded-borders card card--one">
        <div class="flex flex--center" style="height: 100%">
          <h1>{{current.text}}</h1>
        </div>
      </Vue2InteractDraggable>
    </div>
    <div
      v-if="next"
      class="rounded-borders card card--two fixed fixed--center"
      style="z-index: 2">
      <div class="flex flex--center" style="height: 100%">
        <h1>{{next.text}}</h1>
      </div>
    </div>
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
<script>
import { Vue2InteractDraggable } from 'vue2-interact'

export default {
  name: 'SwipeableCards',
  components: { Vue2InteractDraggable },
  data() {
    return {
      isVisible: true,
      index: 0,
      cards: [
        { text: 'one' },
        { text: 'two' },
        { text: 'three' },
      ]
    }
  },
  computed: {
    current() {
      return this.cards[this.index]
    },
    next() {
      return this.cards[this.index + 1]
    }
  },
  methods: {
    right() {
      setTimeout(() => this.isVisible = false, 200)
      setTimeout(() => {
        this.index++
        this.isVisible = true
      }, 300)
    }
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
  &--one {
    background-image: url('../assets/salmon-sushi.jpg')
    // background-color: pink;
  }
  &--two {
    background-image: url('../assets/hamburger.jpg');
    // background-color: red;
    width: 280px;
    top: 51%;
  }
  &--three {
    // background-color: orange;
    background-image: url('../assets/ramen.jpg');
    width: 260px;
    top: 51.8%;
  }
}
</style>
