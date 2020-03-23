# Quiz: Object Relationships

???

## Object Relationships

?: Which is an example of object relationships?

( ) Seeing mutually shared friends in a social media application ( ) Comments on a blog from various users ( ) Viewing previous orders on a shopping platform (X) All of the Above

?: If a comment can have only one user, this is a `belongs to` relationship.

(X) True ( ) False

?: If a user can make comments on a post, this a `belongs to` relationship.

( ) True (X) False

?: If a user can have a type (ex. admin, moderator, subscriber, etc.) , this a `belongs to` relationship.

(X) True ( ) False

?: If a user can make posts, this is a `has many` relationship.

(X) True ( ) False

?: If a user can like posts, this is a `has many` relationship.

(X) True ( ) False

?: If a post can receive likes, this is a `belongs to` relationship.

( ) True (X) False

?: If a comment can have only one user and a user can have many comments, what is this relationship called?

( ) belongs to ( ) has many (X) belongs to/has many ( ) Object Reciprocity

?:

```ruby
class User
  attr_accessor :user

  def initialize(user)
    @user = user
    @comments = []
  end

  def add_comment(comment)
    @comments << comment
    comment.user = self
  end

  def comments
    @comments
  end
end

class Comment
  attr_accessor :user, :text

  @@all = []

  def initialize(text)
    @text = text
    save
  end

  def save
    @@all << self
  end

  def self.all
    @@all
  end
end
```

Maintaining the relationship on both the `User` instance and the `Comment` instance in this code means there are two sources of truth.

(X) True ( ) False

?:

```ruby
class Comment
  attr_accessor :user, :text

  @@all = []

  def initialize(text)
    @text = text
    save
  end

  def save
    @@all << self
  end

  def self.all
    @@all
  end
end
```

```ruby
class User
  attr_accessor :user

  def initialize(user)
    @user = user
  end

  def add_comment(text)
    comment = Comment.new(text)
    comment.user = self
  end

  def comments
    Comment.all.select {|comment| comment.user == self}
  end
end
```

This implementation is a "has-many" / "belongs-to" relationship with a single source of truth.

(X) True ( ) False

?: A user can have many "likes" from posts with a "has-many-through" relationship.

(X) True ( ) False

???
