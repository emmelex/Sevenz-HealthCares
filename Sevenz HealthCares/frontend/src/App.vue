<template>
  <section id="container">
      <Dashboard />
      <Record />
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Dashboard from './components/Dashboard.vue';
import Record from './components/Record.vue';


export default defineComponent({
  name: 'App',
  components: {
    Dashboard,
    Record,
},
data() {
    return {

    }
},


});
</script>

<style>
*{
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
    padding: 0px;
    margin: 0px;
}
body {
    background-color: #c1c1c1;
}
#container {
    background-color: #c1c1c1;
    display: flex;
    padding-top: 30px;
    align-items: center;
    padding-bottom: 40px;
    justify-content: center;
}
@media only screen and (min-width: 200px)  and (max-width: 801px) {  
        body {
                padding: 0px 20px 0px 15px;
            }
    }
</style>
