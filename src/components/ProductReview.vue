<template>
	<div id="product-review" class="product-review">
		<form class="review-form" @submit.prevent="onSubmit">
			<div class="form-input-wrapper">
				<label class="text-align-left" for="name">Name:</label>
				<input id="name" v-model="name" placeholder="name">
			</div>

			<div class="form-input-wrapper">
				<label class="text-align-left" for="review">Review:</label>
				<textarea id="review" v-model="review"></textarea>
			</div>

			<div class="form-input-wrapper">
				<label class="text-align-left" for="rating">Rating:</label>
				<select id="rating" v-model.number="rating">
					<option>5</option>
					<option>4</option>
					<option>3</option>
					<option>2</option>
					<option>1</option>
				</select>
			</div>

			<div class="form-input-wrapper">
				<strong class="my-1">Would you like to recommend this product?</strong>
				<div class="radio-group d-flex flex-col">
					<div class="radio-btn">
						<input class="m-0" type="radio" id="yes" name="recommendation" value="yes">
						<label class="mx-1" for="yes">Yes</label>
					</div>

					<div class="radio-btn">
						<input class="m-0" type="radio" id="no" name="recommendation" value="no">
						<label class="mx-1" for="no">No</label>
					</div>
				</div>
			</div>

			<!-- Errors -->
			<div v-if="errors.length">
				<b>Please correct the following error(s):</b>
				<ul>
					<li v-for="error in errors" :key="error">{{ error }}</li>
				</ul>
			</div>

			<button type="submit" class="submit-btn">Submit</button>
		</form>
	</div>
</template>

<script>
	export default {
		name: 'ProductReview',
		props: [],
		data() {
			return {
				name: '',
				review: '',
				rating: 0,
				errors: []
			}
		},
		methods: {
			onSubmit() {
				if(this.name && this.review && this.rating) {
					let productReview = {
						name: this.name,
						review: this.review,
						rating: this.rating,
						recommend: this.recommend,
					};
					this.$emit('review-submitted', productReview);
					this.name = null;
					this.review = null;
					this.rating = null;
					this.recommend = null;
				} else {
					if(!this.name) this.errors.push("Name required.");
					if(!this.review) this.errors.push("Review required.");
					if(!this.rating) this.errors.push("Rating required.");
					if(!this.recommend) this.errors.push("Recommendation required.");
				}
			}
		},
		computed: {
		}
	}
</script>

<style>
	.product-review {
		border: none !important;
	}

	.review-form {
		margin: 0 !important;
		display: flex;
		flex-direction: column;
	}

	.form-input-wrapper {
		display: flex;
		flex-direction: column;
		margin: 1rem 0;
	}

	.radio-btn {
		display: flex;
		align-items: center;
		padding: 0.5rem 0;
	}

	.radio-btn label {
		margin-top: 0.125rem;
	}

	.submit-btn {
		margin-top: 2rem;
	}
</style>
