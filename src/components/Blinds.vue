<template>
  <div class="card" style="width: 18rem;">
    <b-card-img :src="blind.images.main" class="card-img-top" :alt="blind.name"></b-card-img>
    <div class="card-body text-center">
      <p class="card-text">From {{`£${calculateFromPrice()}`}}</p>
      <b-button variant="primary" class="d-block" @click="showModal = true">Get Price</b-button>
    </div>
    <b-modal v-model="showModal" size="lg" centered hide-footer="true">
      <div class="d-flex justify-content-between row">
        <div class="col-lg-4 col-sm-12 col-md-6">
          <img style="max-height: 600px; width: auto;" :src="blind.images.thumb" class="card-img-top mx-auto" :alt="blind.name">
        </div>
        <div class="col-lg-7 col-sm-12">
          <h2 class="card-title mb-1">{{ blind.name }}</h2>
          <p>{{ blind.description }}</p>
          <div class="mt-3 ">
            <h6 class="text-bold">Enter Measurements to get a price</h6>
            <div class="d-flex gap-2 mb-3">
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
            <div v-if="isValid">
              <b-button variant="primary" class="d-block" @click="addToBasket; resetModal">Add to basket</b-button>
            </div>
          </div>
        </div>
      </div>
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
      const inputedNum = (width / 100) * (drop / 100);
      const price = inputedNum * this.blind.price_per_metre_squared;
      return price.toFixed(2);
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
    calculateFromPrice(){
     const fromPrice = this.blind.price_per_metre_squared * (this.blind.limits.width.min * this.blind.limits.drop.min) / 10000
     return fromPrice.toFixed(2)
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
