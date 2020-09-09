<template>
  <div id="app">
    <div class="cart d-flex justify-content-center align-items-center">
      Cart({{ cart.length }})
    </div>
    <Product :premium="premium" @add-to-cart="updateCart"></Product>
  </div>
</template>

<script>
import Product from './components/Product';

export default {
	name: 'App',
	data() {
		return {
			premium: true,
			cart: []
		}
	},
	methods: {
		updateCart(...args) {
		const [id, totalQuantity] = args;
		const quanntityInCart = this.cart.filter(productID => productID === id);

		if (quanntityInCart.length < totalQuantity) {
		this.cart.push(id);
		}
	}
	},
	components: {
		Product
	}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  position: relative;
}

body {
  font-family: tahoma, sans-serif;
  color:#282828;
  margin: 0;
}

.cart {
  position: absolute;
  top: 2.5rem;
  right: 2.5rem;
}

.nav-bar {
  background: linear-gradient(-90deg, #84CF6A, #16C0B0);
  height: 60px;
  margin-bottom: 15px;
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

.m-0 {
	margin: 0 !important;
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

.text-align-left {
  text-align: left;
}

.disabledButton {
  cursor: not-allowed;
  background-color: #dedede;
  color: black;
}
</style>
