<template>
	<main class="main skeleton-body">
		<pv-shop-banner></pv-shop-banner>

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
				<li class="breadcrumb-item active">Shop</li>
			</ol>
		</nav>

		<div class="container shop-off-canvas">
			<div class="row mt-2">
				<div
					class="sidebar-overlay"
					@click="hideSidebarFilter"
				></div>
				<aside class="sidebar-shop col-lg-3 order-lg-first mobile-sidebar custom-scrollbar position-fixed">
					<pv-sidebar-filter-three
						:category-list="categoryList"
						:featured-products="featuredProducts"
						:is-sub-menu="false"
						v-if="featuredProducts.length > 0"
					></pv-sidebar-filter-three>

					<div
						class="sidebar-content skeleton-body"
						v-else
					>
						<aside class="widget"></aside>
						<aside class="widget"></aside>
						<aside class="widget"></aside>
					</div>
				</aside>

				<div class="col-lg-12">
					<pv-product-list-one
						:category-list="categoryList"
						:items-per-row="4"
					></pv-product-list-one>
				</div>
			</div>
		</div>

		<div class="mb-4"></div>
	</main>
</template>

<script>
import { VueTreeList, Tree } from 'vue-tree-list';
import PvSidebarFilterThree from '~/components/partials/shop/sidebar-filter/PvSidebarFilterThree';
import PvProductListOne from '~/components/partials/shop/product-list/PvProductListOne';
import PvShopBanner from '~/components/partials/shop/PvShopBanner';
import Api, { baseUrl, currentDemo } from '~/api';

export default {
	components: {
		PvSidebarFilterThree,
		PvProductListOne,
		PvShopBanner
	},
	data: function () {
		return {
			categoryList: [],
			featuredProducts: []
		};
	},
	mounted: function () {
		this.getCategoryLists();
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
		hideSidebarFilter: function () {
			document.querySelector( 'body' ).classList.remove( 'sidebar-opened' );
		}
	}
};
</script>