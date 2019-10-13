---
layout: post
title:      "Observing and Preserving"
date:       2019-10-13 20:00:08 +0000
permalink:  observing_and_preserving
---



After finishing my MVC Sinatra Application felt like I caught a glimpse of what is possible. I know that there is still so much to learn before I can confidently start applying to jobs. Though after completing it did feel a sense that yes as long as keep on this track that will be possible. The first project took a toll on me and while I did complete it on the first try due to how much trouble I had understanding the concepts had to use the grace period. Coming into this project had that worried that would need the grace period again or worst-case scenario would have to fall behind one cohort. Happy to say that wasn’t the case this time around. Felt as though I understood the concepts quicker and while yes still got stuck it didn’t take me half as long this time to understand where the issue was coming from and to fix it. 

One of the issues I did have with this project would be that since I was a week behind due to the first project I had to skip the CSS section. This led to the application not having the aesthetics I wanted it to have. Did make some small changes though even though weren’t perfect in my eyes. The CSS section is something that I will be going back to complete. I want to make this application better, given that it is one that I want to present during job interviews but not in its current state. 

The basics of my applications are that it allows users to sign in and out and create posts about nighttime observations. While all signed-in users are allowed to see all other users post only the owner of the post is able to edit or delete their own post. Validations are in place requiring that during the initial sign up Name, Username, and password must be entered, while the post requires no blank entries are left for title, link, description, latitude, longitude, and date. In addition, added a validation that the username must be unique and that the password must be at least 3 characters long. Snip it of my code below for models of post and user. 

```
class User < ActiveRecord::Base
   
    has_many :post
    has_secure_password 
 
    validates :username, :password, presence: true
    validates :password, length: { minimum: 3 }
    validates :username, uniqueness: true
  end
class Post < ActiveRecord::Base
    belongs_to :user
    validates :title, :link, :description, :latitude, :longitude, :date, presence: true
    
end
```

```
class User < ActiveRecord::Base
   
    has_many :post
    has_secure_password 
 
    validates :username, :password, presence: true
    validates :password, length: { minimum: 3 }
    validates :username, uniqueness: true
  end
class Post < ActiveRecord::Base
    belongs_to :user
    validates :title, :link, :description, :latitude, :longitude, :date, presence: true
    
end
```
 

One of the little extras I wanted to add in is that I wanted each post to state who wrote the post underneath each entry so that they could get credit. In the possibility anybody would like to do the same here is how I did it. 

In my index.rb under Posts, I used the following code. 

```
<h1>Posts</h1> 
<br> 
<br> 
<% @posts.each do |detail| %> 
    <h2><a href ="/posts/<%=detail.id%>"><%= detail.title %></a></h2>
    <% @user = User.find_by(:id => detail.user_id) %>
    <h4> Written By "<%= @user.name %>" <h4> 
    
<% end %> 
```
 

The first thing my code does is split each post created individually into details. Then @user is defined ad being the details user id which would be the foreign key for the post. This allows us to know which user wrote the post, though at this step only the number is known. I follow this up by stating @user.name which now gives us the name of the writer of the post. It’s simple to do and gives a personal touch which I think is nice. 

As a side note, I just want to thank the person who wrote the Corneal Gem made starting it off so easy. 
