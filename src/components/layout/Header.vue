<template>
    <div>
    <div class="flex flex-row justify-between px-16 py-2 items-center">
        <Slide disableOutsideClick width="175">
            <div class="block items-center">
            <h1 class="text-4xl items-center mr-8">Distance</h1>
            <div class="mt-4">
                <div>
                    <ul>
                        <label class="inline flex items-center">
                        <li><input type="radio" v-on:change="emitGlobalClickEvent" name="distance" v-model="radius" class="form-radio" value="800">
                        <span class="ml-2">4 Blocks</span>
                        </li>
                        </label><br>
                        <label class="inline flex items-center">
                        <li><input type="radio" v-on:change="emitGlobalClickEvent" name="distance" v-model="radius" class="form-radio" value="1609">
                        <span class="ml-2">1 Mile</span>
                        </li></label><br>
                        <label class="inline flex items-center">
                        <li><input type="radio" v-on:change="emitGlobalClickEvent" name="distance" v-model="radius" class="form-radio" value="3200">
                        <span class="ml-2">2 Miles</span>
                        </li></label><br>
                        <label class="inline flex items-center">
                        <li><input type="radio" v-on:change="emitGlobalClickEvent" name="distance" v-model="radius" class="form-radio" value="8000">
                        <span class="ml-2">5 Miles</span>
                        </li>
                        </label><br>
                        <label class="inline flex items-center">
                        <li><input type="radio" v-on:change="emitGlobalClickEvent" name="distance" v-model="radius" class="form-radio" value="16000">
                        <span class="ml-2">10 Miles</span>
                        </li>
                        </label><br>
                    </ul>
                </div>
            </div>
            </div>
        </Slide>
        <h1 id="center" class=' ml-8 text-orange-700' style="text-shadow:1px 1px black; font-size: 84px;">Munchmaps</h1>
        <img :src="require('./burgerLogo.png')" alt="BurgerLogo" style="height: 100px; width: 100px;"/>
    </div>
    <div class="bg-gray-800" style="padding-top:.1rem; padding-bottom:.1rem;">
        
    </div>
    <br>
    </div>
</template>



<script>

import { Slide } from 'vue-burger-menu'
import { EventBus } from '../../../event-bus.js'

export default {
    name: 'Header',
    components: {
        Slide
    },
    data(){
        return{
            radius: 1609
        }  
    },
    methods: {
        emitGlobalClickEvent(){
            EventBus.$emit('i-got-clicked', this.radius);
        }
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
        width: 62px;
        height: 62px;
        left: 36px;
        top: 30px;
        cursor: pointer;
        }

        .bm-overlay {
      background: rgba(255, 255, 255, 0);
    }
    
    
    #center{
        margin-left: 1.5em;
    }

</style>
