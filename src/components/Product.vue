<template>
  <div id="product" class="product">
    <div class="product-image">
      <img :src="variants[0].variantImage" :alt="altText" class="width-100"/>
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
              @click="addToCart"
              :disabled="!inStock"
              :class="{disabledButton: !inStock}"
          >
            Add to cart
          </button>
          <button @click="removeFromCart" class="ml-1">Remove from cart</button>
        </div>
      </div>

      <div class="sub-wrapper">
        <h2>Reviews</h2>
        <p v-if="!reviews.length">There are no reviews yet.</p>
        <ul>
          <li v-for="review in reviews" :key="review">
            <p>{{ review.name }}</p>
            <p>Rating: {{ review.rating }}</p>
            <p>{{ review.review }}</p>
          </li>
        </ul>
      </div>

      <product-review @review-submitted="addReview"></product-review>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Product',
  props: ['premium'],
	data() {
		return {
			brand: 'Vue Mastery',
			product: 'Socks',
			description: 'A pair of warm, fuzzy socks',
			altText: 'A pair of socks',
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
					variantImage: require('../assets/img/socks-gow.jpg'),
					variantQuantity: 2
				},
				{
					variantId: 235,
					variantColour: 'blue',
					variantImage: require('../assets/img/socks-bow.jpg'),
					variantQuantity: 5
				}
			],
      onSale: true,
      reviews: []
		}
	},
	methods: {
    addReview(productReview) {
      this.reviews.push(productReview)
    },
		addToCart: function() {
      this.$emit('add-to-cart',
      this.variants[this.selectedVariant].variantId,
      this.variants[this.selectedVariant].variantQuantity
      );
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
  },
  components : {}
}
</script>

<style>
button {
  border: none;
  background-color: #1E95EA;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
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

.product {
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
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

ul {
  padding: 0 1rem;
}

ul li {
  text-align: left;
}
</style>
