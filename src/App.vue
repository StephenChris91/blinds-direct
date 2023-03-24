<template>
  <Header :blinds="blinds"/>
  <BlindsList :blindsList="blinds.products"/>
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
  data() {
    return {
      blinds: {},
    }
  },
  async created() {
    const apiURL = `https://www.interiorgoodsdirect.com/interview/api/products/?key=`
    const apiKey = `6HJx2R8st$%Q`
    const res = await fetch(`${apiURL}${apiKey}`)
    const { data } = await res.json()
    this.blinds = data
    console.log(this.blinds)
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
</style>
