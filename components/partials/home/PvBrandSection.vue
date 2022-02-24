<template>
	<pv-carousel
		class="partners-carousel appear-animate"
		data-animation-name="fadeIn"
		data-animation-delay="100"
		v-animate
		:options="brandSlider"
	>
		<div class="swiper-slide">
			<img
				src="~/static/images/brands/small/brand1.png"
				alt="logo image"
				width="140"
				height="60"
			>
		</div>

		<div class="swiper-slide">
			<img
				src="~/static/images/brands/small/brand2.png"
				alt="logo image"
				width="140"
				height="60"
			>
		</div>

		<div class="swiper-slide">
			<img
				src="~/static/images/brands/small/brand3.png"
				alt="logo image"
				width="140"
				height="60"
			>
		</div>

		<div class="swiper-slide">
			<img
				src="~/static/images/brands/small/brand4.png"
				alt="logo image"
				width="140"
				height="60"
			>
		</div>

		<div class="swiper-slide">
			<img
				src="~/static/images/brands/small/brand5.png"
				alt="logo image"
				width="140"
				height="60"
			>
		</div>

		<div class="swiper-slide">
			<img
				src="~/static/images/brands/small/brand6.png"
				alt="logo image"
				width="140"
				height="60"
			>
		</div>
	</pv-carousel>
</template>

<script>
import PvCarousel from '~/components/features/PvCarousel';
import { brandSlider } from '~/utils/data/carousel';

export default {
	components: {
		PvCarousel
	},
	data: function () {
		return {
			brandSlider: brandSlider
		}
	}
}
</script>