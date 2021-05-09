---
layout: post
title: Basic AJAX Setup
---

## Add CDN to Application
Add the [J-Query CDN](https://code.jquery.com/) to the application.  This can be added to a location such as `app/views/shared` in a file such as `_cdn_assets.html.erb`.  This then needs to be rendered in the `app/views/layouts/application.html.erb` (`<%= render "shared/cdn_assets" %>`). 

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.js"></script>
```

## Basic Pattern

### Break the Links
In a `link_to`, add `remote: true` option.

Example:
```ruby
<%= link_to "delete", movie, method: :delete, remote: true %>
```
In a `form_with`, add `local: false` option.

```ruby
<%= form_with(model: comment, local: false) do |form| %>
```

### Add JS Support to Controller

If following stardard Rails conventions, this can be done with something as simple as adding `format.js` to the controller action.
```ruby
  def destroy
    @movie.destroy
    respond_to do |format|
      format.html { redirect_to movies_url, notice: "Movie was successfully destroyed." }
      format.json { head :no_content }
      format.js
    end
  end
```

If this needs to be a custom action, the full path should be called out explicitly.
```ruby
    respond_to do |format|
    # Handle JSON and HTML formats above as usual

    format.js do
        render template: "comments/destroy.js.erb"
    end
    end
```

### Create JS file in View folder
Create a file in the appropriate view folder for the action that needs to take place, such as `destroy.js.erb` or `create.js.erb`.  This is where the javascript will live that will determine the behavior of the website.