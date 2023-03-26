<template>
    <div class="card" style="width: 18rem;">
      <img :src="blind.images.main" class="card-img-top" :alt="blind.name">
      <div class="card-body text-center">
        <h5 class="card-title">{{ blind.name }}</h5>
        <p class="card-text">From {{ blind.price_per_metre_squared }}</p>
        <button href="#" class="btn btn-primary d-block" data-bs-toggle="modal" :data-bs-target="'#exampleModal-' + blindId" @click="showModal = true">Get Price</button>
      </div>
      <Modal :blind="blind" :show="showModal" :modalId="'exampleModal-' + blindId" @close="showModal = false"></Modal>
    </div>
  </template>
  
  <script>
  import Modal from './Modal.vue';
  
  export default {
    name: 'Blind',
    props: {
      blind: Object,
      blindId: Number
    },
    components: {
      Modal
    },
    data() {
      return {
        showModal: false,
      };
    }
  };
  </script>
  
  <style scoped>
    button {
      width: 100% !important;
    }
  </style>
  