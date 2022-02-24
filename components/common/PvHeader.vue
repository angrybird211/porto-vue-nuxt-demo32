<template>
	<header class="home header header-transparent">
		<div class="header-top d-flex align-items-center">
			<div class="container">
				<div class="header-left mr-lg-0 mr-3 d-sm-flex d-none">
					<h4 class="mb-0">Get 10% OFF at the Porto GIFTs Selection - <a href="javascript:;">Shop Now!</a></h4>
				</div>
				<div class="header-right">
					<ul class="d-lg-flex d-none">
						<li>
							<nuxt-link to="/pages/account">My account</nuxt-link>
						</li>
						<li>
							<nuxt-link to="/pages/wishlist">My Wishlist</nuxt-link>
						</li>
						<li>
							<nuxt-link to="/pages/cart">Cart</nuxt-link>
						</li>
						<li>
							<nuxt-link to="/pages/login">Log In</nuxt-link>
						</li>
					</ul>

					<div class="header-dropdown ">
						<a href="javascript:;">USD</a>
						<div class="header-menu">
							<ul>
								<li><a href="javascript:;">EUR</a></li>
								<li><a href="javascript:;">USD</a></li>
							</ul>
						</div>
					</div>

					<div class="header-dropdown mr-auto mr-sm-3 mr-md-0">
						<a href="javascript:;"><i class="flag-us flag"></i>Eng</a>
						<div class="header-menu">
							<ul>
								<li><a href="javascript:;"><i class="flag-us flag mr-2"></i>Eng</a>
								</li>
								<li><a href="javascript:;"><i class="flag-fr flag mr-2"></i>Fra</a></li>
							</ul>
						</div>
					</div>
				</div>
			</div>
		</div>

		<div class="header-middle sticky-header">
			<div class="container">
				<div class="header-left">
					<button
						class="mobile-menu-toggler"
						type="button"
						@click="showMobileMenu"
					>
						<i class="fas fa-bars"></i>
					</button>

					<nuxt-link
						to="/"
						class="logo"
					>
						<img
							src="~/static/images/logo-black.png"
							width="111"
							height="44"
							alt="Porto Logo"
						/>
					</nuxt-link>
				</div>

				<div class="header-right">
					<pv-header-search></pv-header-search>

					<a
						href="javascript:;"
						class="header-icon header-icon-user"
						title="login"
						@click="openLoginModal"
					><i class="icon-user-2"></i></a>

					<nuxt-link
						to="/pages/wishlist"
						class="header-icon"
					>
						<i class="icon-wishlist-2"></i>
					</nuxt-link>

					<pv-cart-menu></pv-cart-menu>
				</div>
			</div>
		</div>

		<pv-main-menu v-if="isMainMenu"></pv-main-menu>
	</header>
</template>

<script>
import PvMainMenu from '~/components/common/partials/PvMainMenu';
import PvCartMenu from '~/components/common/partials/PvCartMenu';
import PvHeaderSearch from '~/components/common/partials/PvHeaderSearch';

document.querySelector( 'body' ).classList.add( 'loaded' );

export default {
	components: {
		PvMainMenu,
		PvCartMenu,
		PvHeaderSearch
	},
	computed: {
		isMainMenu: function () {
			if ( this.$route.path === '/' ) {
				return true;
			}
			return false;
		}
	},
	methods: {
		openLoginModal: function () {
			this.$modal.show(
				() => import( '~/components/features/modal/PvLoginModal' ),
				{},
				{ width: '525', height: 'auto', adaptive: true }
			);
		},
		showMobileMenu: function () {
			document.querySelector( 'body' ).classList.add( 'mmenu-active' );
		},
		showMobileSearch: function ( e ) {
			let headerSearch = e.currentTarget.closest( '.header-search' );
			headerSearch.classList.add( 'show' );
			headerSearch
				.querySelector( '.header-search-wrapper' )
				.classList.add( 'show' );
		}
	}
};
</script>