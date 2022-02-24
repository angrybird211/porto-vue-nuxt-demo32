<template>
	<pv-carousel
		class="top-slider slide-animate show-nav-hover"
		:options="introSlider"
		v-animate
	>
		<div class="swiper-slide">
			<div
				class="home-slide home-slide1"
				v-lazy:background-image="'./images/home/slider/home_slider1.jpg'"
				style="background-position: 60%"
			>
				<div class="slide-content content-left">
					<div
						class="divide-txt mb-0 appear-animate"
						data-animation-name="fadeInUpShorter"
						data-animation-delay="100"
						v-animate
					>
						<span class="font2">New Brown Collection</span>
					</div>
					<h2
						class="appear-animate"
						data-animation-name="fadeInUpShorter"
						data-animation-delay="300"
						v-animate
					>
						Summer Sale</h2>
					<h3
						class="appear-animate"
						data-animation-name="fadeInUpShorter"
						data-animation-delay="500"
						v-animate
					>30%
						OFF</h3>
					<div
						class="image-info-group appear-animate"
						data-animation-name="fadeInUpShorter"
						data-animation-delay="700"
						v-animate
					>
						<h5>STARTING AT <span><sup>$</sup>39<sup>99</sup></span></h5>
						<nuxt-link
							to="/shop"
							class="btn"
						>GET YOURS!</nuxt-link>
					</div>
				</div>
			</div>
		</div>

		<div class="swiper-slide">
			<div
				class="home-slide home-slide2"
				style="background-image: url('./images/home/slider/home_slider2.jpg');"
			>
				<div class="slide-content content-right">
					<div
						class="divide-txt no-txt appear-animate"
						data-animation-name="fadeInUpShorter"
						data-animation-delay="100"
						v-animate
					>
						<div class="divide-line"></div>
					</div>
					<h2
						class="appear-animate"
						data-animation-name="fadeInUpShorter"
						data-animation-delay="300"
						v-animate
					>
						Must Have</h2>
					<h3
						class="appear-animate"
						data-animation-name="fadeInUpShorter"
						data-animation-delay="500"
						v-animate
					>
						SANDALS</h3>
					<div
						class="image-info-group appear-animate"
						data-animation-name="fadeInUpShorter"
						data-animation-delay="700"
						v-animate
					>
						<h5>STARTING AT <span><sup>$</sup>19<sup>99</sup></span></h5>
						<nuxt-link
							to="/shop"
							class="btn"
						>GET YOURS!</nuxt-link>
					</div>
				</div>
			</div>
		</div>
	</pv-carousel>
</template>

<script>
import PvCarousel from '~/components/features/PvCarousel';
import { introSlider } from '~/utils/data/carousel';

export default {
	components: {
		PvCarousel
	},
	data: function () {
		return {
			introSlider: introSlider
		};
	}
};
</script>