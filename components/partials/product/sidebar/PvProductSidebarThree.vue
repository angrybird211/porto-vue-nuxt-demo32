<template>
	<aside class="sidebar-product d-block sidebar-common">
		<div
			class="sidebar-wrapper"
			data-start-top="100"
			data-offset-top="56"
			v-sticky
		>
			<div class="widget">
				<h3 class="widget-title">
					<a
						data-toggle="collapse"
						href="javascript:;"
						role="button"
						aria-expanded="true"
						aria-controls="widget-body-8"
					>Custom HTML Block</a>
				</h3>

				<div
					class="collapse show"
					id="widget-body-8"
				>
					<div class="widget-body">
						<h4 class="widget-subtitle">This is a custom sub-title.</h4>

						<p class="mb-4 ls-0">Lorem ipsum dolor sit amet, con sec tetur elitad.</p>
					</div>
				</div>
			</div>

			<div class="widget widget-banner pb-2">
				<div class="product-category">
					<nuxt-link to="/shop">
						<figure>
							<img
								src="~/static/images/home/banners/banner-sidebar.jpg"
								width="266"
								height="266"
								alt="Banner"
							/>
						</figure>

						<div class="category-content content-right p-0">
							<h3>Sport<br>Shoes</h3>
						</div>
					</nuxt-link>
				</div>
			</div>
		</div>
	</aside>
</template>