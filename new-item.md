## Latest items ထည့်သွင်းခြင်း
1. Admin Panel ကနေ **Contents** > **Blocks** အောက်မှာ **新着商品** ဆိုတဲ့ Block ကို ပြင်ပါမယ်။ *(EC-Cube က default ပါတဲ့ block တွေကိုမထိချင်ဘူးဆို Block အသစ်လုပ်နိုင်ပါတယ်။)*
2. ရှိပြီးသား code တွေကို ရှင်းပြီး အောက်ပါကုဒ်ကိုထည့်လိုက်ပါ။
	```Twig
	{%
	set query = repository('Eccube\\Entity\\Product')
					.createQueryBuilder('p')
					.where('p.Status = 1')
					.orderBy('p.update_date', 'DESC')
					.setMaxResults(20)
					.getQuery()
	%}
	{% set latest_products = query.getResult() %}
	{% set count = latest_products|length %}
	{% if count == 0  %}
		{% set count = 1 %}
	{% endif %}
	{% if count > 6  %}
		{% set count = 5 %}
	{% endif %}

	{% block stylesheet %}
		<style>
			.new_products .main_slick{
				width: 100%;
				margin: 0 auto;
				max-width: 1130px;
				padding: 0 30px;
			}
			#new_products_slick{
				width: 95%;
				margin: 0 auto;
			}
			.slick-prev,
			.slick-next{
				font-size: 0;
				line-height: 0;
				position: absolute;
				top: 32%;
				display: block;
				width: 25px;
				height: 25px;
				padding: 0;
				-webkit-transform: translate(0, -50%);
				-ms-transform: translate(0, -50%);
				transform: translate(0, -50%);
				cursor: pointer;
				color: transparent;
				background: transparent;
				border: 1px solid transparent;
				outline: 1px solid transparent;
				background: 1px solid green;
				background: #6f6f6f;
				border-radius: 50%;
			}
			.slick-prev{
				left: -25px;
			}
			.slick-next{
				right: -25px;
			}
			.slick-prev::before {
				content: "";
				display: block;
				border-bottom: 3px solid;
				border-bottom-color: currentcolor;
				border-left: 3px solid;
				border-left-color: currentcolor;
				transform: rotate(45deg);
				width: 10px;
				height: 10px;
				border-color: #fff;
				position: absolute top: 50%;
				margin: 8px;
			}
			.slick-next::after {
				content: "";
				display: block;
				border-bottom: 3px solid;
				border-bottom-color: currentcolor;
				border-left: 3px solid;
				border-left-color: currentcolor;
				transform: rotate(-135deg);
				width: 10px;
				height: 10px;
				border-color: #fff;
				position: absolute top: 50%;
				margin: 6px;
			}
			.slick-slider {
				margin-bottom: 30px;
			}

			.slick-dots {
				position: absolute;
				bottom: -45px;
				display: block;
				width: 100%;
				padding: 0;
				list-style: none;
				text-align: center;
			}

			.slick-dots li {
				position: relative;
				display: inline-block;
				width: 20px;
				height: 20px;
				margin: 0 5px;
				padding: 0;
				cursor: pointer;
			}

			.slick-dots li button {
				font-size: 0;
				line-height: 0;
				display: block;
				width: 20px;
				height: 20px;
				padding: 5px;
				cursor: pointer;
				color: transparent;
				border: 0;
				outline: none;
				background: transparent;
			}

			.slick-dots li button:hover,
			.slick-dots li button:focus {
				outline: none;
			}

			.slick-dots li button:hover:before,
			.slick-dots li button:focus:before {
				opacity: 1;
			}

			.slick-dots li button:before {
				content: " ";
				line-height: 20px;
				position: absolute;
				top: 0;
				left: 0;
				width: 12px;
				height: 12px;
				text-align: center;
				opacity: .25;
				background-color: black;
				border-radius: 50%;

			}

			.slick-dots li.slick-active button:before {
				opacity: .75;
				background-color: black;
			}

			.slick-dots li button.thumbnail img {
				width: 0;
				height: 0;
			}
			.ec-newItemRole .ec-newItemRole__listItem:nth-child(even),
			.ec-newItemRole .ec-newItemRole__listItem:nth-child(odd){
				margin: 0 10px;
			}
			.online_subtitle {
				font-size: 132%;
				padding-bottom: 5px;
				border-bottom: 1px solid #150532;
				margin-bottom: 30px;
			}
			.online_subtitle .all {
				display: inline-block;
				font-size: 76%;
				float: right;
				color: #000;
			}
			.ec-newItemRole .ec-newItemRole__listItemPrice{
				color: red;
			}
			@media only screen and (max-width: 767px){
				.slick-prev{
					left: -25px;
				}
				.slick-next{
					right: -25px;
				}
			
		</style>
	{% endblock %}

	{% block javascript %}
		<script>
			$(function() {
				$('#new_products_slick').slick({
				slidesToShow: {{ count }},
				slidesToScroll: 1,
				autoplay: false,
				autoplaySpeed: 2000,
				responsive: [
					{
					breakpoint: 980,
					settings: {
						slidesToShow: 3,
				slidesToScroll: 1,
				autoplay: false,
				autoplaySpeed: 2000
					}
					},
					{
					breakpoint: 769,
					settings: {
					slidesToShow: 2,
				slidesToScroll: 1,
				autoplay: false,
				autoplaySpeed: 2000
					}
					}
				]
				});
			});
		</script>
	{% endblock javascript %}
	<div class="ec-role ec-sliderRole new_products">
		<div class="ec-newItemRole main_slick">
			<h2 class="online_subtitle">新着商品<a class="all" href="http://localhost/densaku/products/list">すべて見る</a></h2>
			<div class="ec-newItemRole__list" id="new_products_slick">

				{% for product in latest_products %}
				<div class="ec-newItemRole__listItem item slick-slide">
					<a href="{{ url('product_detail', {'id': product.id}) }}">
						<img src="{{ asset(product.main_list_image|no_image_product, 'save_image') }}">
						<p class="ec-newItemRole__listItemTitle">{{ product.name }}</p>
						<p class="ec-newItemRole__listItemPrice">{{ product.price02_min|price }}(税込)</p>
					</a>
				</div>
				{% endfor %}

			</div>
		</div>
	</div>
	```
3. Top Page setting ကိုသွားပြီးတော့ new item block ကို main area ထဲရောက်နေအောင်ထည့်ပါ။
	![Block Positioning](images/seasonal-item-block-position.PNG)
