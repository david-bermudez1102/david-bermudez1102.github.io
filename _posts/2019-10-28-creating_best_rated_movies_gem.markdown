---
layout: post
title:      "Creating Best Rated Movies Gem"
date:       2019-10-28 21:40:06 -0400
permalink:  creating_best_rated_movies_gem
---




The idea of this gem is to help users to check the best top rated movies by genre/year based in Rotten Tomatoes score with all of their details, like genre, year, score, description and who directed the movie.

If user wanted to see Today's Best Rated Movies, they would just type "today" and the program would just scrape through https://www.rottentomatoes.com/browse/cf-in-theaters/ and get all the information from there.

When user wanted to see a specific genre, we'd have to scrape the website fo that specific genre. Unfortunately, I wasn't able to find a a page in rotten tomatoes where all movies were listed, but I made sure to only scrape the site when user requests that specific genre.

I started by creating my gem with `bundle gem list_best_rated_movies` then adding two classes to the lib folder `Movie` and `Genre` which have a `Memorable` module in concerns. A Movie can have many genres and a Genre can have many movies.

Once I created all the appropriate methods for those two classes, I created the Scraper class to scrape all the data I needed for the program to work.  Then I created my class to list Today's best rated movies. I called it CertifiedFresh since it is how Rotten Tomatoes calls it.

I made my scraper methods as simple as possible, then I started adding some abstraction.

## Time to start building my CLI!

This is where the fun part came! It was already time to start playing with the classes I created.

First, I initialized the class by instanciating two new objects: 
```
        @scraper = ListBestRatedMovies::Scraper.new # This variable calls my Scraper class
        @genres = @scraper.scrape_genres #This scrapes the genres and save them in the Genre class
        @certified_fresh = ListBestRatedMovies::CertifiedFresh.new # This variable calls my CertifiedFresh
```

Then I create the method `call` where I welcome my user, then `list_genres`  which is where I show the genres I stored in the Genre class at the beginning and prompt user to input a valid genre. You can go ahead and download my gem at https://github.com/david-bermudez1102/list-best-rated-movies-cli-gem.

So far, everything looks like this:

![](https://i.imgur.com/5YIaLCZ.png)

Check out my Youtube video https://youtu.be/wItLM9_F-Dc to know more about this gem!




