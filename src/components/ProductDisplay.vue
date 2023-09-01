<script>
import Product from './Product.vue';

export default {
    name: "ProductDisplay",
    components: {
        Product,
    },
    data() {
        return {
            // products: [],
            // product: []
        }
    },
    methods: {
        // async getProductData() {
        //     const response = await fetch("https://fakestoreapi.com/products");

        //     const results = await response.json();
        //     this.products = results;

        // },
    },
    // created() {
    //     this.getProductData();
    // }
}

</script>

<template>
    <div class="container">
        <div class="bg-female" />

        <!-- :title="products['title']" 
        :description="products['description']" 
        :price="products['price']" 
        :image="products['image']"    
        :category="products['category']" -->
        <Product />
    </div>
</template>

<style></style>