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


## 3. Hirb Gem - Enables tabular view in rails console
- Add `gem 'hirb'`
- Go to rails console and run `Hirb.enable`
- Now you are good to view data in tabular forms

## 4. Action Cable
- Run `rails g channel chatroom` to create a channel
- Update the `app/channels/chatroom_channel.rb`
```ruby
  def subscribed
    stream_from "chatroom_channel"
  end
```

- To Mount the cable to route, add the following line to `config/routes.rb`
```ruby
 mount ActionCable.server, at: '/cable'
```

- Update the controller
- Previously
```ruby
  def create
    message = current_user.messages.build(message_params)
    if message.save
      redirect_to root_path
    end
  end
```
- After update
```ruby
  def create
    message = current_user.messages.build(message_params)
    if message.save
      ActionCable.server.broadcast "chatroom_channel", mod_message: message_render(message)
    end
  end

# Add the following private method
  def message_render(message)
    render(partial: 'message', locals: {message: message})
  end
```

- Update `app/javascripts/channels/chatroom.coffee`
```coffee
  received: (data) ->
    $('#message-container').append data.mod_message
```

- Update the views
    - Add the id of `message-container`
    - ```ruby
        <div class="ui feed" id="message-container">
          <%= render @messages %>
        </div>
        ```
    - Add `remote: true` to the form
    - ```ruby
       <%= form_for(@message, html: {class: "ui reply form"}, url: message_path, remote: true) do |f| %>
      ```
