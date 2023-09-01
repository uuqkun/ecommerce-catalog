<script>
import Button from './Button.vue';
import Rating from './Rating.vue';

export default {
  name: "Product",
  components: {
    Rating,
    Button
  },
  data() {
    return {
      products: [],
      product: [],
      index: 0
    }
  },
  methods: {
    async getProductData() {
      const response = await fetch("https://fakestoreapi.com/products");

      const results = await response.json();

      // Save products data to local state
      this.products = results;
      this.product = this.products[this.index]


    },
    nextProduct() {
      this.product = this.products[this.index++]
      console.log(this.product["id"])
    },
    buyProduct() {}
  },
  created() {
    this.getProductData();
  }
}

</script>

<template>
  <!-- content -->
  <div class="container__card">
    <div class="container__card-img">
      <img src="../assets/images/mock_image.png" :alt="product['title']" />
    </div>
    <div class="container__card-content">
      <header>
        <h1>{{ product['title'] }}</h1>
        <div class="container__card-subheader">
          <p>{{ product['category'] }}</p>

          <Rating />
        </div>
      </header>

      <p>{{ product['description'] }}</p>

      <div>
        <div class="container__card-price">
          <h2 class="female-accent">${{ product['price'] }}</h2>
        </div>

        <div class="container__card-btns">
          <Button title="Buy Now" category="female" :option="1" :clicked="buyProduct"/>
          <Button title="Next Product" category="female" :option="2" :clicked="nextProduct" />
        </div>
      </div>
    </div>
  </div>
</template>

<style></style>