<template>
	<div id="product-tabs" class="product-tabs">
		<div class="tabs-wrapper">
			<span
				class="tab"
				:class="{ active: selectedTab === tab }"
				v-for="(tab, index) in tabs"
				:key="index"
				@click="onTabClicked(tab)"
			>
				{{ tab }}
			</span>
		</div>

		<!-- Reviews -->
		<div v-if="selectedTab === tabs[0]" class='product-reviews'>
			<p
				v-if='!reviews.length'
				class="text-align-left"
			>
				There are no reviews yet.
			</p>

			<!-- List of reviews -->
			<ul v-else>
				<li v-for='review in reviews' :key='review'>
				<p>{{ review.name }}</p>
				<p>Rating: {{ review.rating }}</p>
				<p>{{ review.review }}</p>
				</li>
			</ul>
		</div>

		<!-- Make a review -->
		<product-review v-else></product-review>
	</div>
</template>

<script>
	import ProductReview from './ProductReview';

	export default {
		name: 'ProductTabs',
		props: {
			reviews: {
				type: Array,
				required: false
			}
		},
		data() {
			return {
				tabs: ['Reviews', 'Make a Review'],
				selectedTab: 'Reviews'
			}
		},
		methods: {
			onTabClicked (tab) {
				this.selectedTab = tab;
			},
			addReview () {

			}
		},
		computed: {
		},
		components: {
			ProductReview
		}
	}
</script>

<style>
	.product-tabs {
		display: flex;
		flex-direction: column;
		margin: 1rem 0;
	}

	.tabs-wrapper {
		display: flex;
	}

	.tab {
		background-color: white;
		color: black;
		padding: 1rem;
		cursor: pointer;
		transition: all 300ms ease;
	}

	.tab.active {
		background-color: #1e95ea;
		color: white;
	}
</style>
