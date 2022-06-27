<template>
  <div class="main">
    <Logo />
    <router-view></router-view>
    <div v-if="homePage" class="main-page">
      <InputForm class="inputForm mt-[20px] mx-auto"/>
      <Result class="mt-[20px] mx-auto"/>
</div>
  </div>
</template>

<script>
import { RouterLink, RouterView } from 'vue-router'
import InputForm from './components/InputForm.vue'
import Result from './components/Result.vue'
import Logo from './components/Logo.vue'

  export default{
    name: 'App',
    components: {
      InputForm, Result, Logo
    },
    data(){
      return {
      }
    },
    methods: {
    },
    computed: {
      homePage() {
        if(this.$route.path == "/") {
          return true
        } else {
          return false
        }
      }
    }
}

</script>

<style scoped>

</style>