---
layout: post
title:      "Partials sometimes slow your web application."
date:       2020-08-21 06:36:13 -0400
permalink:  partials_sometimes_slow_your_web_application
---

I was developing my Rails project for Flatiron School and the app I choose to make requires me to render a list of recommendations and I want that list to be used by more than one route. The obvious solution is to make a partial of a recommend template and iterate through various recommends collection and render the partial for each recommend, but then I learn that using partial to render a collection only slows down my application because for every iteration it will open and close the partial, which takes some time apparently. Here's how I came up with a very under-my-nose solution, but first let me tell you about the project first.

## The project

I made this application thinking that there are already a lot of recommendation app, but only for a specific category like Yelp for restaurants or IMDB for movies and shows. That's where I got my idea that "what if I made a recommendation app where users can make their own category?". This app gives its users freedom to recommend on anything they think of, may it be a movie, book, or specific ones like Dungeons and Dragons play show. You can try the app here [Recommend](https://shaq-recommend.herokuapp.com/)

## Band-aid remedy

First, here's a snap of the list of recommendation I've been talking about.

![recommend-list](https://ibb.co/NF93DDC)

I search for solutions with this problem and I learned that you can actually pass a collection to a partial via the :collection option, and the partial will be inserted once for each member in the collection. Source: [Layouts and rendering](https://guides.rubyonrails.org/layouts_and_rendering.html#using-partials)

- index.html.erb

	 	<h1>Products</h1>
		<%= render partial: "product", collection: @products %>

- _product.html.erb

		<p>Product Name: <%= product.name %></p>

at first I thought it was a good fix for my problem but after looking at the logs, the partial opens just once for the collection but somehow still takes the same time as opening and closing it with each iteration.

## The solution

Like I said, the solution is very under-my-nose and that is to just not use partials and just accept that I cannot refactor a code even if it exist in more than one view, for the sake of a fast web application.

## Conclusion

In a small project it still could be viable to use partials when iterating a collection but imagining it in a larger project, I thought it's best practice to just iterate over the collection through your views and not open and close a partial while doing so.

