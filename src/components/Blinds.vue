<template>
    <div class="card text-center" style="width: 18rem;">
    <img :src="blind.images.main" class="card-img-top" alt="...">
    <div class="card-body">
        <h5 class="card-title">{{ blind.name }}</h5>
        <p class="card-text">From {{blind.price_per_metre_squared}}</p>
        <button @click="showModal" href="#" class="btn btn-primary btn-block" >Get Price</button>
    </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      blind: Object
    },
    methods: {
      showModal() {
        // Show modal logic here
      }
    }
  }
  </script>

  <style scoped>
    button{
        width: 100% !important;
    }
  </style>
  