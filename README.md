# Lightning Talk - Formtastic

Formtastic is a Ruby gem to help speed up form creation. It's pretty similar to the standard Rails form code, but it generates more HTML that can be used to make your forms more functional.

## Installing Formtastic

Add this line to your Gemfile and run bundle install.

```
gem 'formtastic', '~> 3.1'
```

Run rails generate to install the template into your app. This is a one time only step.

```
rails generate formtastic:install
```

Formtastic also comes with some default CSS that you can later adjust to create your own look and feel for your forms.

![alt text](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2011/12/origami-form.png)

Add the following lines to: `app/assets/stylesheets/application.css`

```
  *= require formtastic
  *= require my_formtastic_changes
```

If you'd like to make any changes to the styling, create a new file called `my_formtastic_changes.css` in your stylesheets folder.

```
touch app/assets/stylesheets/my_formtastic_changes.css
```

## Relationships

Formtastic automatically handles relationships between models for you.

```
# generate the Article scaffold with a category
rails generate scaffold Article title:string category:references body:text author:string

# add the relationship to the Article model
belongs_to :category

# update strong parameters in the Article Controller
def article_params
  params.require(:article).permit(:title, :body, :category_id, :author)
end

# generate the Category model, we are adding in a cat_type for further classification
rails generate model Category name:string cat_type:integer

# create categories in the Rails console
Category.create(name: 'Technology', cat_type: 1)
Category.create(name: 'Lifestyle', cat_type: 2)
Category.create(name: 'Business', cat_type: 1)
Category.create(name: 'Entertainment', cat_type: 2)
```
So Formtastic will automatically reference the relationship if you reference it by the relationship name `category` and not by the table column name `category_id`

```
<%= f.inputs do %>
  <%= f.input :title %>
  <%= f.input :category %>
  <%= f.input :body %>
<% end %>
```

## TLDR

* It can handle belongs_to associations (like Post belongs_to :author), rendering a select or set of radio inputs with choices from the parent model.
* It can handle has_many and has_and_belongs_to_many associations (like: Post has_many :tags), rendering a multi-select with choices from the child models.
* It's Rails 3/4 compatible (including nested forms).
* It has internationalization (I18n)!
* It's really quick to get started with a basic form in place (4 lines), then go back to add in more detail if you need it.
* There's heaps of elements, id and class attributes for you to hook in your CSS and JS.
* It handles real world stuff like inline hints, inline error messages & help text.
* It doesn't hijack or change any of the standard Rails form inputs, so you can still use them as expected (even mix and match).
* It's got absolutely awesome spec coverage.
* There's a bunch of people using and working on it (it's not just one developer building half a solution).
* It has growing HTML5 support (new inputs like email/phone/search, new attributes like required/min/max/step/placeholder)

## More info

[Formtastic Forms in Rails for Beginners](http://buildingrails.com/a/formtastic_forms_in_rails_for_beginners) - A beginner's guide to setting up Formtastic

[Formtastic](https://github.com/justinfrench/formtastic) - Offical Formtastic site

[Formtastic Wiki ](https://github.com/justinfrench/formtastic/wiki) - More details and guides to Formtastic