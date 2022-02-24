<template>
	<main class="main skeleton-body">
		<pv-shop-banner></pv-shop-banner>

		<div class="container">
			<nav
				aria-label="breadcrumb"
				class="breadcrumb-nav border-bottom-0"
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

			<div class="row">
				<div class="col-12">
					<pv-product-list-two></pv-product-list-two>
				</div>
			</div>
		</div>

		<div class="mb-4"></div>
	</main>
</template>

<script>
import { VueTreeList, Tree } from 'vue-tree-list';
import PvSidebarFilterFour from '~/components/partials/shop/sidebar-filter/PvSidebarFilterFour';
import PvProductListTwo from '~/components/partials/shop/product-list/PvProductListTwo';
import PvShopBanner from '~/components/partials/shop/PvShopBanner';
import Api, { baseUrl, currentDemo } from '~/api';

export default {
	components: {
		PvSidebarFilterFour,
		PvProductListTwo,
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
		}
	}
};
</script>