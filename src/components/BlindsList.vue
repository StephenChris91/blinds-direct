<template>
  <div class="container mb-5 mx-auto row d-flex justify-content-between m-4">
    <div id="blind" class="mt-5 col-sm-6 col-md-6 col-lg-3" v-for="(blind, index) in blindsList" :key="index">
      <Blinds :blind="blind" :blindId="'blind-' + index"/>
    </div>
  </div>
</template>

<script>
import Blinds from './Blinds.vue';
export default {
  name: 'BlindsList',
  props: {
    blindsList: Array,
    blindId: String,
  },
  components: {
    Blinds,
  }
}
</script>

<style scoped>
  
</style>
