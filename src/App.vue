<template>
  <div id="app">
    <div class="product-image">
      <img :src="image" :alt="altText"/>
    </div>

    <div class="product-info mx-1">
      <h1 class="text-align-left">{{ title }}</h1>
      <p class="text-align-left">{{ description }}</p>
      <div class="text-align-left"><a :href="link" target="_blank">More products like this</a></div>
      <p v-if="inStock" class="text-align-left">In Stock</p>
      <p v-else class="text-align-left">Out of Stock</p>

      <div class="sub-wrapper d-flex flex-col align-items-start">
        <h3 class="text-align-left">Details</h3>
        <ul>
          <li v-for="detail in details" :key="detail">{{ detail }}</li>
        </ul>
      </div>

      <div class="sub-wrapper d-flex flex-col align-items-start sizes">
        <h3 class="text-align-left">Sizes</h3>
        <ul>
          <li v-for="size in sizes" :key="size">{{ size }}</li>
        </ul>
      </div>

      <div class="sub-wrapper d-flex flex-col align-items-start">
        <div v-for="variant in variants" :key="variant.variantId">
          <p @mouseover="updateProduct(variant.variantImage)">{{ variant.variantColor }}</p>
        </div>
      </div>

      <div class="sub-wrapper d-flex flex-row justify-content-space-between">
        <div class="action-buttons d-flex">
          <button
              v-on:click="addToCart"
              :disabled="!inStock"
              :class="{disabledButton: !inStock}"
          >
            Add to cart
          </button>
          <button v-on:click="removeFromCart" class="ml-1">Remove from cart</button>
        </div>

        <div class="cart d-flex justify-content-center align-items-center">
          Cart({{ cart }})
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import ProductPage from './components/ProductPage.vue'

export default {
  name: 'App',
  data() {
    return {
      brand: 'Vue Mastery',
      product: 'Socks',
      description: 'A pair of warm, fuzzy socks',
      altText: 'A pair of socks',
      image: require('./assets/img/socks-gow.jpg'),
      link: 'https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks',
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      sizes:[
        'S', 'M', 'L', 'XL', 'XXL', 'XXXL'
      ],
      cart: 0,
      selectedVariant: 0,
      variants: [
        {
          variantId: 234,
          variantColour: 'green',
          variantImage: require('./assets/img/socks-gow.jpg'),
          variantQuantity: 2
        },
        {
          variantId: 235,
          variantColour: 'blue',
          variantImage: require('./assets/img/socks-bow.jpg'),
          variantQuantity: 5
        }
      ],
      onSale: true
    }
  },
  methods: {
    addToCart: function() {
      this.cart = this.cart + 1;
    },
    removeFromCart: function() {
      this.cart = this.cart > 0 ? this.cart - 1 : 0;
    },
    updateProduct: function(variantImage) {
      this.image = variantImage;
    }
  },
  computed: {
    title() {
      return this.onSale ? `${this.brand} - ${this.product}` : ``;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    }
  }
  // components: {
  //   ProductPage
  // }
}
</script>

<style>
body {
  font-family: tahoma, sans-serif;
  color:#282828;
  margin: 0;
}

.nav-bar {
  background: linear-gradient(-90deg, #84CF6A, #16C0B0);
  height: 60px;
  margin-bottom: 15px;
}

.product {
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 0 2.5rem;
  box-shadow: 0 0.5px 1px #d8d8d8;
}

.product-image,
.product-info {
  margin-top: 10px;
}

.product-image {
  width: 50%;
}

.product-info {
  min-width: 25%;
}

.sub-wrapper {
}

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}

.cart {
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}

button {
  border: none;
  background-color: #1E95EA;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
}

.disabledButton {
  background-color: #d8d8d8;
}

.review-form {
  width: 400px;
  padding: 20px;
  margin: 40px;
  border: 1px solid #d8d8d8;
}

input {
  width: 100%;
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}

.tab {
  margin-left: 20px;
  cursor: pointer;
}

.activeTab {
  color: #16C0B0;
  text-decoration: underline;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
}

.text-align-left {
  text-align: left;
}

.d-flex {
  display: flex;
}

.flex-col {
  flex-direction: column;
}

.flex-row {
  flex-direction: row;
}

.justify-content-start {
  justify-content: flex-start;
}

.justify-content-center {
  justify-content: center;
}

.justify-content-space-between {
  justify-content: space-between;
}

.align-items-start {
  align-items: flex-start;
}

.align-items-center {
  align-items: center;
}

.ml-1 {
  margin-left: 1rem;
}

.my-1 {
  margin: 1rem 0;
}

.mx-1 {
  margin: 0 1rem;
}

.width-100 {
  width: 100%;
}

ul {
  padding: 0 1rem;
}

ul li {
  text-align: left;
}

.text-align-left {
  text-align: left;
}

.disabledButton {
  cursor: not-allowed;
  background-color: #dedede;
  color: black;
}
</style>
