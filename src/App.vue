<template>
  <Courses/>

</template>

<script>
import Courses from './components/Courses.vue'
// import Courses from './components/Courses.vue'
export default {
    name: 'App',
    components: { Courses,}

}
</script>

<style>
#app {
    font-family: Avenir, Arial, Helvetica, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #444;
    margin-top: 60px;
}
body {
    margin: 0;
    background: grey;
    background-image: '220px-UniLagos.jpg'

}
</style>