---
layout: post
title:      "Foggy, but not for long "
date:       2020-10-02 01:01:16 -0400
permalink:  theres_still_a_lot_to_learn_and_relearn
---


You truly do forget what you don’t practice. Since I needed to complete a few past assignments to get to the 95% percent that is required in order to graduate I went back and finished the Sinatra Fwitter Group Project. When first looking at it I thought it was going to be a breeze. It wasn't until I was an hour in that  I realized just how much I had forgotten about Sinatra. 

Concepts that at one point I spent so much time learning and memorizing that were so clear to me at one point, were then so foggy that if I was driving I would have pulled over and waited for the fog to clear. It was an uphill struggle to say the least. Now, that being said the fog did clear and the concepts did start coming back to me little by little, but boy oh boy I thought I was going to hit a tree in that fog. 

One concept that had left my memory in a complete haze was the difference between using erb and redirect in controllers. And let me tell you the errors kept popping up letting me know when I was using the incorrect one. 

After a lot of trial and error I re-learned that a key difference is that `redirect to` does not persist data, simply put all the data is lost when `redirect to` is used. While when using `erb` the instance variables are saved. 

Another key difference is how erb and redirect are called upon in the controllers.

```
    get '/signup' do
        if !logged_in?
            erb :'users/signup'
        else
            redirect to "/tweets"
        end
    end
```

As can be seen above when using erb the location of the erb file must be specified including adding the folder of where it is under. While when using the redirect to it is referring to ‘/tweets’ under the TweetsController. 

```
    get '/tweets' do
        if logged_in?
          @tweets = Tweet.all
          erb :'tweets/tweets'
        else
          redirect to '/login'
        end
      end
```

This wasn't the only concept that cleared for me when trying to finish this mini-project. 

One refresher came while I was completing the the Sinatra Fwitter project, it was what ||= was used for. ||= states that if whatever is to the left of is false or equal to nil then and only then assign it to the formula that is to the right of it.

      `@current_user ||= User.find_by(id: session[:user_id]) if session[:user_id]`

In the example above it is stating that if @current_user equals nil then assign @current_user to the User that is equal to the user_id of the session. But only if the session has a current user. 

In this example if @current_user equals nil and session[:user_id] equals nil as well then and only then will @current_user equal nil. 




