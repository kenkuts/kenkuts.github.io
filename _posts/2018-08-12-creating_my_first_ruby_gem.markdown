---
layout: post
title:      "Creating my first ruby gem"
date:       2018-08-13 00:53:09 +0000
permalink:  creating_my_first_ruby_gem
---


For this project I have created a rubygem that lets you search for your favorite artists touring schedule or [`gigs`](https://rubygems.org/gems/gigs). 

The website that I scraped the info from is [bigstub](http://bigstub.com). I used ```nokogiri``` as my scraper and ```selenium-webdriver``` as my webdriver in case I have to scrape javascript renedered HTML. I also used ```colorize``` to make my CLI look colorful. 

When I first started my project I was having difficulty understanding why when I scraped a certain band I could not get any of thier information. When I would scrape blink 182's ticket page there would be no issue but when I scraped modest mouse ticket page I couldn't get anything. This is after verifying that the elements that I was scraping did exist and were on the webpage. I asked around some forums and found out that the reason my scraper was not doing its job was because the modest mouse ticket page was `javascript` rendered. Meaning that the contents of certain pages would need to wait at least a second or two before all its elements could be rendered and put into place.

This is where ```selenium-webdriver``` comes in. ```selenium-webdriver``` lets you automate web browsers and lets you test and verify if your aplication is working. For the purpose of my project I only used ```selenium``` to open up a ```headless``` web brower to let javascrip rendered elements load up. After the js elements gets rendered the brower closes and the ```page_source``` or HTML for that rendered page gets  parsed by nokogiri. If the element cannot be found for a certain artist after about 5 seconds the program closes the browser and throws an exception telling us that the artist, band or dj is not touring or it doesn't exist.  

After solving my initial issue everything was downhill from there. I created my classes with different attributes that relate to other classes. The ```concert``` class has different attributes such as `input`, `artist`, `venue` and `date`. The `input` attribute is to keep track of which concert event the other attributes belonged to. Sometimes the data we get doesn't correspond to the user input an example would be if a user looks for the artist kaskade. Kaskade's tour dates pop up but some of his events is where he performs at festivals. This gives our `artist` attribute the festival name instead of `kaskade`. So for this problem I created the `input` attribute where the program saves the users searched artists and assocaites that `artists` attribute with them regardless if the `artist` attribute is a festival or an event. This also keeps track of the artists that the user has searched for.

Now comes the fun part the `CLI`. I enjoyed creating the `CLI` for this gem mainly because of the colorful `colorize` gem. I used the color `cyan` to signify instructions, `red` for errors and `red` `white` and `blue` for the artist, venue and date. 

# Conclusion
Overall I enjoyed the learning experience. I enjoyed learning how to create a `headless` running browser with `selenium-webdriver`.

I do have some things that I would like to improve on this gem especially with the user input on searching for an artists. One good example would be a form of input manipulation. If a user was looking to see if "j.cole" was touring or not I would implement `regex` to change the `.` into a `-` so that it could be interpolated into the website link to search for `j.cole`. 

