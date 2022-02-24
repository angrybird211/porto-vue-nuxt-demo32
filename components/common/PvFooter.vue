<template>
	<footer class="footer">
		<div class="footer-top bg-dark">
			<div class="container d-flex align-items-center justify-content-between flex-wrap">
				<div class="widget-newsletter pl-3 d-md-flex align-items-center">
					<div class="widget-newsletter-info">
						<h5 class="widget-newsletter-title text-uppercase m-b-1 text-white">SIGN UP TO NEWSLETTER
						</h5>
						<p class="widget-newsletter-content font2 mb-0">Get all the latest information..</p>
					</div>
					<form
						action="#"
						class="mb-0"
					>
						<div class="footer-submit-wrapper d-flex  mt-2 mb-1 mt-md-0 mb-md-0">
							<input
								type="email"
								class="form-control bg-dark"
								placeholder="Enter your e-mail address"
								size="40"
								required
							>
							<button
								type="submit"
								class="btn btn-dark btn-sm"
							>Submit</button>
						</div>
					</form>
				</div>
			</div>

			<div class="porto-content-box">
				<h4>20$ OFF</h4>
				<h3>GOPORTO</h3>
				<span>USE COUPONS</span>

				<a
					href="javascript:;"
					class="box-close"
					@click="removeContentBox($event)"
				>×</a>
			</div>
		</div>

		<div class="container">
			<div class="footer-middle">
				<div class="row">
					<div class="col-lg-4">
						<div class="info-box info-box-icon-left text-white justify-content-start">
							<i class="icon-shipping"></i>

							<div class="info-box-content">
								<h4>FREE SHIPPING &amp; RETURN</h4>
								<p class="font2">Free shipping on all orders over $99.</p>
							</div>
						</div>

						<div class="info-box info-box-icon-left text-white justify-content-start">
							<i class="icon-money"></i>

							<div class="info-box-content">
								<h4>MONEY BACK GUARANTEE</h4>
								<p class="font2">100% money back guarantee</p>
							</div>
						</div>

						<div class="info-box info-box-icon-left text-white justify-content-start">
							<i class="icon-support"></i>

							<div class="info-box-content">
								<h4>LIVE SUPPORT</h4>
								<p class="font2">Lorem ipsum dolor sit amet.</p>
							</div>
						</div>
					</div>

					<div class="col-md-6 col-lg-2">
						<div class="widget">
							<h3 class="widget-title">Account</h3>
							<div class="widget-content">
								<ul>
									<li>
										<nuxt-link to="/pages/account">My Account</nuxt-link>
									</li>
									<li><a href="javascript:;">Track Your Order</a></li>
									<li><a href="javascript:;">Payment Methods</a></li>
									<li><a href="javascript:;">Shipping Guide</a></li>
									<li><a href="javascript:;">FAQs</a></li>
									<li><a href="javascript:;">Product Support</a></li>
									<li><a href="javascript:;">Privacy</a></li>
								</ul>
							</div>
						</div>
					</div>

					<div class="col-md-6 col-lg-3">
						<div class="widget">
							<h3 class="widget-title">About</h3>
							<div class="widget-content">
								<ul>
									<li>
										<nuxt-link to="/pages/about-us">About Porto</nuxt-link>
									</li>
									<li><a href="javascript:;">Our Guarantees</a></li>
									<li><a href="javascript:;">Terms And Conditions</a></li>
									<li><a href="javascript:;">Privacy Policy</a></li>
									<li><a href="javascript:;">Return Policy</a></li>
									<li><a href="javascript:;">Intellectual Property Claims</a></li>
									<li><a href="javascript:;">Site Map</a></li>
								</ul>
							</div>
						</div>
					</div>

					<div class="col-lg-3">
						<div class="widget-group">
							<div class="widget mb-3">
								<h3 class="widget-title">Follow Us</h3>
								<div class="widget-content">
									<div class="social-icons ml-1">
										<a
											href="javascript:;"
											class="social-icon social-facebook"
											
											title="Facebook"
										>
											<i class="icon-facebook"></i>
										</a>
										<a
											href="javascript:;"
											class="social-icon social-twitter"
											
											title="Twitter"
										>
											<i class="icon-twitter"></i>
										</a>
										<a
											href="javascript:;"
											class="social-icon social-instagram"
											
											title="instagram"
										>
											<i class="icon-instagram"></i>
										</a>

										<a
											href="javascript:;"
											class="social-icon social-linkedin"
											
											title="Linkedin"
										>
											<i class="fab fa-linkedin-in"></i>
										</a>
									</div>
								</div>
							</div>

							<div class="widget">
								<h3 class="widget-title">Payment Methods</h3>
								<div class="widget-content">
									<img
										src="~/static/images/home/payments_long.png"
										alt="payment image"
										width="201"
										height="31"
									>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>

			<div class="footer-bottom flex-column flex-sm-row">
				<p>Porto eCommerce. © 2021. All Rights Reserved</p>
				<ul>
					<li><a href="javascript:;">Affiliates</a></li>
					<li><a href="javascript:;">Privacy Policy</a></li>
					<li><a href="javascript:;">Terms & Conditions</a></li>
				</ul>
			</div>
		</div>
	</footer>
</template>

<script>
export default {
	methods: {
		removeContentBox: function ( e ) {
			e.currentTarget.parentNode.remove();
		}
	}
}
</script>