<template>
    <div class="flex flex-row justify-between px-16">
        <button class="shadow-lg">Button</button>
        <h1 class='text-6xl text-orange-700' style="text-shadow:1px 1px black;">Munchmaps</h1>
        <img src="./burgerLogo.png" alt="BurgerLogo" style="height: 100px; width: 100px;">
    </div>
</template>

<script>
export default {
    name: "Header"
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
