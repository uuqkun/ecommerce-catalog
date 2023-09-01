<script>
import Product from './Product.vue';

export default {
    name: "ProductDisplay",
    components: {
        Product,
    },
}

</script>

<template>
    <div class="container flex">
        <div class="bg-female" />

        <Product />
    </div>
</template>

<style scoped>
.container { 
    justify-content: center;
    align-items: center;
    height: 100vh;
}

</style>