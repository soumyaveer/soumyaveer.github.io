---
layout: post
title: Nested Forms in Rails
date:  2017-09-29 17:30:00
categories: main
banner_image: "coding1.jpg"
summary: When I started reading about Nested forms, it looked difficult. But soon I realised, I am not alone on this journey. Rails has provided me with some great helpers!
---

While reading about creating forms in Rails, I came across __Nested Forms__. On the first glance it looked difficult, but as I progressed, I said to myself, "It's not so bad!".

In order to create Nested Forms, it is important to understand about the helpers provided by Rails.

1). `accepts_nested_attributes_for`: Imagine that we have a BookShelf which has many Books. And the Books contain a title and an author. This setup calls for nested attributes.
<br/>
<br/>
```ruby
  class BookShelf < ActiveRecord::Base
    has_many :books
    accepts_nested_attributes_for :books
  end
```
<br/>

`accepts_nested_attributes_for` provides us with `books_attributes=` (setter) method. Now, we can set the attributes of model `books`, through `bookshelf` hash. The params in this case will be.
<br/>
<br/>

```ruby
params = {
  bookshelf: {
    size: "small",
    books_attributes: [
      {title: "Coders at Work", author: "Peter Seibel"},
      {title: "Design Patterns in Ruby", author: "Russ Olsen"},
      {title: "The Pragmatic Programmer", author: "Andy Hunt"}
    ]
  }
}
```
<br/>
`accepts_nested_attributes_for` also provides us with some options:
   * `reject_if`: Helps us to ignore the hashes that fail the criteria or required validations.

      ```ruby
       class BookShelf < ActiveRecord::Base
         has_many :books
         accepts_nested_attributes_for :books, reject_if: proc {
          |attribute| attribute['title'].blank?
         }
       end
      ```
<br/>

  * `allow_destroy`: Allows us to delete the records trough attributes hash.

     ```ruby
     class BookShelf < ActiveRecord::Base
         has_many :books
         accepts_nested_attributes_for :books, allow_destroy: true
      end
     ```
<br/>

2). `fields_for`: This helper takes two arguments. The first argument is the model for which we want to create the attributes and the second is the object. It allows the methods to be called on builder in order to generate fields.
 <br/>
 <br/>

    ```ruby

      <%= f.fields_for :books, Book.new do |book_attributes| %>
        <%= book_attributes.text_field :title %>
        <%= book_attributes.text_field :author %>
      <% end %>

    ```

<br/>
 Using these form helpers, we can create nested forms.

__Step1.__ Add `accepts_nested_attributes_for` in the model whose hash will contain the nested attributes.
<br/>
<br/>

  ```ruby
    class BookShelf < ActiveRecord::Base
      has_many :books
      accepts_nested_attributes_for :books
    end
  ```

  As stated above, this code will provide us with `books_attributes=` method.
<br/>
<br/>
__Step2.__ Update strong parameters in `BookShelf` controller so that it accepts the `books_attributes`.
<br/>
<br/>

  ```ruby
    class BookShelvesController < ApplicationController
      def index
        @bookshelves = BookShelf.all
      end

      def show
        @bookshelf = BookShelf.find(params[:id])
      end

      def new
        @bookshelf = BookShelf.new
      end

      def create
        @bookshelf = BookShelf.new(bookshelf_params)
        if @bookshelf.save
          redirect_to bookshelf_path(@bookshelf)
        else
          render new_bookshelf_path
        end
      end

      private

      def bookshelf_params
        params.require(:bookshelf).permit(:size, books_attributes: [:title, :author])
      end
    end
  ```
  <br/>

__Step 3.__ Updating the view. In our view, we use `fields_for` helper method.
<br/>
<br/>

  ```html
    <div>
      <%= form_for :bookshelf do |f| %>
        <div>
          <%= f.label :size %>
          <%= f.text_field :size %>
        <div/>
        <div>
          <%= f.fields_for :books, Book.new do |book_attributes| %>
            <%= book_attributes.label :title %>
            <%= book_attributes.text_field :title %>
            <br/>
            <%= book_attributes.label :author %>
            <%= book_attributes.text_field :author %>
          <% end %>
        <div/>
        <%= f.submit %>
      <% end %>
    <div/>
  ```

Finally, login to rails server and check the form.
