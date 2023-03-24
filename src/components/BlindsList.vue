<template>
   <div v-for="blind in blindList" :key="blind.id" class="container">
    <Blinds :blinds="blinds"/>
   </div>
</template>

<script>
import Blinds from './Blinds.vue'
    export default {
        name: 'BlindsList',
        props: {
            blindList: Array,
        },
        components: {
            Blinds,
        }
    }
</script>