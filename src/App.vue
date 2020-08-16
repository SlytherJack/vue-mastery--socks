<template>
  <div id="app">
    <div class="product-image">
      <img :src="image" :alt="altText"/>
    </div>

    <div class="product-info">
      <h1>{{ product }}</h1>
      <p>{{ description }}</p>
      <a :href="link" target="_blank" class="text-align-left">More products like this</a>

      <div v-if="onSale">On Sale</div>

      <p v-if="inStock">In Stock</p>
      <p v-else>Out of Stock</p>

      <div class="sub-wrapper d-flex flex-col align-items-start">
        <h4 class="text-align-left">Details</h4>
        <ul>
          <li v-for="detail in details" :key="detail">{{ detail }}</li>
        </ul>
      </div>

      <div class="sub-wrapper d-flex flex-col align-items-start sizes">
        <h4 class="text-align-left">Sizes</h4>
        <ul>
          <li v-for="size in sizes" :key="size">{{ size }}</li>
        </ul>
      </div>

      <div class="sub-wrapper d-flex flex-col align-items-start">
        <div v-for="variant in variants" :key="variant.variantId">
          <p @mouseover="updateProduct(variant.variantImage)">{{ variant.variantColor }}</p>
        </div>
      </div>

      <div class="sub-wrapper d-flex flex-row">
        <div class="action-buttons d-flex">
          <button v-on:click="addToCart">Add to cart</button>
          <button v-on:click="removeFromCart">Remove from cart</button>
        </div>

        <div class="cart">
          <p>Cart({{ cart }})</p>
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
      product: 'Socks',
      description: 'A pair of warm, fuzzy socks',
      altText: 'A pair of socks',
      image: require('./assets/img/socks-gow.jpg'),
      link: 'https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks',
      inStock: true,
      onSale: true,
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      sizes:[
        'S', 'M', 'L', 'XL', 'XXL', 'XXXL'
      ],
      cart: 0,
      variants: [
        {
          variantId: 234,
          variantColour: 'green',
          variantImage: require('./assets/img/socks-gow.jpg')
        },
        {
          variantId: 235,
          variantColour: 'blue',
          variantImage: require('./assets/img/socks-bow.jpg')
        }
      ]
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
  }
  // components: {
  //   ProductPage
  // }
}
</script>

<style>
body {
  font-family: tahoma;
  color:#282828;
  margin: 0px;
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
  margin: 40px;
  box-shadow: 0px .5px 1px #d8d8d8;
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
  display: flex;
  justify-content: space-between;
  align-items: center;
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

.align-items-start {
  align-items: flex-start;
}

</style>
