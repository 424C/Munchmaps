<template>
  <section class="container">
    <div>
        <Vue2InteractDraggable
          v-for="(card, index) in cards"
          :key="index"
          :interact-out-of-sight-x-coordinate="500"
          :interact-max-rotation="15"
          :interact-x-threshold="200"
          :interact-y-threshold="200"
          @draggedRight="right"
          class="rounded-borders card fixed fixed--center"
          :class="{
            'card--top': index === 0
          }">
          <div class="flex flex--center" style="height: 100%">
            <h1>{{card.text}}</h1>
          </div>
      </Vue2InteractDraggable>
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
      cards: [
        { text: 'one' },
        { text: 'two' },
        { text: 'three' },
      ]
    }
  },
  methods: {
    right() {
      setTimeout(() => this.cards.shift(), 300);
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  background: #eceff1;
  width: 100%;
  height: 100vh;
}

.flex {
  display: flex;
  &--center {
    align-items: center;
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
  border-radius: 2rem
}
.card {
  pointer-events: none;
  width: 300px;
  height: 400px;
  &:nth-child(1) {
    background: pink;
    z-index: 3;
  }
  &:nth-child(2) {
    z-index: 2;
    background: red;
    top: 52%;
  }
  &:nth-child(3) {
    z-index: 1;
    background: green;
    top: 54%;
  }
  &--top {
    pointer-events: auto !important;
  }
}
</style>