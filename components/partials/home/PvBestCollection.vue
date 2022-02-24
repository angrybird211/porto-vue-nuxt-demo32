<template>
	<section
		class="best-product-section appear-animate"
		data-animation-name="fadeIn"
		data-animation-delay="100"
		v-animate
	>
		<div class="section-title">
			<div class="divide-txt">
				<div class="divide-line"></div>
				<span><strong>Best Seller</strong> Products</span>
				<div class="divide-line"></div>
			</div>
			<h3 class="section-subtitle">Only the best seller products added recently in our catalog</h3>
		</div>

		<pv-carousel
			class="product-panel show-nav-hover mb-0"
			:options="bestSlider"
			v-if="products.length === 0"
		>
			<div
				class="swiper-slide"
				v-for="number in [1,2,3,4]"
				:key="'best-skel-' + number"
			>
				<div class="product-loading-overlay"></div>
			</div>
		</pv-carousel>

		<pv-carousel
			class="product-panel show-nav-hover mb-0"
			:options="bestSlider"
			v-if="products.length > 0"
		>
			<div
				class="swiper-slide"
				v-for="product in products.slice(0,4)"
				:key="'best' + product.name"
			>
				<pv-product-one :product="product">
				</pv-product-one>
			</div>
		</pv-carousel>
	</section>
</template>

<script>
import PvCarousel from '~/components/features/PvCarousel';
import PvProductOne from '~/components/features/product/PvProductOne';
import { bestSlider } from '~/utils/data/carousel';

export default {
	components: {
		PvCarousel,
		PvProductOne
	},
	props: {
		products: Array
	},
	data: function () {
		return {
			bestSlider: bestSlider
		}
	}
}
</script>