<script>
import Button from './Button.vue';
import Rating from './Rating.vue';
import UnavailableProduct from "./UnavailableProduct.vue";

export default {
  name: "Product",
  components: {
    Rating,
    Button,
    UnavailableProduct
  },
  data() {
    return {
      products: [],
      product: [],
      index: 0,
      isMaleProduct: false,
      isReady: false
    }
  },
  methods: {
    async getProductData() {
      try {
        const response = await fetch("https://fakestoreapi.com/products");

        if (!response.ok) {
          throw new Error("Gagal mengambil data dari API");
        }

        const results = await response.json();

        // Check if the results isn't null || undefined
        if (results !== null || results !== undefined || response.ok) {
          this.isReady = true
        }

        // Save products data to local state
        this.products = results;
        this.product = this.products[this.index]

        if (this.product['category'] === "men's clothing") this.isMaleProduct = true;
        else this.isMaleProduct;
      } catch (error) {
        console.error("Terjadi kesalahan: ", error.message)
      }



    },
    nextProduct() {
      if (this.index === this.products.length - 1) {
        this.index = 0;
        this.product = this.products[this.index++]
      } else {
        this.product = this.products[this.index++]
      }

      const isWomenProduct = this.product['category'] === "women's clothing" || this.product['category'] === "jewelery";

      if (this.product['category'] === "men's clothing") {
        this.isMaleProduct = true;
      }
      else if (isWomenProduct) {
        this.isMaleProduct = false;
      }
      else {
        this.isMaleProduct = true;
      }

    },
    buyProduct() { },
  },
  created() {
    this.getProductData();
  },
}

</script>

<template>
  <div class="fragment flex-center">
    <!-- content -->
    <div v-if="isReady === false">
      <UnavailableProduct />
    </div>
    <div v-else class="container__card flex">
      <div :class="[isMaleProduct ? 'bg-male' : 'bg-female', 'container__card-bg-product']" />

      <div class="container__card-img flex-center">
        <img :src="product['image']" />
      </div>

      <div class="container__card-content flex">
        <header class="flex">
          <h1 :class="[isMaleProduct ? 'txt-male-accent' : 'txt-female-accent', 'text-header']">{{ product['title'] }}
          </h1>
          <div class="container__card-subheader flex">
            <p class="text-subheader">{{ product['category'] }}</p>

            <Rating />
          </div>
        </header>

        <p class="p-text text-dark container__card-desc">{{ product['description'] }}</p>

        <div class="container__card-price flex">
          <h2 :class="[isMaleProduct ? 'txt-male-accent' : 'txt-female-accent', 'female-accent text-header']">${{
            product['price'] }}</h2>
          <div class="container__card-btns flex">
            <Button title="Buy Now" :category="[isMaleProduct ? 'male' : 'female']" :option="1" :clicked="buyProduct" />
            <Button title="Next Product" :category="[isMaleProduct ? 'male' : 'female']" :option="2"
              :clicked="nextProduct" />
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<style scoped src="../assets/style/product.css" />