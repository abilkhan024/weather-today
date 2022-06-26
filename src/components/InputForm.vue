<template>
    <div class="text-[32px] parent bg-[#FFFFFF95] w-fit p-[30px] rounded-[10px] hover:bg-white">
        <h1 class="text-blue-400 text-center mb-[10px]">Weather in</h1>
        <input @blur="changeBg()" @focus="changeBg()" class="cityName pl-[5px] bg-blue-400 placeholder-white rounded-[5px] text-white" type="text" placeholder="City">
        <button class="isBtn rounded-[10px] px-[15px] ml-[5px] bg-blue-400 text-white">is..</button>
    </div>
</template>

<script>
export default {
    name: 'InputForm',
    created(){
    },
    methods: {
        changeBg(){
        if(document.querySelector('.cityName') === document.activeElement){
            document.querySelector('.parent').classList.add('bg-white')
        }
        else{
            document.querySelector('.parent').classList.remove('bg-white')
        }
        }
    }
    
}
</script>

<style scoped>
.parent{
    transition: all .7s ease-out;
}
.parent:hover{
    transition-duration: .7s;
}

</style>