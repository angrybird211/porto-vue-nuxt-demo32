<template>
	<main class="main mb-5">
		<div class="container-fluid skeleton-body">
			<div class="product-single-container product-single-default">
				<div class="row">
					<div class="col-xl-2cols col-lg-3">
						<div
							class="sidebar-overlay"
							@click="hideSidebar"
						></div>
						<div
							class="sidebar-toggle custom-sidebar-toggle"
							@click="showSidebar"
						><i class="fas fa-sliders-h"></i></div>
						<aside
							class="sidebar-shop mobile-sidebar"
							sticky-container
						>
							<pv-sidebar-filter-one
								:category-list="categoryList"
								v-if="categoryList"
							></pv-sidebar-filter-one>

							<div
								class="sidebar-content skeleton-body"
								v-else
							>
								<aside class="widget"></aside>
								<aside class="widget"></aside>
								<aside class="widget"></aside>
							</div>
						</aside>
					</div>

					<div class="col-xl-8cols col-lg-9">
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
									<nuxt-link to="/shop">Shop</nuxt-link>
								</li>
								<li
									class="breadcrumb-item"
									v-if="loaded"
								>
									<nuxt-link
										:to="{path: '/shop', query: {category: category.slug}}"
										v-for="(category, index) in productCategory"
										:key="`product-category-${index}`"
									>{{index === productCategory.length - 1 ? category.name : category.name + ', '}}</nuxt-link>
								</li>
								<li
									class="breadcrumb-item active"
									aria-current="page"
									v-if="loaded"
								>{{product.name}}</li>
							</ol>
						</nav>

						<div
							class="row"
							v-if="product"
						>
							<div class="col-lg-5 col-md-6 product-single-gallery">
								<pv-media-one :product="product"></pv-media-one>
							</div>

							<div class="col-lg-7 col-md-6 product-single-details">
								<pv-detail-two
									:product="product"
									:prev-product="prevProduct"
									:next-product="nextProduct"
								></pv-detail-two>
							</div>
						</div>

						<pv-desc-one
							:product="product"
							v-if="product"
						></pv-desc-one>

						<div
							class="skel-group main-content"
							v-if="!product"
						>
							<div class="summary-before col-lg-5 col-md-6"></div>
							<div class="summary entry-summary col-lg-7 col-md-6"></div>
							<div class="tab-content col-lg-12"></div>
						</div>

						<pv-related-products
							:products="relatedProducts"
							class="mb-1"
						></pv-related-products>
					</div>

					<div class="col-xl-2cols d-none d-xl-block">
						<pv-product-sidebar-three></pv-product-sidebar-three>
					</div>
				</div>
			</div>
		</div>
	</main>
</template>
    
<script>
import { VueTreeList, Tree } from 'vue-tree-list';
import Api, { baseUrl, currentDemo } from '~/api';
import PvSidebarFilterOne from '~/components/partials/shop/sidebar-filter/PvSidebarFilterOne';
import PvMediaOne from '~/components/partials/product/media/PvMediaOne';
import PvDetailTwo from '~/components/partials/product/detail/PvDetailTwo';
import PvDescOne from '~/components/partials/product/description/PvDescOne';
import PvRelatedProducts from '~/components/partials/product/PvRelatedProducts';
import PvSmallCollection from '~/components/partials/product/PvSmallCollection';
import PvProductSidebarThree from '~/components/partials/product/sidebar/PvProductSidebarThree';

export default {
	components: {
		PvMediaOne,
		PvDetailTwo,
		PvDescOne,
		PvRelatedProducts,
		PvSmallCollection,
		PvSidebarFilterOne,
		PvProductSidebarThree
	},
	data: function () {
		return {
			product: null,
			relatedProducts: null,
			featuredProducts: null,
			bestProducts: null,
			latestProducts: null,
			topRatedProducts: null,
			nextProduct: null,
			prevProduct: null,
			baseUrl: baseUrl,
			loaded: false,
			categoryList: [],
			productCategory: [],
			categoryList: []
		};
	},
	created: function () {
		this.getProduct();
		this.getCategoryLists();
	},
	methods: {
		getCategoryLists: function () {
			Api.get( `${ baseUrl }/shop/sidebar-list`, {
				params: { demo: currentDemo }
			} )
				.then( response => {
					this.categoryList = response.data.sidebarList;
				} )
				.catch( error => ( { error: JSON.stringify( error ) } ) );
		},
		getProduct: function () {
			this.loaded = false;

			Api.get( `${ baseUrl }/products/${ this.$route.params.slug }`, {
				params: { demo: currentDemo }
			} )
				.then( response => {
					this.product = response.data.product;
					this.relatedProducts = response.data.relatedProducts;
					this.featuredProducts = response.data.featuredProducts;
					this.bestProducts = response.data.bestSellingProducts;
					this.latestProducts = response.data.latestProducts;
					this.topRatedProducts = response.data.topRatedProducts;
					this.prevProduct = response.data.prevProduct;
					this.nextProduct = response.data.nextProduct;

					this.product.product_categories.map( item => {
						this.productCategory.push( item );
					} );

					this.loaded = true;
				} )
				.catch( error => ( { error: JSON.stringify( error ) } ) );
		},
		hideSidebar: function () {
			document.querySelector( 'body' ).classList.remove( 'sidebar-opened' );
		},
		showSidebar: function () {
			document.querySelector( 'body' ).classList.add( 'sidebar-opened' );
		}
	}
};
</script>