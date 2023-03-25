<template>
      <!-- Modal -->
      <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog modal-dialog-centered pb-5" style="width: 350rem;">
          <div class="modal-content">
            <div class="modal-header">
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body d-flex justify-content-between row">
            <div class="col-lg-4"> 
              <img style="width: 10rem;" :src="blind.images.thumb" class="card-img-top" :alt="blind.name">
            </div>
              <div class="col-lg-8">
                <h3 class="modal-title ml-10" id="exampleModalLabel">{{ blind.name }}</h3>
                <p class="modal-title" id="exampleModalLabel">{{ blind.description }}</p>
                <div class="mt-3">
                  <h6 class="text-bold">Enter Measurements to get a price</h6>
                  <div class="d-flex gap-2"> 
                    <input type="text" class="form-control" placeholder="Width (cm)" aria-label="Username" aria-describedby="basic-addon1">
                    <input type="text" class="form-control" placeholder="Drop (cm)" aria-label="Username" aria-describedby="basic-addon1">
                  </div>
                </div>
                
              </div>
              <!-- Add any other details you want to show in the modal body -->
            </div>
          </div>
        </div>
      </div>
</template>

<script>
    export default {
        name: 'Modal',
        props: {
          blind: Object
        }
    }
</script>

<style scoped>
  .modal-dialog{
    height: 800px !important;
  }
</style>