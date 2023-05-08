<template>
  <div class="home">
    <div class=slider>
      <div class="slides">
        <input type="radio" name="radio-btn" id="radio1">
        <input type="radio" name="radio-btn" id="radio2">
        <input type="radio" name="radio-btn" id="radio3">
        <input type="radio" name="radio-btn" id="radio4">

        <div class="slide first">
          <img src="../assets/img/banner-do-shop-thoi-trang-nam-tphcm-tmluxury.jpg">
        </div>
        <div class="slide">
          <img src="../assets/img/download.jpg">
        </div>
        <div class="slide">
          <img src="../assets/img/OIP.jpg">
        </div>
        <div class="slide">
          <img src="../assets/img/download.jpg">
        </div>

        <div class="navigation-auto">
          <div class="auto-btn1"></div>
          <div class="auto-btn2"></div>
          <div class="auto-btn3"></div>
          <div class="auto-btn4"></div>
        </div>
      </div>
      <div class="navigation-manual">
        <label for="radio1" class="manual1-btn"></label>
        <label for="radio2" class="manual1-btn"></label>
        <label for="radio3" class="manual1-btn"></label>
        <label for="radio4" class="manual1-btn"></label>
      </div>
    </div>

    <div class="columns is-multiline">
      <div class="column is-12">
          <h2 class="is-size-2 has-text-centered">Latest products</h2>
      </div>

      <ProductBox 
        v-for="product in latestProducts"
        v-bind:key="product.id"
        v-bind:product="product" />
    </div>
  </div>
</template>


<script>
import axios from 'axios'

import ProductBox from '../components/ProductBox.vue'

export default {
  name: 'Home',
  data() {
    return {
      latestProducts: []
    }
  },
  components: {
    ProductBox
  },
  mounted() {
    this.getLatestProducts()

    document.title = 'Home | Djackets'
  },
  methods: {
    async getLatestProducts() {
      this.$store.commit('setIsLoading', true)

      await axios
        .get('/api/v1/latest-products/')
        .then(response => {
          this.latestProducts = response.data
        })
        .catch(error => {
          console.log(error)
        })

      this.$store.commit('setIsLoading', false)
    }
  }
}
</script>