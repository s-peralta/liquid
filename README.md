Beginners Guide to Shopify Theme Developer with Liquid
=============================

Folder Structure
--------
  - <strong>Assets</strong> (JS / IMG / CSS)
  - <strong>Config</strong> Folder (Settings Html / Settings JSON)
  - <strong>Layout</strong> (Theme.liquid File AKA Header & Footer)
  - <strong>Snippets</strong> (Imported Modules, Ex/ Social Media Icons , Pagination)
  - <strong>Template</strong> (404.liquid / Article.liquid (Blog Details Page) / Blog.liquid (Blod Listing) / Cart.liquid / Collection.liquid (Display difrent collections/categories) / index.liquid (Homepage / page.liquid (About/Conact/General) / ) Product.liquid (Product detail page) / Search.liquid )


CSS Link
--------
```
{{ "normalize.css" | asset_url | stylesheet_tag }}
{{ "style.css" | asset_url | stylesheet_tag }}
```
JS Link
--------
```
{{ "customer_area.js"  | shopify_asset_url | script_tag }}
{{ '//ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.js' | script_tag }}
```
Image Link
--------
```
{{ 'image-name.gif' | asset_url | img_tag }}
```

HTML Title
--------
```
<title>{{ page_title }} - {{ shop.name }}</title> 
```

```
<body>
  <div class="container">
     <div class="content"> 
      {{ content_for_layout}}
     </div>
  </div>
</body>
 ``` 
Main Menu
--------
``` 
<nav class="main-menu">
 <ul>
   {% for link in linklists.main-menu.links %}
   <li {% if link.active %}class="current"{% endif %}><a href="{{ link.url }}">{{ link.title }}</a></li>
   {% endfor %}
 </ul>
</nav>
  ``` 

Footer Menu
--------
``` 
<footer>
  <ul>
    {% for link in linklists.footer.links %}
    <li><a href="{{ link.url }}">{{ link.title }}</a></li>
    {% endfor %}
  </ul>
</footer>
``` 

Adding Snippet Include
--------
``` 
{% include 'snippet-name' %} Ex / {% include 'header' %}
``` 

Assigns Page and Collection to Index Page
--------
``` 
{% assign page = pages.frontpage %}
<div class="rte index-page">
    <h2>{{ page.title }}</h2>
    {{ page.content }}
</div>

```
``` 

{% assign collection = collections.frontpage %}
<div class="index-collection clearfix">
  <h2>{{ collection.title }}</h2>
    <ul>
    {% for product in collection.products | limit:8 %}
      {{ product.title }}
      <li>
      <a href="{{product.url}}">
        <img src="{{ product.featured_image | product_img_url: 'medium' }}" />
      </a>
      {{product.price | money}}
    </li>
    {% endfor %}
  </ul>
</div>

```


  
Settings HTML
--------

Settings.html Wrapper
```
<fieldset>
  <legend>Product pages</legend>
  <table>
  </table>
</fieldset>
```
Input Field
```
<input type="text" name="text_input" value="" />
{{settings.text_input}} 

```
Text Area
```
<textarea name="text_area" cols="60" rows="5" id="my_textarea" value="" />
{{settings.text_areat}} 
```

Checked Conditional Statment
```
{% if settings.my_checkbox %}
  <p> Lorem Ipsum</p>
{% end-if  %}
```

If Conditional Statment
```
{% if template == 'list-collections' %}
{% include 'collection-listing' %}
{% else %}
{{ content_for_layout }}
{% endif %}
```
