<template>
    <div class="text-[32px] parent bg-[#ffffffd7] w-fit p-[30px] rounded-[10px] hover:bg-white">
        <h1 class="text-blue-400 text-center mb-[10px]">Weather in</h1>
        <input @blur="changeBg()" @focus="changeBg()" class="cityName pl-[5px] bg-blue-400 placeholder-[#ffffffc6] rounded-[5px] text-white" type="text" placeholder="City">
        <button class="isBtn rounded-[10px] ml-[5px] bg-blue-400 text-white"><i class="fa-solid fa-magnifying-glass"></i></button>
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
    margin-top: 100px;
}
.parent:hover{
    transition-duration: .7s;
}
@media screen and (min-width: 900px){
    .isBtn{
        padding-inline: 10px;
    }
}
@media screen and (max-width: 900px) {
    .parent{
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 80%;
        margin-top: 150px;
        background-color: white;
    }
    .isBtn{
        margin-top: 15px;
        width: 20%;
    }
    .cityName{
        width: 80%;
    }
}
</style>