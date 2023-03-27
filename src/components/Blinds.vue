<template>
  <div class="card" style="width: 18rem;">
    <b-card-img :src="blind.images.main" class="card-img-top" :alt="blind.name"></b-card-img>
    <div class="card-body text-center">
      <p class="card-text">From {{ blind.price_per_metre_squared }}</p>
      <b-button variant="primary" class="d-block" @click="showModal = true">Get Price</b-button>
    </div>
    <b-modal v-model="showModal" size="lg" centered>
      <div class="d-flex justify-content-between row">
        <div class="col-lg-4">
          <img style="max-height: 300px; width: auto;" :src="blind.images.thumb" class="card-img-top" :alt="blind.name">
        </div>
        <div class="col-lg-6">
          <h2 class="card-title mb-1">{{ blind.name }}</h2>
          <p>{{ blind.description }}</p>
          <div class="mt-3">
            <h6 class="text-bold">Enter Measurements to get a price</h6>
            <div class="d-flex gap-2">
              <div class="mr-3">
                <b-form-input type="number" v-model="width" placeholder="Width (cm)" @input="validateWidth"></b-form-input>
                <div class="text-danger">{{ widthError }}</div>
              </div>
              <div>
                <b-form-input type="number" v-model="drop" placeholder="Drop (cm)" @input="validateDrop"></b-form-input>
                <div class="text-danger">{{ dropError }}</div>
              </div>
            </div>
            <div v-if="!isValid" class="text-danger"></div>
            <h1 v-else-if="calculatedPrice" class="text-success text-center">{{`£${calculatedPrice}`}}</h1>
          </div>
        </div>
      </div>
      <template v-if="isValid" v-slot:modal-footer="{}">
        <b-button variant="primary" @click="addToBasket; resetModal">Add to basket</b-button>
        <b-button variant="outline-primary" @click="resetModal">Cancel</b-button>
      </template>
    </b-modal>
  </div>
</template>


<script>
export default {
  name: "Blind",
  props: {
    blind: Object,
  },
  data() {
    return {
      showModal: false,
      width: null,
      drop: null,
      widthError: null,
      dropError: null,
    };
  },
  computed: {
    calculatedPrice() {
      const { width, drop } = this;
      if (!width || !drop) return null;
      const price = this.blind.price_per_metre_squared;
      const pricePerSquareMeter = price / (this.blind.limits.width.min * this.blind.limits.drop.min);
      const area = (width / 100) * (drop / 100);
      const calculatedPrice = area * pricePerSquareMeter;
      return calculatedPrice.toFixed(2);
    },
    isValid() {
      return this.width && this.drop && !this.widthError && !this.dropError;
    },
  },
  methods: {
    addToBasket() {
      this.$emit('add-to-basket', { ...this.blind, width: this.width, drop: this.drop })
      this.resetModal()
    },
    resetModal(){
      this.width = null;
      this.drop = null;
      this.widthError = null;
      this.dropError = null;
    },
    validateWidth() {
      const { width } = this;
      if (width && (width < this.blind.limits.width.min || width > this.blind.limits.width.max)) {
        this.widthError = `Width should be between ${this.blind.limits.width.min}cm and ${this.blind.limits.width.max}cm.`;
      } else {
        this.widthError = '';
      }
    },
    validateDrop() {
      const { drop } = this;
      if (drop && (drop < this.blind.limits.drop.min || drop > this.blind.limits.drop.max )) {
        this.dropError = `Drop should be between ${this.blind.limits.drop.min}cm and ${this.blind.limits.drop.max}cm.`;
      } else {
        this.dropError = '';
      }
    },
    calculatePrice() {
      const { width, drop } = this;
      if (width && drop && width >= this.blind.limits.width.min && drop >= this.blind.limits.drop.min) {
        const area = width * drop;
        const pricePerSquareMeter = (width * drop) ** this.blind.price_per_metre_squared;
        this.calculatedPrice = (area * pricePerSquareMeter).toFixed(2);
      } else {
        this.calculatedPrice = null;
      }
    }
  }
}
</script>


<style scoped>
  .d-block{
    width: 100% !important;
  }

  .text-danger{
    font-size: 12px !important;
  }
</style>
