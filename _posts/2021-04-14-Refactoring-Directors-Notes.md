---
layout: post
title: Refactoring Directors
---

### Step by step notes for directors set up

 - Generating model using `rails g model director name dob:date`
 - Ran `rake db:migrate` (I think this was required)
 - Added `resources :directors` to route.rb
 - Created directors controller
 - Created directors index page
 - Created directors new page
 - Created directors show page
 - Created directors edit page
 - Used `form date_select` to capture date in appropriate format
 - Added validation that both `:name` and `:dob` are present in the model
 - Added links to get from Movies index to Directors index, and vice-versa
 