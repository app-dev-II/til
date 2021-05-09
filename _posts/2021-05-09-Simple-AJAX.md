---
layout: post
title: Basic AJAX Setup
---

## Step 1: Add CDN to Application.
Add the [J-Query CDN](https://code.jquery.com/) to the application.  This can be added to a location such as `app/views/shared` in a file such as `_cdn_assets.html.erb`.  This then needs to be rendered in the `app/views/layouts/application.html.erb` (`<%= render "shared/cdn_assets" %>`). 

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.js"></script>
```