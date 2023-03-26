<template>
  <div class="container mb-5 mx-auto row justify-content-between">
    <div class="mt-5 col-sm-6 col-md-6 col-lg-3" v-for="(blind, index) in blindsList" :key="index">
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
  },
  components: {
    Blinds,
  }
}
</script>
