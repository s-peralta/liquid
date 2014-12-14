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

Declare Header
--------
```
<head>
  <meta charset="utf-8">

  {{ content_for_header }}

  {{ "normalize.css" | asset_url | stylesheet_tag }}
  {{ "style.css" | asset_url | stylesheet_tag }}
</head>
 ``` 

Declare Body Content
--------
```
<body>
  <div class="container">
     <div class="content"> 
      {{ content_for_layout}}
     </div>
  </div>
</body>
 ``` 
<img src="http://www.tetchi.ca/wp-content/uploads/2013/04/sections.png" alt="sections"/>


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

Paginate Products
--------
``` 
{% paginate collection.products by 3 %}

{% for product in collection.products %}
  {{ product.title }}
  <li>
  <a href="{{product.url}}">
    <img src="{{ product.featured_image | product_img_url: 'medium' }}" />
  </a>
  {{product.price | money}}
</li>
{% endfor %}

{% if paginate.pages > 1 %}
<div class="pagination">
  {{ paginate | default_pagination }}
</div>
{% endif %}

{% endpaginate %}

```
Add Contact Page
--------
```
<div id="page" class="row">
  
  <div class="span12">
    <h1>{{ page.title }}</h1>
    <div class="page-with-contact-form">
      {{ page.content }}
            
        {% form 'contact' %}
        {% if form.posted_successfully? %}
        <div class="successForm feedback">
          <p>{{ 'contact.form.post_success' | t }}</p>
        </div>
        {% endif %}

        {% if form.errors %}
        <div class="errorForm feedback">
          <p>{{ 'contact.form.post_error' | t }}</p>
          {% for field in form.errors %}
            <p>{{ 'contact.form.post_field_error_html' | t: field: field, error: form.errors.messages[field] }}</p>
          {% endfor %}
        </div>
        {% endif %}

        <div id="contactFormWrapper">
          <p>
            <label>{{ 'contact.form.name' | t }}:</label><br/>
            <input type="text" id="contactFormName" name="contact[name]" placeholder="{{ 'contact.placeholder.name' | t }}" />
          </p>
          <p>
            <label>{{ 'contact.form.email' | t }}:</label><br/>
            <input type="email" id="contactFormEmail" name="contact[email]" placeholder="{{ 'contact.placeholder.email' | t }}" />
          </p>
          <p>
            <label>{{ 'contact.form.phone' | t }}:</label><br/>
            <input type="telephone" id="contactFormTelephone" name="contact[phone]" placeholder="{{ 'contact.placeholder.phone' | t }}" />
          </p> 
          <p>
            <label>{{ 'contact.form.message' | t }}:</label><br/>
            <textarea rows="15" cols="75" id="contactFormMessage" name="contact[body]" placeholder="{{ 'contact.placeholder.message' | t }}"></textarea>
          </p>
          <p>
            <input type="submit" id="contactFormSubmit" value="{{ 'contact.form.send' | t }}" class="btn" />
          </p>
        </div>
        {% endform %}
      
    </div>
  </div>
  
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
