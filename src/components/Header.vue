<template>
    <div class="container-fluid p-3 bg-light text-center">
            <h1 id="header-title">BLINDS DIRECT</h1>
            <h6 id="#header-title-sub" class="mb-3 mt-0">DEFINED BY QUALITY</h6>
            <div class="container border-top border-bottom p-3">
                <p class="">{{ blinds.description }}</p>
            </div>
    </div>
</template>

<script>

export default {
    name: 'Header',
    props: {
    blinds: Object,
  },
}

</script>

<style scoped>
    h1, h6{
        font-family: 'serif';
    }
</style>