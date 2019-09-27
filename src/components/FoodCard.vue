<template>
  <section class="container">
    <div class="fixed-center">
        <Vue2InteractDraggable
            @draggedRight="draggedRight"
            :interact-max-rotation="15"
            :interact-out-of-sight-x-coordinate="500"
            :interact-x-threshold="200">
  <div>
    <h1 strong>Drag me!</h1>
  </div>
</Vue2InteractDraggable>

    </div>
  </section>
</template>

<script>
import { Vue2InteractDraggable } from 'vue2-interact'

export default {
  name: 'FoodCards',
  components: { Vue2InteractDraggable }
}
</script>