<template>
	<main class="main home-page">
		<pv-intro-section></pv-intro-section>

		<pv-service-section></pv-service-section>

		<div class="container">
			<pv-featured-collection :products="featuredProducts"></pv-featured-collection>

			<pv-category-section></pv-category-section>

			<pv-best-collection :products="bestProducts"></pv-best-collection>

			<pv-brand-section></pv-brand-section>
		</div>
	</main>
</template>

<script>
import PvIntroSection from '~/components/partials/home/PvIntroSection';
import PvServiceSection from '~/components/partials/home/PvServiceSection';
import PvFeaturedCollection from '~/components/partials/home/PvFeaturedCollection';
import PvCategorySection from '~/components/partials/home/PvCategorySection';
import PvBrandSection from '~/components/partials/home/PvBrandSection';
import PvBestCollection from '~/components/partials/home/PvBestCollection';

import {
	getProductsByAttri,
	getTopSellingProducts,
	getTopRatedProducts
} from '~/utils/service';
import { getCookie } from '~/utils';
import Api, { baseUrl } from '~/api';

export default {
	components: {
		PvIntroSection,
		PvServiceSection,
		PvFeaturedCollection,
		PvCategorySection,
		PvBrandSection,
		PvBestCollection
	},
	data: function () {
		return {
			products: [],
			posts: [],
			featuredProducts: [],
			newProducts: [],
			bestProducts: [],
			topRatedProducts: [],
			timerId: 0
		};
	},
	mounted: function () {
		document.querySelector( 'body' ).classList.add( 'home-page' );

		Api.get( `${ baseUrl }/demo32` )
			.then( response => {
				this.products = response.data.products;
				this.posts = response.data.posts;
				this.featuredProducts = getProductsByAttri(
					response.data.products
				);
				this.newProducts = getProductsByAttri(
					response.data.products,
					'is_new'
				);
				this.bestProducts = getTopSellingProducts(
					response.data.products
				);
				this.topRatedProducts = getTopRatedProducts(
					response.data.products
				);
			} )
			.catch( error => ( { error: JSON.stringify( error ) } ) );

		this.timerId = setTimeout( () => {
			if (
				this.$route.path === '/' &&
				getCookie( 'newsletter' ) !== 'false'
			) {
				this.$modal.show(
					() =>
						import( '~/components/features/modal/PvNewsletterModal' ),
					{},
					{ width: '740', height: 'auto', adaptive: true, class: 'newsletter-modal' }
				);
			}
		}, 10000 );
	},
	destroyed: function () {
		document.querySelector( 'body' ).classList.remove( 'home-page' );
		clearTimeout( this.timerId );
	}
};
</script>