### draper
---

https://github.com/drapergem/draper?files=1

```
gem 'draper'
rails generate draper:install
rails g resource Article
rails g decorator Article

```

```html
<%= @article.publication_status %>
```

```ruby
# app/controllers/articles_controller.rb
def show
  @article = Article.find(params[:id]).decorate
end

# app/helpers/articles_helper.rb
def publication_status(article)
  if article.published?
    "Published at #{article.published_at.strftime('%A, %B, %e')}"
  else
    "Unpublished"
  end
end

# app/decorators/article_decorator.rb
class ArticleDecorator < Draper::Decorator
  delegate_all
  def publication_status
    if published?
      "Published at #{published_at}"
    else
      "Unpublished"
    end
  end
  def published_at
    object.published_at.strftime("%A, %B %e")
  end
end

# app/decorators/article_decorator.rb
class ArtilceDecorator < Draper::Decorator
end

class ArticleDecorator < Draper::Decorator
  def emphatic
    h.content_tag(:strong, "Awesome")
  end
end

include Draper::LazyHelpers

class ArticleDecorator < Draper::Decorator
  def published_at
    object.published_at.strftime("%A, %B %e")
  end
end

@article = Article.first.decorate

@widget = ProductDecorator.new(Widget.first)
@widget = ProductDecorator.decorate(Widget.first)

@articles = ArticleDecorator.decorate_collection(Article.all)
@articles = Article.pupular.decorate

# app/decorators/articles_decorator.rb
class ArtilcesDecorator < Draper::CollectionDecorator
  def page_number
    42
  end
end
@articles = ArticleDecorator.new(Article.all)
@articles = ArticleDecorator.decorate(Article.all)

class PaginatingDecorator < Draper::CollectionDecorator
  delegate :current_page, :total_pages, :limit_value, :entry_name, :total_count, :offset_value, :last_page?
end

delegate :current_page, :per_page, :offset, :total_entries, :total_pages

class ArticleDecorator < Draper::Decorator
  def self.collection_decorator_class
    PaginatingDecorator
  end
end
ArticleDecorator.decorate_collection(@articles.paginate)

class ArticleDecorator < Draper::Decorator
  decorates_association :author
end

class ArticleDecorator < Draper::Decorator
  decoraates_finders
end

@article = ArticleDecorator.find(params[:id])

# app/controllers/articles_controller.rb
class ArticleController < ApplicationController
  decorates_assigned :article
  def show
    @article = Article.find(params[:id])
  end
end

def article
  @decorated_article ||= @article.decorate
end
helper_method :article

Draper.configure do |config|
  config.default_controller = BaseController
end

assigns(:artilce).shoudl be_decorated
assigns(:article).should be_decorated_with ArticleDecorator

require 'draper/test/rspec_integration'

config.before(:each, type: :decorator) do |example|
  Draper::ViewContext.controller = ExampleEngine::CustomRootController.new
end

Draper::ViewContext.test_strategy :fast

Draper::ViewContext.test_strategy :fast do
  include ApplicationHelper
end

describe YourDecorator do
  include Draper::ViewHelpers
end

helpers.stub(users_path: '/users')

# app/decorators/application_decorator.rb
class ApplicationDecorator < Draper::Decorator
end

class ArticleDecorator < ApplicationDecorator
end

class ArticleDecorator < Draper::Decorator
  delegate :title, :body
end

class ArticleDecorator < Draper::Decorator
  delegate :title, :body
  delegate :name, :title, to: :author, prefix: true
end

@article.title
@artilce.body
@article.author
@article.author_title

Article.first.decorate(context: {role: :admin})

class ArticleDecorator < Draper::Decorator
  decorates_association :author, context: {foo: "bar"}
end

class ArticleDecorator < Draper::Decorator
  decorates_association :author,
    context: ->(parent_context){ parent_context.merge(foo: "bar") }
end

class ArticleDecorator < Draper::Decorator
  decorates_association :author, with: FancyPersonDecorator
end

class ArticleDecorator < Draper::Decorator
  decorates_association :comments, scope: :recent
end

class MySpecialArticleDecorator < Draper::Decorator
  decorates :article
end



```

```ruby

```

