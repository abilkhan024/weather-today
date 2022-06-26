<template>
  <div class="main my-auto">
    <InputForm class="mt-[20px] mx-auto"/>
    <Result class="mt-[20px] mx-auto"/>
  </div>
</template>

<script>
import { RouterLink, RouterView } from 'vue-router'
import InputForm from './components/InputForm.vue'
import Result from './components/Result.vue'

  export default{
    name: 'App',
    components: {
      InputForm, Result
    },
    data(){
      return {
      }
    },
    methods: {
    }
}

</script>

<style>
</style>
