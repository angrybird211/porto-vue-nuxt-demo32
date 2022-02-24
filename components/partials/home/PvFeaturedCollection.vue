<template>
	<section
		class="featured-section text-center appear-animate"
		data-animation-name="fadeIn"
		data-animation-delay="100"
		v-animate
	>
		<div class="section-title">
			<div class="divide-txt">
				<div class="divide-line"></div>
				<span><strong>Featured</strong> Products</span>
				<div class="divide-line"></div>
			</div>
			<h3 class="section-subtitle">Amazing products added recently in our catalog</h3>
		</div>

		<div
			class="row text-left product-ajax-grid"
			v-if="products.length === 0"
		>
			<div
				class="col-6 col-md-3"
				v-for="(product,index) in [1,2,3,4]"
				:key="'featured-skel-' + index"
			>
				<div class="product-loading-overlay"></div>
			</div>
		</div>

		<div
			class="row text-left product-ajax-grid"
			v-if="products.length > 0"
		>
			<div
				class="col-6 col-md-3"
				v-for="(product,index) in products.slice(0,4)"
				:key="'featured-' + index"
			>
				<pv-product-one :product="product"></pv-product-one>
			</div>
		</div>
	</section>
</template>

<script>
import PvProductOne from '~/components/features/product/PvProductOne';

export default {
	components: {
		PvProductOne
	},
	props: {
		products: Array
	}
}
</script>