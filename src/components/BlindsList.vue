<template>
    <div class="container mb-5 mx-auto row justify-content-between">
      <div class="mt-5 col-sm-6 col-md-6 col-lg-3" v-for="blind in blindsList" :key="blind.id">
        <Blinds :blind="blind"/>
      </div>
    </div>
  </template>  

<script>
import Blinds from './Blinds.vue';
    export default {
        name: 'BlindsList',
        props: {
        blindsList: Array,
    },
        components: {
            Blinds,
        }
    }
</script>

<style scope>
    
</style>