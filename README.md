# rake js:rails:routes

Generate a ES6 module that contains Rails routes.

## Description

This gem provides "js:rails:routes" rake task.
It generates a ES6 requirable module whith exports url helper functions defined by your Rails application.

Suppose there are some routes defined:

```rb
# == Route Map
#
#       Prefix Verb   URI Pattern                        Controller#Action
#     articles GET    /articles(.:format)                articles#index
#              POST   /articles(.:format)                articles#create
#  new_article GET    /articles/new(.:format)            articles#new
# edit_article GET    /articles/:id/edit(.:format)       articles#edit
#      article GET    /articles/:id(.:format)            articles#show
#              PATCH  /articles/:id(.:format)            articles#update
#              PUT    /articles/:id(.:format)            articles#update
#              DELETE /articles/:id(.:format)            articles#destroy
Rails.application.routes.draw do
  resources :articles
end
```

The JS file generated by this gem exports following functions:

```js
var RailsRoutes = require('./rails-routes');
RailsRoutes.articles_path();              //=> '/articles'
RailsRoutes.new_article_path();           //=> '/articles/new'
RailsRoutes.edit_article_path({ id: 1 }); //=> '/articles/1/edit'
RailsRoutes.article_path({ id: 1 });      //=> '/articles/1'
```

## VS.

[railsware/js-routes](https://github.com/railsware/js-routes) spreads url helpers via global variable.

This gem uses ES6 modules.

## Requirement

- Rails >= 3.0

## Usage

Write all routes to app/assets/javascripts/rails-routes.js:

```
rake js:rails:routes
```

Write to client/src/rails-routes.js:

```
rake js:rails:routes path='client/src/rails-routes.js'
```

Generate routes except paths start with "/rails/" or "/sidekiq/":

```
rake js:rails:routes excludes='^/(rails|sidekiq)/'
```
Generate routes start with "/articles/" only:

```
rake js:rails:routes includes='^/articles/'
```

## Install

Your Rails Gemfile:

```
gem 'js_rails_routes', group: :development
```

## License

[MIT](https://github.com/yuku-t/js_rails_routes/blob/master/LICENCE)

## Author

[mizchi](https://github.com/mizchi) wrote "js:rake" task with referencing [mtrpcic/js-routes](https://github.com/mtrpcic/js-routes).

[yuku-t](https://yuku-t.com) refactor and improve the mizchi's script and published to rubygems.
