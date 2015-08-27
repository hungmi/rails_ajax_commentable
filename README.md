# Rails_Ajax_Commentable
Rails commentable concerns for controller and model.
Update comments via Ajax.

## Installation
```
app/controllers/concerns/commentable_actions.rb
app/models/concerns/commentable.rb
```
## Controller
class UsersController < ApplicationController
  include CommentableActions
end

## Model
``` ruby
class User < ActiveRecord::Base
  include Commentable
  
  def my_comments
    Comment.where(author_id: id)
  end
end
```
``` ruby
class Comment < ActiveRecord::Base
  belongs_to :commentable, polymorphic: true
  belongs_to :author, class_name: "User", foreign_key: :author_id
  include Commentable
end
```

## Usage

### All comments ON an USER
``` ruby
User.first.comments
```
### All comments OF an AUTHOR
NOTE: Only User can be Author.
``` ruby
User.first.my_comments
```
### Author of a comment
``` ruby
Comment.first.author
```



