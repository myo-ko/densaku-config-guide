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

## Gift Products
1. Navigate to **Contents** > **Pages**
2. Create a new page.
    - Page Name: Gift (お中元　お歳暮) Page
	- URL: gift
	- File Name: gift
3. Add the following code:
	```
	{% set tag = 'お中元　お歳暮' %}
	{% set query = repository('Eccube\\Entity\\Product').createQueryBuilder('p').innerJoin('p.ProductTag','pt').innerJoin('pt.Tag','t').where('t.name = :tag').andWhere('p.Status = 1').setParameter('tag', tag).getQuery() %}
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
4. Select the **下層ページ用レイアウト** in Layout Setting -> PC.
5. Leave others as default.
6. Save.

## Generating URL for the 2 pages
1. Navigate to **Contents** > **Blocks**.
2. Find the block with name **カテゴリ**.
3. There should be an `<a>` element around line 39 or 44. *(39 is pick-up products link and 44 is gift products link)*
4. Modify their `href` attribute as follows:
    - Pick-up products link : `href="{{ url('user_data',{'route':'pick_up'}) }}"`
    - Gift products link : `href="{{ url('user_data',{'route':'gift'}) }}"`
5. Full code:
	```
	{#
	This file is part of EC-CUBE

	Copyright(c) LOCKON CO.,LTD. All Rights Reserved.

	http://www.lockon.co.jp/

	For the full copyright and license information, please view the LICENSE
	file that was distributed with this source code.
	#}
	<style>
		.ec-categoryRole {
			background: #fff;
		}
		@media only screen and (max-width: 767px){
			.ec-categoryRole .ec-categoryRole__listItem{
				width: 50%;
			}
			.ec-categoryRole .ec-categoryRole__listItem a{
				display: inline-block;
				width: 95%;
			}
			.ec-categoryRole .ec-categoryRole__listItem:nth-child(even){
				text-align: right;
			}
		}
		
	</style>

	<div class="ec-categoryRole">
		<div class="ec-role">
			<div class="ec-secHeading">
				{#<span class="ec-secHeading__en">{{ 'CATEGORY'|trans }}</span>#}
				{#<span class="ec-secHeading__line"></span>#}
				<span class="ec-secHeading__en">{{ 'カテゴリ'|trans }}</span>
			</div>
			<div class="ec-categoryRole__list">
				<div class="ec-categoryRole__listItem">
					<a href="{{ url('user_data',{'route':'pick_up'}) }}">
						<img src="{{ asset('assets/img/category/img_top_bna_pickup.jpg') }}">
					</a>
				</div>
				<div class="ec-categoryRole__listItem">
					<a href="{{ url('user_data',{'route':'gift'}) }}">
						<img src="{{ asset('assets/img/category/img_top_bna_gift.jpg') }}">
					</a>
				</div>
				<div class="ec-categoryRole__listItem">
					<a href="http://renew.den-saku.com/supplierdensaku/public/jobSearch">
						<img src="{{ asset('assets/img/category/img_top_bna_recruit.jpg') }}">
					</a>
				</div>
				<div class="ec-categoryRole__listItem">
					<a href="#" target="_blank">
						<img src="{{ asset('assets/img/category/img_default.jpg') }}">
					</a>
				</div>
			</div>
		</div>
	</div>
	```
6. Save the changes.
7. Verify that **カテゴリ** block is in Top Page Layout. <br>
	![Block Positioning](images/seasonal-item-block-position.PNG)