<template>
    <div>
    <div class="flex flex-row justify-between px-16 items-center">
        <Slide disableOutsideClick width="175">
            <div class="block items-center">
            <h1 class="text-4xl items-center mr-8">Distance</h1>
            <div class="mt-4">
                <div>
                    <ul>
                        <label class="inline flex items-center">
                        <li><input type="radio" name="distance" class="form-radio" value="1" checked>
                        <span class="ml-2">4 Blocks</span>
                        </li>
                        </label><br>
                        <label class="inline flex items-center">
                        <li><input type="radio" name="distance" class="form-radio" value="2">
                        <span class="ml-2">1 Mile</span>
                        </li></label><br>
                        <label class="inline flex items-center">
                        <li><input type="radio" name="distance" class="form-radio" value="3">
                        <span class="ml-2">2 Miles</span>
                        </li></label><br>
                        <label class="inline flex items-center">
                        <li><input type="radio" name="distance" class="form-radio" value="4">
                        <span class="ml-2">5 Miles</span>
                        </li>
                        </label><br>
                        <label class="inline flex items-center">
                        <li><input type="radio" name="distance" class="form-radio" value="4">
                        <span class="ml-2">10 Miles</span>
                        </li>
                        </label><br>
                    </ul>
                </div>
            </div>
            </div>
        </Slide>
        <h1 id="center" class='text-6xl ml-8 text-orange-700' style="text-shadow:1px 1px black;">Munchmaps</h1>
        <img :src="require('./burgerLogo.png')" alt="BurgerLogo" style="height: 100px; width: 100px;"/>
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

<style>
/* Adding External Font For Header */
    @font-face {
            font-family: "BebasNeue";
            src: url("./BebasNeue-Regular.ttf");
    }

    *{
        font-family: "BebasNeue";
    }

    .bm-burger-bars {
      background-color:rgb(189, 80, 7);
      box-shadow: 1px 1px 1px black;
    }

    .bm-burger-button {
        position: fixed;
        width: 62px;
        height: 62px;
        left: 36px;
        top: 68px;
        cursor: pointer;
        }

        .bm-overlay {
      background: rgba(255, 255, 255, 0);
    }

    #center{
        margin-left: 1.5em;
    }

</style>
