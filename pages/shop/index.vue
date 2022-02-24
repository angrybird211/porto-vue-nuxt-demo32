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
					</aside>
				</div>

				<div class="col-xl-8cols col-lg-6 col-md-8">
					<div class="container p-0">
						<nav
							aria-label="breadcrumb"
							class="breadcrumb-nav"
						>
							<div class="container">
								<ol class="breadcrumb">
									<li class="breadcrumb-item">
										<nuxt-link to="/">
											Home
										</nuxt-link>
									</li>
									<li class="breadcrumb-item">
										<nuxt-link :to="{ path: '/shop/boxed-image', query: {'category': 'Men'} }">Men</nuxt-link>
									</li>
									<li
										class="breadcrumb-item active"
										aria-current="page"
									>Accessories</li>
								</ol>
							</div>
						</nav>

						<pv-shop-banner class="mb-3"></pv-shop-banner>

						<pv-product-list-one :category-list="categoryList"></pv-product-list-one>
					</div>
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
import PvProductListOne from '~/components/partials/shop/product-list/PvProductListOne';
import PvProductSidebarThree from '~/components/partials/product/sidebar/PvProductSidebarThree';
import PvShopBanner from '~/components/partials/shop/PvShopBanner';
import Api, { baseUrl, currentDemo } from '~/api';
import { baseSlider6 } from '~/utils/data/carousel';

export default {
	directives: {
		Sticky
	},
	components: {
		PvSidebarFilterFour,
		PvProductListOne,
		PvProductSidebarThree,
		PvShopBanner
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