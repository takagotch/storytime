### storytime
---
https://github.com/CultivateLabs/storytime

```
gem "storytime"
bundle binstub storytime
stotytime install
storytime install -d
rails g storytime:install

rake storytime:install:migrations
rake db:migrate

rails g storytime:views
rails g storytime:views - v dashboard pages posts
rails g storytime:views -v application blogs comments dashboard pages posts sites snippets subscription_mailer subscriptions


rails g storytime_admin:resource Widget

```

```ruby
mount Storytime::Engine => "/"

class User < ActiveRecord::Base
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :trackable, :validatable
  storytime_user
end


# app/controllers/stroytime_admin/widgets_controller.rb
module StroytimeAdmin
  class WidgetsController < StorytimeAdmin::ApplicationController
    set_tab :admin, :widgets
  end
end

# config/initializers/storytime_admin.rb
StorytimeAdmin.configure do |config|
  config.user_class = 'Admin'
end

# app/models/admin.rb
class Admin
  storytime_user
  def admin?
    true
  end
end

# config/initializers/storytime.rb
config.post_sanitizer = Proc.new do |draft_content|
  if Rails::VERSION::MINOR <= 1
    white_list_sanitizer.allowed_tags
    tags = white_list_sanitizer.allowed_tags
    attributes = white_list_sanitizer.allowed_attributes
  else
    white_list_sanitizer = Rails::Html::WhiteListSanitizer.new
    tags = Loofah::HTML5::WhiteList::ALLOWED_ELEMENTS_WITH_LIBXML_2
    attributes = Loofah::HTML5::WhiteList::ALLOWED_ATTRIBUTES
  end
  tags.add("iframe")
  attributes.merge(["frameborder", "allowfullscreen"])
  white_list_sanitizer.sanitize(draft_content, tags: tags, attributes: attributes)
end


config.post_sanitizer = Proc.new do |draft_content|
  draft_content
end

@@post_sanitizer = Proc.new do |draft_content|
  if Rails::VERSION::MINOR <= 1
    white_list_sanitizer = HTML::WhiteListSanitizer.new
    tags = white_list_sanitizer.allowed_tags
    attributes = white_list_sanitizer.allowed_attributes
  else
    white_list_sanitizer = Rails::Html::WhiteListSanitizer.new
    tags = Loofah::HTML5::WhiteList::ALLOWED_ELEMENTS_WITH_LIBXML2
    attributes = Loofah::HTML5::WhiteList::ALLOWED_ATTRIBUTES
  end
  white_list_sanitizer.sanitize(draft_content, tags: tags, attributes: attributes)

```

```
<div class="post"><%= @post.content %><?div>
<div>Enjoy this post? Sing up and we'll notify you of future posts!</div>
<%= stroytime_email_subscription_form %>
```


