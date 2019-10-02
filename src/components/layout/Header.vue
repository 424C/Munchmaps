<template>
    <div>

    <div class="flex flex-row justify-between px-16">
        <Slide width="200">
            <div>
            <h1 class="text-3xl">Distance</h1>
            <input type="radio" name="distance" value="5miles">5 Miles
            </div>
            
        </Slide>
        <h1 class='text-6xl text-orange-700' style="text-shadow:1px 1px black;">Munchmaps</h1>
        <img src="./burgerLogo.png" alt="BurgerLogo" style="height: 100px; width: 100px;">
    </div>
    </div>
</template>



<script>

import { Slide } from 'vue-burger-menu'

export default {
    name: "Header",
    components: {
        Slide
    }
}

</script>

<style scoped>
/* Adding External Font For Header */
@font-face {
        font-family: "BebasNeue";
        src: url("./BebasNeue-Regular.ttf");
}

*{
    font-family: "BebasNeue";
}
</style>
