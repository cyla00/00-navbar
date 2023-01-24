<script>
import { defineComponent } from 'vue'
import Navbar from './components/Navbar.vue'

export default defineComponent({
    data() {
        return{

        }
    },
    components: {
        Navbar
    }
})
</script>


<template>
    <Navbar :dark="true"/>
</template>

<style>
body{
    margin: 0;
    padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
  scroll-behavior: smooth;
  text-align: center;
}
</style>
