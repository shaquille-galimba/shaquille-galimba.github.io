---
layout: post
title:      "Mondex! CLI data gem project"
date:       2020-03-15 08:39:11 +0000
permalink:  mondex_cli_data_gem_project
---


Hey guys! So, I'm now a month into my web-development online boot camp and I just finished my first portfolio project. I hope I intrigued you with the name of my application even if it's not really that interesting. I'm really proud of having to come up with this idea because I think it shows a little bit about me. As I stated on my first blog, I'm a gamer and this application that I made is for gamers who plays a specific game.

My gem is called "Mondex" because it's a "Pokedex" but for Monster Hunter bosses! Lame name, I know, but I'm really proud of it. It is like a pokedex in a sense that it gives you details about a certain Monster Hunter boss and that's about it lol. No, it didn't have the sounds that a boss make or even a picture of the monster because, well it's a data gem. The application will give the user a monster's species, locations, weakness, resistances, elements, and description.

**The process**

*Planning*

So, how did I really come up with the idea of making this gem? First, I just want to say that the planning phase is the second most time-consuming part of the project, the first one is scraping of course. It is time-consuming because I feel like there's a lot of ideas in my head that none of them is actually popping out. However, after taking a day off of programming just to relax my mind a little bit and just play my games, I actually got the opposite. I ended up being frustrated because of losing, but that gave me the idea to make a gem that could resolve one of my frustrations before in a game, that game is "Monster hunter" (this game was different from the game that I just lost that time). I will explain how the game frustrates me and how did I possibly solved it with this project.

*Classes*

* CLI
* Scraper
* Monster
* Species

*Scraping*

Now, the horror begins, SCRAPING. However, I just want to say that making a skeleton app is quite hard too if it is your first time making a gem(which is the case for me), but there's a lot of videos that Flatiron provides to help me with that. Back to scraping! First, I spent 4 hours scraping the first website that I saw that has the list of all monster hunter boss only to found out that the individual page for each monster is inconsistent with one another that it's nearly impossible to scrape it. So, I searched for another website because I'm all in on this idea, and found a better one. It has it's inconsistencies but I managed to get around it using string methods. Here is the code for scraping the attributes of the monster instances: 
```
def self.scrape_monster_page(url)
    monster = {}

    monster_page = Nokogiri::HTML(open("https:" + url))

    monster[:bio] = monster_page.css("#wiki-content-block blockquote p").text

    monster_box = monster_page.css("div.infobox .wiki_table tr").children.map {|el| el.text.strip}.reject {|c| c.empty?}
    monster_box.each_with_index do |title, idx|
      if title == "Location(s)" || title == "Locations"
        monster[:locations] = monster_box[idx+1]
      elsif title == "Species"
        monster[:species] = monster_box[idx+1].delete_suffix("s")
      elsif title == "Elements"
        monster[:elements] = monster_box[idx+1]
      elsif title == "Weakness" || title == "Weaknesses"
        monster[:weakness] = monster_box[idx+1].gsub(/[(][A-Z]/, "(w").gsub("\u00e2\u00AD\u0090", "*").gsub("\u00A0", "").split /(?=[A-Z])/
      elsif title == "Resistances"
        monster[:resistances] = monster_box[idx+1].gsub(/[(][A-Z]/, "(w").gsub("\u00e2\u00AD\u0090", "*").gsub("\u00A0", "").split /(?=[A-Z])/
      end
    end

    monster[:species] = monster_page.css("#wiki-content-block ul li").find {|t| t.text.include?("Species")}.text.split(": ")[1].delete_suffix("s") unless monster[:species]

    monster
  end
```

See that it has a lot of String#gsub methods because some of the text are actually symbols that cannot be read by the terminal or at least I don't yet know how to make the terminal read it.

*Class methods, attributes, and relationship*

The CLI class is responsible for interacting with the user so I had to require the 'colorize' gem so that it would be eye-pleasing at least. Also, it calls for my Scraper method to create Monster instances and add attributes to it. While adding the :species attributes to a monster instance it also makes a relationship to the Species class by creating an instance of a species and adding itself to the @Monsters instance array of the instance. Here's the actual instance method of the Monster class that adds attributes to it from a hash of attributes returned by another method from Scraper class.

```
def add_attributes(hash)
    hash.each do |attribute, value|
      if attribute == :species
        new_species = Mondex::Species.create_or_find_by_name(value)
        self.send("#{attribute}=", new_species)
        new_species.monsters << self
      else
        self.send("#{attribute}=", value)
      end
    end
    self
  end
```

**The project**

*Frustration from earlier*

I promised to explain why a certain frustration from another game lead me into making this gem, here it is. When I was only started playing Monster Hunter, I have no idea what elements I should use to effectively beat a monster that I was facing for the first time because the game only gives you its details after you beat it a number of times. That frustrates me because fighting a monster while having a random weapon with a random element for the first time, takes a lot of time! Of course I could have searched for it in the web, but this gem gives you the 'deetz' of all monster hunter bosses with less time than the website (atleast, that's what I've been telling myself) Also, this application also gives you a list of all the species and all the monsters belong to a specific species, which the actual game doesn't. This species list option helps players to quickly know what monster to fight to complete their quest, usually I have to search for a certain species on the web and search for what monster has that species because the game only tells you "Kill/Capture a Bird Wyvern" and not give a list of monsters, which would not really help if you're just starting.

*Demonstration*

After all the debugging, cleaning, and refactoring. I now have the chance to enjoy the first application that I made from scratch. Here's a link of my video demonstration of how the application works:

https://youtu.be/cPy2M6YInd0

Overall, I was really proud that I made this gem because this shows me how much I understand all the lessons I've done so far and I'm really looking forward for the next challenges and knowledges the boot camp will give me. I hope you're all doing great and let's get it!
