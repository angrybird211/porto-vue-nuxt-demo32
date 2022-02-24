<template>
	<main class="main skeleton-body">
		<div class="container-fluid">
			<div class="row">
				<div class="col-xl-2cols col-lg-3">
					<div
						class="sidebar-overlay"
						@click="hideSidebar"
					></div>
					<aside
						class="sidebar-shop mobile-sidebar"
						sticky-container
					>
						<div
							v-sticky="isSticky"
							sticky-offset="{top: 75}"
						>
							<pv-sidebar-filter-four
								:category-list="categoryList"
								:featured-products="featuredProducts"
								v-if="featuredProducts.length > 0"
							></pv-sidebar-filter-four>

							<div
								class="sidebar-content skeleton-body"
								v-if="featuredProducts.length === 0"
							>
								<aside class="widget"></aside>
								<aside class="widget"></aside>
								<aside class="widget"></aside>
							</div>
						</div>
					</aside>
				</div>

				<div class="col-xl-8cols col-lg-6 col-md-8">
					<nav
						aria-label="breadcrumb"
						class="breadcrumb-nav"
					>
						<ol class="breadcrumb">
							<li class="breadcrumb-item">
								<nuxt-link to="/">
									Home
								</nuxt-link>
							</li>
							<li class="breadcrumb-item">
								<nuxt-link :to="{ path: '/shop/boxed-slider', query: {'category': 'Men'} }">Shop</nuxt-link>
							</li>
							<li
								class="breadcrumb-item active"
								aria-current="page"
							>Boxed Slider</li>
						</ol>
					</nav>

					<pv-carousel
						class="boxed-slider mb-2"
						:options="baseSlider6"
					>
						<div
							class="home-slide banner-cat d-flex align-items-center swiper-slide"
							:style="{'background-image': `url(./images/home/banners/category_banner.jpg)`}"
						>
							<div class="slide-content">
								<div class="content-left">
									<div class="divide-txt">
										<span class="font2 ls-0">New Brown Collection</span>
										<div class="divide-line"></div>
									</div>
									<h2>Summer Sale</h2>
									<h3 class="ls-0">30% OFF</h3>
								</div>
								<div class="image-info-group">
									<nuxt-link
										to="/shop"
										class="btn mt-0"
									>GET YOURS!</nuxt-link>
								</div>
							</div>
						</div>
					</pv-carousel>

					<pv-product-list-one :category-list="categoryList"></pv-product-list-one>
				</div>

				<div class="col-xl-2cols col-lg-3 col-md-4">
					<pv-product-sidebar-three></pv-product-sidebar-three>
				</div>
			</div>

			<div class="mb-4"></div>
		</div>
	</main>
</template>

<script>
import { VueTreeList, Tree } from 'vue-tree-list';
import Sticky from 'vue-sticky-directive';
import PvCarousel from '~/components/features/PvCarousel';
import PvSidebarFilterFour from '~/components/partials/shop/sidebar-filter/PvSidebarFilterFour';
import PvProductSidebarThree from '~/components/partials/product/sidebar/PvProductSidebarThree';
import PvProductListOne from '~/components/partials/shop/product-list/PvProductListOne';
import Api, { baseUrl, currentDemo } from '~/api';
import { baseSlider6 } from '~/utils/data/carousel';

export default {
	directives: {
		Sticky
	},
	components: {
		PvSidebarFilterFour,
		PvProductListOne,
		PvCarousel,
		PvProductSidebarThree
	},
	data: function () {
		return {
			categoryList: [],
			featuredProducts: [],
			baseSlider6: baseSlider6,
			isSticky: false
		};
	},
	mounted: function () {
		this.getCategoryLists();
		this.resizeHandler();
		window.addEventListener( 'resize', this.resizeHandler, {
			passive: true
		} );
	},
	destroyed: function () {
		window.removeEventListener( 'resize', this.resizeHandler );
	},
	methods: {
		getCategoryLists: function () {
			Api.get( `${ baseUrl }/shop/sidebar-list`, {
				params: { demo: currentDemo }
			} )
				.then( response => {
					this.categoryList = response.data.sidebarList;
					this.featuredProducts = response.data.featuredProducts;
				} )
				.catch( error => ( { error: JSON.stringify( error ) } ) );
		},
		resizeHandler: function () {
			this.isSticky = window.innerWidth > 991 ? true : false;
		},
		hideSidebar: function () {
			document.querySelector( 'body' ).classList.remove( 'sidebar-opened' );
		}
	}
};
</script>