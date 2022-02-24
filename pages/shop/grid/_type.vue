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

		<div class="container-fluid">
			<div class="row">
				<!-- <div :class="itemCountsPerRow[cols] > 4 ? 'col-xl-8cols col-lg-6 col-md-8 main-content' : 'col-xl-8cols col-lg-6 col-md-8 main-content'">
					<pv-product-list-one
						:category-list="categoryList"
						:items-per-row="itemCountsPerRow[cols]"
					></pv-product-list-one>
				</div> -->

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
								v-else
							>
								<aside class="widget"></aside>
								<aside class="widget"></aside>
								<aside class="widget"></aside>
							</div>
						</div>
					</aside>
				</div>

				<div :class="itemCountsPerRow[cols] > 4 ? 'col-xl-9cols col-lg-9 main-content' : 'col-xl-8cols col-lg-6 col-md-8 main-content'">
					<pv-product-list-one
						:category-list="categoryList"
						:items-per-row="itemCountsPerRow[cols]"
					></pv-product-list-one>
				</div>

				<div
					class="col-xl-2cols col-lg-3 col-md-4"
					:class="{'d-lg-none': itemCountsPerRow[cols] > 4}"
				>
					<pv-product-sidebar-three></pv-product-sidebar-three>
				</div>
			</div>
		</div>

		<div class="mb-4"></div>
	</main>
</template>

<script>
import { VueTreeList, Tree } from 'vue-tree-list';
import Sticky from 'vue-sticky-directive';
import PvSidebarFilterFour from '~/components/partials/shop/sidebar-filter/PvSidebarFilterFour';
import PvProductListOne from '~/components/partials/shop/product-list/PvProductListOne';
import PvProductSidebarThree from '~/components/partials/product/sidebar/PvProductSidebarThree';
import PvShopBanner from '~/components/partials/shop/PvShopBanner';
import Api, { baseUrl, currentDemo } from '~/api';

export default {
	components: {
		PvSidebarFilterFour,
		PvProductListOne,
		PvShopBanner,
		PvProductSidebarThree
	},
	directives: {
		Sticky
	},
	data: function () {
		return {
			categoryList: [],
			featuredProducts: [],
			itemCountsPerRow: {
				'3cols': 3,
				'4cols': 4,
				'5cols': 5,
				'6cols': 6,
				'7cols': 7,
				'8cols': 8
			},
			cols: '3cols',
			isSticky: false
		};
	},
	mounted: function () {
		this.cols = this.$route.params.type;
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