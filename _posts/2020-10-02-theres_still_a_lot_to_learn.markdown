---
layout: post
title:      "There's still a lot to learn and relearn"
date:       2020-10-02 01:40:04 -0400
permalink:  theres_still_a_lot_to_learn
---


As my final was near and my requirement to complete 95% of all assignments was also fast approaching I found myself going back to past bonus labs that I didn’t complete during my initial run. During those labs I re-learned many little things that I only used a handful of times and some just one or twice for lab. A portion of the things I re-learned would have made my life much easier for other projects while for some labs I learned brand new things that I know wish I would have played around with more during that initial run. 

Another concept that I glanced over and never fully delved into were Slugs. Not the ones in our backyards or gardens but the ones that are used by so many different websites to make our daily browsing so much easier. While slugs change something in a small one, some may say when you notice it, it’s hard to miss it. Kinda like a slug in your garden eating your tomato. 

Slugs are the reason that when you go to your Facebook profile it states `https://www.facebook.com/unique_user_identifer/` instead of `https://www.facebook.com/asdfsdafjka98wr93r8ayefiuhrawr9yere9yfda89fasdf/ `one is much more user friendly and easy on the eyes. While the other is friendly if you couldn’t solve the captcha or can't correctly select all the squaures contain the traffic light. 

To set up a Slug all you need to do is navigate over to your Model and do the following. 

```
class User < ActiveRecord::BASE 

      def slug 

          self.username.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')

     end 	

      def self.find_by_slug(slug)
	         User.all.find{|user| user.slug == slug}
       end 

end
```

I know many may be asking what is that slugging doing. I’m more than happy that you asked. 

This slug is ensuring that all characters are lowercase. It is ensuring that there are no leading or trailing whitespaces, done by adding strip. The first gsub replacing any spaces the user enters with hyphens. The following gsuc removes all non-alpha, non-dash, non-underscore characters meaning only characters a-z and numbers 1-9 will populate. 

Now in the users controller I’d write the following

    get '/users/:slug' do
      @user = User.find_by_slug(params[:slug])
      erb :'users/show'
    end


And with that the url has become a lot more friendly. 

Regex a topic that was viewed and passed as quickly as possible. During my initial contact with Regex I become so confused with this section that I skipped it. It just didn’t make sense at all the first time I came upon it. After going through almost every section of the program I decided to revisit this section that vexed me so much. After learning so much and using Regex on a few occasions for very basic actions I was required to use it for I can say with complete honesty that was and to a certain point still confused by the topic. That being stated I wasn’t as confused as the first time I tried to understand. So that was a plus. 

At it’s basic regular expressions are written between forward slashes / term/. So if in a paragraph the word “going” appears four times then with regular expressions it will be able to find and locate the word. It’s just like using CMD f or CTRL F for a word or phrase. 

The complexiest start arriving when you realize that Metacharacters can be used. Now what exactly are MetaCharacters and that would be a good question since I had the same one the first time I tried these labs. At the core Metacharacteres are just shortcuts. As an example if \S then it will locate any non-whitespace character in the text. While \d will locate in any non-digit in the text. 

No need to fear trying to learn all the shortcuts there are plenty of guides out there with all the shortcuts. And if you will be using them in the future you'll start remembering the ones that you use all the time. 



