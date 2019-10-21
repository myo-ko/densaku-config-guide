# Added Picked-up Products and Gifted Products Pages
## Pick-up Products
1. Create 2 new product tags: Pick-up **(ピックアップ)** and Gift **(お中元　お歳暮)**.
 Use the Japanese characters only.
2. Link products with the tags. *(optional)*
3. Navigate to **Contents** > **Pages**
4. Create a new page.
    - Page Name: Picked Up (ピックアップ) Page
    - URL: pick_up
    - File Name: pick_up
5. Add the following code:
	```
	{% set query = repository('Eccube\\Entity\\Product').createQueryBuilder('p').innerJoin('p.ProductTag','pt').innerJoin('pt.Tag','t').where('t.name = :tag').andWhere('p.Status = 1').setParameter('tag', 'ピックアップ').getQuery() %}
	{% set products = query.getResult() %}

	{% extends 'default_frame.twig' %}

	{% block main %}
	<div class="ec-role">
		<div class="ec-newItemRole">
			<div class="ec-newItemRole__list">
				<div class="ec-newItemRole__listItem">
					<div class="ec-newItemRole__listItemHeading ec-secHeading--tandem">
						<span class="ec-secHeading__en">ピックアップ</span>
						<span class="ec-secHeading__line"></span>
						<span class="ec-secHeading__ja"></span>
						<a class="ec-inlineBtn--top" href="{{ url('product_list') }}">{{ 'more'|trans }}</a>
					</div>
				</div>
				{% for product in products %}
				<div class="ec-newItemRole__listItem">
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

	{% endblock %}
	```
6. Select the **下層ページ用レイアウト** in Layout Setting -> PC.
7. Leave others as default.
8. Save.