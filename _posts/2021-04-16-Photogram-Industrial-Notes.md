---
layout: post
title: Photogram Industrial
---

 - General Questions as I work?
   - For comments, does both users and photos need an index?
   - When do I need to reference `foreign_key` or `inverse_of`
   - Do I just use `inverse_of: 'author'` to reference phots in user model?
   - What does `index: true` in db migration do?  What is the consequnce of having one but not using it?
   - Useful migration tip `rails g migration AddPhotosCountToUsers photos_count:integer`
   - DB update default [link](https://blog.arkency.com/how-to-add-a-default-value-to-an-existing-column-in-a-rails-migration/)
   - Wrap `destroy_all` in `if Rail.env.development` statement to protect production
   - For each `has_many` decide if I need to add a `dependent: :destroy`
 - Steps in creating application
   - Create model/resources
   - Generate business logic: direct and indirect associations
   - Create validations
   - Create scopes