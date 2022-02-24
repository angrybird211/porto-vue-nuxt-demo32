<template>
	<section
		class="category-section text-center appear-animate"
		data-animation-name="fadeIn"
		data-animation-delay="100"
		v-animate
	>
		<div class="section-title">
			<div class="divide-txt">
				<div class="divide-line"></div>
				<span><strong>Summer</strong> Collection</span>
				<div class="divide-line"></div>
			</div>
			<h3 class="section-subtitle">Amazing products added recently in our catalog</h3>
		</div>

		<isotope
			class="row grid"
			:options="isotopeOptions"
			:list="[]"
		>
			<div
				class="grid-item col-lg-6"
				key="cat-iso-1"
			>
				<div class="product-category">
					<nuxt-link to="/shop">
						<figure>
							<img
								:src="'./images/home/banners/home-banner1.jpg'"
								width="265"
								height="265"
								alt="Category Banner"
							/>
						</figure>

						<div class="category-content content-right">
							<h3>Sport<br>Shoes</h3>
						</div>
					</nuxt-link>
				</div>
			</div>
			<div
				class="grid-item col-6 col-lg-3 height-x1"
				key="cat-iso-2"
			>
				<div class="product-category">
					<nuxt-link :to="{path: '/shop', query: {category: 'women'}}">
						<figure>
							<img
								:src="'./images/home/banners/banner-dark.jpg'"
								width="265"
								height="265"
								alt="Category Banner"
							/>
						</figure>

						<div class="category-content content-white">
							<h3>For Her</h3>
						</div>
					</nuxt-link>
				</div>
			</div>
			<div
				class="grid-item col-6 col-lg-3 height-x1"
				key="cat-iso-3"
			>
				<div class="product-category">
					<nuxt-link :to="{path: '/shop', query: {category: 'men'}}">
						<figure>
							<img
								:src="'./images/home/products/product-9.jpg'"
								width="265"
								height="265"
								alt="Category Banner"
							/>
						</figure>
					</nuxt-link>
				</div>
			</div>
			<div
				class="grid-item col-6 col-lg-3 height-x1"
				key="cat-iso-4"
			>
				<div class="product-category">
					<nuxt-link to="/shop">
						<figure>
							<img
								:src="'./images/home/banners/banner-dark.jpg'"
								width="265"
								height="265"
								alt="Category Banner"
							/>
						</figure>

						<div class="category-content content-white">
							<h3>For Him</h3>
						</div>
					</nuxt-link>
				</div>
			</div>
			<div
				class="grid-item col-6 col-lg-3 height-x1"
				key="cat-iso-5"
			>
				<div class="product-category">
					<nuxt-link to="/shop">
						<figure>
							<img
								:src="'./images/home/products/product-11.jpg'"
								width="265"
								height="265"
								alt="Category Banner"
							/>
						</figure>
					</nuxt-link>
				</div>
			</div>
			<div
				class="col-1 grid-col-sizer"
				key="cat-iso-sizer"
			></div>
		</isotope>
	</section>
</template>

<script>
import isotope from 'vueisotope';

export default {
	components: {
		isotope
	},
	data: function () {
		return {
			isotopeOptions: {
				itemSelector: 'grid-item',
				layoutMode: 'masonry',
				percentPosition: false,
				masonry: {
					columnWidth: '.grid-col-sizer'
				}
			}
		}
	}
}
</script>