<template>
	<main class="main mb-5">
		<div class="container-fluid">
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
					<div class="page-header">
						<div class="container d-flex flex-column align-items-center">
							<nav
								aria-label="breadcrumb"
								class="breadcrumb-nav border-0 mb-1"
							>
								<div class="container">
									<ol class="breadcrumb">
										<li class="breadcrumb-item">
											<nuxt-link to="/">Home</nuxt-link>
										</li>
										<li class="breadcrumb-item">
											<nuxt-link to="/shop">Shop</nuxt-link>
										</li>
										<li
											class="breadcrumb-item active"
											aria-current="page"
										>My Account</li>
									</ol>
								</div>
							</nav>

							<h1>My Account</h1>
						</div>
					</div>

					<div class="container login-container">
						<div class="row">
							<div class="col-lg-10 mx-auto">
								<div class="row">
									<div class="col-md-6">
										<div class="heading mb-1">
											<h2 class="title">Login</h2>
										</div>

										<form action="#">
											<label for="login-email">
												Username or email address
												<span class="required">*</span>
											</label>
											<input
												type="email"
												class="form-input form-wide"
												id="login-email"
												required
											/>

											<label for="login-password">
												Password
												<span class="required">*</span>
											</label>
											<input
												type="password"
												class="form-input form-wide"
												id="login-password"
												required
											/>

											<div class="form-footer">
												<div class="custom-control custom-checkbox mb-0">
													<input
														type="checkbox"
														class="custom-control-input"
														id="lost-password"
													/>
													<label
														class="custom-control-label mb-0"
														for="lost-password"
													>
														Remember
														me
													</label>
												</div>

												<nuxt-link
													to="/pages/forgot-password"
													class="forget-password text-dark form-footer-right"
												>
													Forgot
													Password?
												</nuxt-link>
											</div>
											<button
												type="submit"
												class="btn btn-dark btn-md w-100"
											>LOGIN</button>
										</form>
									</div>
									<div class="col-md-6">
										<div class="heading mb-1">
											<h2 class="title">Register</h2>
										</div>

										<form action="#">
											<label for="register-email">
												Email address
												<span class="required">*</span>
											</label>
											<input
												type="email"
												class="form-input form-wide"
												id="register-email"
												required
											/>

											<label for="register-password">
												Password
												<span class="required">*</span>
											</label>
											<input
												type="password"
												class="form-input form-wide"
												id="register-password"
												required
											/>

											<div class="form-footer mb-2">
												<button
													type="submit"
													class="btn btn-dark btn-md w-100 mr-0"
												>Register</button>
											</div>
										</form>
									</div>
								</div>
							</div>
						</div>
					</div>
				</div>

				<div class="col-xl-2cols col-12">
					<pv-product-sidebar-three></pv-product-sidebar-three>
				</div>

			</div>
		</div>
	</main>
</template>

<script>
import Api, { baseUrl, currentDemo } from '~/api';
import PvSidebarFilterOne from '~/components/partials/shop/sidebar-filter/PvSidebarFilterOne';
import PvProductSidebarThree from '~/components/partials/product/sidebar/PvProductSidebarThree';

export default {
	components: {
		PvSidebarFilterOne,
		PvProductSidebarThree
	},
	data: function () {
		return {
			categoryList: []
		};
	},
	created: function () {
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
		hideSidebar: function () {
			document.querySelector( 'body' ).classList.remove( 'sidebar-opened' );
		},
		showSidebar: function () {
			document.querySelector( 'body' ).classList.add( 'sidebar-opened' );
		}
	}
}
</script>