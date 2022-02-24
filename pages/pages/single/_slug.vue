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
									<nuxt-link to="/pages/blog">Blog</nuxt-link>
								</li>
								<li
									class="breadcrumb-item"
									v-if="loaded"
								>
									<nuxt-link
										:to="{path: '/pages/blog', query: {category: category.slug}}"
										v-for="(category, index) in blogCategory"
										:key="`blog-category-${index}`"
									>{{index === blogCategory.length - 1 ? category.Name : category.Name + ', '}}</nuxt-link>
								</li>
								<li
									class="breadcrumb-item active"
									aria-current="page"
									v-if="loaded"
								>{{post.title}}</li>
							</ol>
						</div>
					</nav>

					<div class="container">
						<div class="row">
							<div class="col-lg-9">
								<template v-if="!loaded">
									<div class="skeleton-body">
										<div class="post"></div>
										<div class="reply"></div>
									</div>
								</template>

								<template v-else>
									<pv-post-two
										:post="post"
										:ad-class="'zoom-effect'"
									></pv-post-two>

									<hr class="mt-2 mb-1" />
								</template>

								<pv-related-posts :posts="relatedPosts"></pv-related-posts>
							</div>

							<div
								class="custom-sidebar-toggle"
								@click="toggleSidebar"
								v-if="isSidebar"
							>
								<i class="fas fa-sliders-h"></i>
							</div>
							<div
								class="sidebar-overlay"
								@click="toggleSidebar"
							></div>

							<pv-blog-sidebar
								:blog-category-list="blogCategoryList"
								:recent-posts="recentPosts"
								:loaded="loaded"
							></pv-blog-sidebar>
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
import PvBlogSidebar from '~/components/partials/page/PvBlogSidebar';
import PvPostTwo from '~/components/features/post/PvPostTwo';
import PvRelatedPosts from '~/components/partials/page/PvRelatedPosts';
import PvSidebarFilterOne from '~/components/partials/shop/sidebar-filter/PvSidebarFilterOne';
import PvProductSidebarThree from '~/components/partials/product/sidebar/PvProductSidebarThree';

export default {
	components: {
		PvBlogSidebar,
		PvPostTwo,
		PvRelatedPosts,
		PvSidebarFilterOne,
		PvProductSidebarThree
	},
	data: function () {
		return {
			baseUrl: baseUrl,
			post: null,
			relatedPosts: null,
			recentPosts: null,
			blogCategory: [],
			blogCategoryList: null,
			isSidebar: false,
			loaded: false,
			categoryList: []
		};
	},
	created: function () {
		this.getBlog();
		this.getCategoryLists();
	},
	mounted: function () {
		this.resizeHandler();
		window.addEventListener( 'resize', this.resizeHandler, {
			passive: true
		} );
	},
	destroyed: function () {
		window.removeEventListener( 'resize', this.resizeHandler );
	},
	methods: {
		getBlog: function () {
			this.loaded = false;

			Api.get( `${ baseUrl }/single/${ this.$route.params.slug }`, {
				params: { demo: currentDemo }
			} )
				.then( response => {
					this.post = response.data.post;
					this.recentPosts = response.data.recentPosts;
					this.blogCategoryList = response.data.blogCategoryList;
					this.relatedPosts = response.data.relatedPosts;

					this.post.blog_categories.map( item => {
						this.blogCategory.push( item );
					} );

					this.loaded = true;
				} )
				.catch( error => ( { error: JSON.stringify( error ) } ) );
		},
		toggleSidebar: function () {
			let body = document.querySelector( 'body' );
			if ( body.classList.contains( 'sidebar-opened' ) ) {
				body.classList.remove( 'sidebar-opened' );
			} else {
				body.classList.add( 'sidebar-opened' );
			}
		},
		resizeHandler: function () {
			this.isSidebar = window.innerWidth > 991 ? false : true;
		},
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
};
</script>