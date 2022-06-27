<template>
    <div class="parent-about w-fit mx-auto mt-[10px]">
        <router-link to="/about" class="text-white text-[42px] hover:text-[#2075b1]">Weather Today <i class="fa-solid fa-copyright text-[14px]"></i></router-link>
    </div>
</template>

<script>
export default {
    name: 'About'    
}
</script>

<style scoped>
    a{
        transition-duration: .5s;
    }
</style>