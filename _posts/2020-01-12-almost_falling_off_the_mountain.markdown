---
layout: post
title:      "Almost Falling Off The Mountain"
date:       2020-01-12 19:25:56 +0000
permalink:  almost_falling_off_the_mountain
---


My Rails Applications is titled Conquering Mountains and in the process of finishing it I was almost knocked out off the mountain. While the applications is pretty straightforward in that it lets logged-in users add Climbers, Mountains, and Climbs to the database. While also connecting the Climbers to the Mountains through Climbs the number of little errors that came up while I was building it caused me to go back to more previous lessons more google searches than in the previous two projects combined. I was going over previous labs to try to find answers and while in the lessons and labs with similar situations it would work with my app it was not. 


The connection between Climbers and Mountains 

Climbers/views/_form.html.erb 
```
    <p> First Mountain Conquered </p> 
    <div class="field">
        <%= f.collection_check_boxes :mountain_ids, Mountain.all, :id, :name %>
        <br>
        <%= f.fields_for :mountains, @climber.mountains.build do |mountains_fields| %>
            <%= mountains_fields.text_field :name %>
        <% end %>
    </div

```

In my application during the initial set up for a climber, my application asks for the first mountain the climber has conquered. The user is then allowed to either choose from the list of mountains that have added before by clicking the checkbox or add a new mountain that has not been conquered before. Both of the methods required additions to both the Climber Controllers and Climber Model. 

In my Climber Controller for the climber_params that are used to create and update the climbers the following params were used to ensure that both methods would yield the mountain being saved. 

```
        def climber_params
            params.require(:climber).permit(:name, :age, :experience,:date_started, mountain_ids:[], mountains_attributes: [:name])
        end 

```

The mountain_ids[] are used for the f.collection selection when the mountain has previously been entered.  While the mountains_attributes: [:name] is used when the mountain name has not been entered before. 

Under the model/climber.rb “accepts_nested_attributes_for :mountains” also needs to be added to make sure that new mountains are saved correctly. In addition, also under model/climber.rb the following code was also added to make sure that no duplicates mountains were added. 

```
    def mountains_attributes=(mountain_attributes) 
        mountain_attributes.values.each do |mountain_attribute|
            mountain = Mountain.find_or_create_by(mountain_attribute)
                self.mountains << mountain
        end 
    end 

```

The key thing I took from this project is just how connected all aspects are connected to one another. The reason I was had such a difficult time with this project was that it was so connected. All the errors were stemming from errors that I was making in different areas and then trying to fix them in the incorrect area. So while the code was right I was thinking it was incorrect resulting in me changing the code around making the code in another area fail. It was a very frustrating process. Though this taught me to really understand the code to a higher level much more than I did at the start of the project. So while it is true that this project pushed me greatly, the learning I did while struggling is not something that I will easily forget. 

In conclusion, if anybody is reading this before the start of their Rails project one piece of advice I can offer is that you really make sure you understand how connected everything is to one another and to take things one step at a time. To not get overwhelmed and start changing everything when the solution might be much easier than previous anticipating.  

