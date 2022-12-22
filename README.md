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
```
- Import the scss file to `app/assets/stylesheets/custom.css.scss`
```scss
@import "semantic-ui";
```