---
layout: post
title:      "CLI Constellations - Crash Course "
date:       2019-08-18 23:13:05 +0000
permalink:  cli_constellations_-_crash_course
---



The title of this post "CLI Constellations - Crash Course" is perfect not only for the brief information that is presented about constellations but also how I felt writing the program. This being my first project without any assistance from the ever so helpful rspec tests, that would let me know if I was on the right path and guide me to the right answer. Now I knew from the start that I was going to miss those guided helpful tests but it wasn't until I was right in the middle of my project that I realized just how much they were sorely  be missed. 

Space is something that I find deeply interesting and entertaining so decided that all my projects would be Space theme is some way. Now the basics of my first project was Scraping using Nokogiri a website that has information on Constellations by Month. It wasn't until I had already gotten approval for the site that realized that my scraping would have to be one level deeper than what was required for the project in order to accurately present the information. Though at that point my belief was that was that I should just continue using the site and that after the first two scraps the final Scrap would be much easier due to doing it twice by then. Now while that was true to a certain degree, it wasn't as helpful as I thought it would be.  

Instead of having the required three rb files for this project mine required four. "constellations.rb", "months.rb", "scraper.rb", and the "cli.rb". This was due to the deeper Scrap. One of the more difficult positions I found myself in was in the second to last scrap. 

The first Scrap is only done once right before the class Start method is used that the program reverts back to once a user has looked up the constellation they wanted information about and wish to learn more about other constellations. So the months are only scraped once throughout the entire time the user is looking up information. The issue I came across was that in the Second Scrap after a user wishes to learn more about another constellation, the user would then be presented with not only the new month they have choosen constellations by the previous month's constellation they had chosen as well. The list would keep on growing due to the Constellations Method saving all the previous choices along with the new choices. 

Beginning of CLI

`  def run 
    welcome
    Scraper.months
    list_months
    start
  end`


Right in the middle of CLI

`      def start
    puts ""
    puts "Which months constellations are you interested in learning about?"
    puts ""  
    puts "If you would like to exit please type 'exit'"
    puts ""
    input = gets.chomp 
    if input != "exit"
      new_input = (input.to_i) -1
      if new_input >= 0 && new_input <=11
        Constellations.all.clear
        month = Months.all[new_input]
        list_constellations(month)
      else 
        puts "Not a valid choice plus choose from list"
        list_months
        puts ""
        start 
      end 
    elsif input == "exit"
      exit 
    end
  end `

At this point I had a choice of whether to expand on my code to make sure sure duplicates wouldn't be saved again which would take some time or to another solution. My first thought was using "if @@all already has the information then don't save it. The problem was that this would only solve not having duplicates but not solve for when new months were choosen. After some trial and error realized that the simplest thing to do was to erase the "Constellations.all" before it was Scraped again. By erasing it before it is Scraped again, only the choosen month constellations would be presented would no fear that any duplicates wold be placed in Constellations array. 

One other issue that I had to find a workaround to make sure the code worked accurately was that each months holds different amount of constellations. Had to make sure that if a user picks 7 for month that only had 5 constellations an error would appear but in a different month where it has 8 that 7 would be a valid choice. Decided to create an array that would take in the the element index after the information about the constellations was presented to the user. Then set it so that the input after applying .to_i to ensure it was in integer form was below or equal to array list if not an error would populate. 

```
  def list_constellations(month)
    Constellations.all.clear
    list = []
    Scraper.constellations(month)
    puts "Which constellations are you interested in learning about?"
    Constellations.all.each.with_index(1) do |constellation, index|
      puts "#{index}. #{constellation.official_name}"
      list << "#{index}"
    end 
    inner_input = gets.chomp 
    if inner_input!= "exit"
      new_inner_input = inner_input.to_i 
        if new_inner_input <= list.length
          final_input = (new_inner_input.to_i)-1
          constellation = Constellations.all[final_input]
          print_details(constellation)
```


Not having the rspecs test's was both terrifying and exciting. Not knowing if the code I was writing was going to end up working out, or have to be deleted and started over from scratch. Truth be told that is just want I needed to do on many occassions. At the same time having that control having to come up with solutions by using prior knowledge and help from google that is something that I enjoyed. After finishing this project and even with all the struggles that came in between realized that I was on the right path in my pursuit for not only a better paying job but one I can go into work knowing that I will be smiling when it is all set and done. 
