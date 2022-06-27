<template>
<div class="parent-about flex flex-col items-center text-[24px]">
    <div class="mt-[50px] about-inf text-center mx-auto text-white w-[520px]">
        This is open source pet-project. Feel free to use it, or distribute it).
    </div>
        <router-link to="/" class="mt-[30px] underline text-white hover:text-[#0D014D]">Go to main page</router-link>
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
.about-inf{
    width: 90%;
}
</style>