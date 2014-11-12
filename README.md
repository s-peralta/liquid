Beginners Guide to Shopify Theme Developer with Liquid
=============================

Folder Structure
--------
  - <strong>Assets</strong> (JS / IMG / CSS)
  - <strong>Config</strong> Folder (Settings Html / Settings JSON)
  - <strong>Layout</strong> (Theme.liquid File AKA Header & Footer)
  - <strong>Snippets</strong> (Imported Modules, Ex/ Social Media Icons , Pagination)
  - <strong>Template</strong> (404.liquid / Article.liquid (Blog Details Page) / Blog.liquid (Blod Listing) / Cart.liquid / Collection.liquid (Display difrent collections/categories) / index.liquid (Homepage / page.liquid (About/Conact/General) / ) Product.liquid (Product detail page) / Search.liquid )
  - 
  

CSS LINK
--------
```
{{ "normalize.css" | asset_url | stylesheet_tag }}
{{ "style.css" | asset_url | stylesheet_tag }}
```
JS LINK
--------
```
{{ "customer_area.js"  | shopify_asset_url | script_tag }}
{{ '//ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.js' | script_tag }}
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


