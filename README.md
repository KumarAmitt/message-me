# Message Me

## 1. Adding `semantic-ui-sass`
- GitHub: `https://github.com/doabit/semantic-ui-sass`
- Add gems: `gem 'semantic-ui-sass'` and `gem 'jquery-rails'`
- Add jquery and semantic-ui to `app/assets/javascripts/application.js`
```js
//= require rails-ujs
//= require activestorage
//= require turbolinks
//= require jquery
//= require semantic-ui
//= require_tree .


// You can add jquery functionality like this (optional)
$(document).on('turbolinks:load', () => {
    $('.ui.dropdown').dropdown();
})

```
- Import the scss file to `app/assets/stylesheets/custom.css.scss`
```scss
@import "semantic-ui";
```

## 2. Adding favicon
- Add `favicon.ico` file to `/images` folder
- Add ` <%= favicon_link_tag %>` to head section in `app/views/layouts/application.html.erb`


## Hirb Gem - Enables tabular view in rails console
- Add `gem 'hirb'`
- Go to rails console and run `Hirb.enable`
- Now you are good to view data in tabular forms