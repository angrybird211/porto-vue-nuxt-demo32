<template>
	<div
		class="home-slide banner-cat d-flex align-items-center"
		:style="{'background-image': `url(./images/home/banners/category_banner.jpg)`}"
	>
		<div class="slide-content">
			<div class="content-left">
				<div class="divide-txt">
					<span class="font2 ls-0">New Brown Collection</span>
					<div class="divide-line"></div>
				</div>
				<h2>Summer Sale</h2>
				<h3 class="ls-0">30% OFF</h3>
			</div>
			<div class="image-info-group">
				<nuxt-link
					to="/shop"
					class="btn mt-0"
				>GET YOURS!</nuxt-link>
			</div>
		</div>
	</div>
</template>