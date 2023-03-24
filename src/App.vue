<template>
  <Header :blinds="blinds"/>
  <BlindsList :blinds="blinds.products"/>
</template>

<script>
import Header from './components/Header.vue'
import BlindsList from './components/BlindsList.vue'
export default {
  name: 'App',

  components: {
    Header,
    BlindsList,
  },

  data(){
    return {
      blinds: {}
    }
  },

  methods: {
    async fetchBlinds(){
      const apiURL = `https://www.interiorgoodsdirect.com/interview/api/products/?key=`
      const apiKey = `6HJx2R8st$%Q`
      const res = await fetch(`${apiURL}${apiKey}`)

      const { data } = await res.json()
      //console.log(data.products)
      return data
    }
  },

  async created(){
    this.blinds = await this.fetchBlinds()
    console.log(this.blinds)
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

</style>
