---
layout: post
title:      "There's still a lot to learn, and relearn "
date:       2020-10-02 05:01:15 +0000
permalink:  theres_still_a_lot_to_learn_and_relearn
---


As my final was near and my requirement to complete 95% of all assignments was also fast approaching I found myself going back to past bonus labs that I didn’t complete during my initial run. During those labs I re-learned many little things that I only used a handful of times and some just one or twice for lab. A portion of the things I re-learned would have made my life much easier for other projects while for some labs I learned brand new things that I know wish I would have played around with more during that initial run. 

One refresher came while I was completing the the Sinatra Fwitter project, it was what ||= was used for. ||= states that if whatever is to the left of is false or equal to nil then and only then assign it to the formula that is to the right of it.

      `@current_user ||= User.find_by(id: session[:user_id]) if session[:user_id]`

In the example above it is stating that if @current_user equals nil then assign @current_user to the User that is equal to the user_id of the session. But only if the session has a current user. 

In this example if @current_user equals nil and session[:user_id] equals nil as well then and only then will @current_user equal nil. 


Another concept that I glanced over and never fully delved into were Slugs. Not the ones in our backyards or gardens but the ones that are used by so many different websites to make our daily browsing so much easier. While slugs change something in a small one some may say when you notice it, it’s hard to miss it. Kinda like a slug in your garden eating your tomato. 

Slugs are the reason that when you go to your Facebook profile it states https://www.facebook.com/unique_user_identifer/ instead of https://www.facebook.com/asdfsdafjka98wr93r8ayefiuhrawr9yere9yfda89fasdf/ one is much more user friendly and easy on the eyes. While the other is friendly if you couldn’t solve the captcha when trying to access one of those pesky websites that keeps asking if you're a human. 

To set up a Slug all you need to do is navigate over to your Model and do the following. 

`
class User < ActiveRecord::BASE 

def slug 

self.username.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')

end 	

def self.find_by_slug(slug)
	User.all.find{|user| user.slug == slug}
end 

end
` 

I know many may be asking what is that slugging doing. I’m more than happy that you asked. 

This slug is ensuring that all characters are lowercase. It is ensuring that there are no leading or trailing whitespaces, done by adding strip. The first gsub replacing any spaces the user enters with hyphens. The following gsuc removes all non-alpha, non-dash, non-underscore characters meaning only characters a-z and numbers 1-9 will populate. 

Now in the users controller I’d write the following

    get '/users/:slug' do
      @user = User.find_by_slug(params[:slug])
      erb :'users/show'
    end


And with that the url has become a lot more friendly. 



