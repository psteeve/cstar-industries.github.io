---
author: Eric Cestari
title: Deploying a Nitrogen application on Heroku
layout: post
abstract: "The one where Nitrogen applications get deployed on Heroku. With a sample project to start from."
---

##Nitrogen is simple and powerful

Do you know [Nitrogen](http://www.nitrogenproject.com)?
Have a look at the [demos](http://nitrogenproject.com/demos).

Nitrogen is a very elegant way of developping web applications. It is event-based, and seamlessly integrate client side and server side in some smooth erlang/elixir code.

I work on a couple projects currently. One is the usual Ruby on Rails, Angular, CoffeeScript stack like we do now.
The other is Nitrogen + DynamoDB.

On the former, I keep hopping from language to language, framework to framework, enabling one layer to talk to the other.
On the latter, I just write Erlang for both client and server. Nitrogen takes care of the rest. I love that.

Although what I like with Rails is how easily it can be deployed and scaled on Heroku.

I wanted the same for my Nitrogen app.

A quick Google search came up with not much; it was a job I had to do myself!

##Hummmph, that was easy

I wrote a small skeleton project, [cstar/nitrogen-on-heroku](https://github.com/cstar/nitrogen-on-heroku) with Cowboy as the webserver.

1. Pull [cstar/nitrogen-on-heroku](https://github.com/cstar/nitrogen-on-heroku)
2. Write your awesome Nitrogen app
2. Create the Heroku app `heroku create --buildpack git://github.com/archaelus/heroku-buildpack-erlang.git`
3. Push your app to Heroku `git push heroku master`
4. [ET VOILA!](http://fathomless-citadel-5420.herokuapp.com)

## What is remarkable about [cstar/nitrogen-on-heroku](https://github.com/cstar/nitrogen-on-heroku)?

I generated the template from Nitrogen with `make rel_cowboy`, took the generated `site` directory and :

- Added [rebar.config](https://github.com/cstar/nitrogen-on-heroku/blob/master/rebar.config)
- Added [Procfile](https://github.com/cstar/nitrogen-on-heroku/blob/master/Procfile)
- Added [.preferred_otp_version](https://github.com/cstar/nitrogen-on-heroku/blob/master/.preferred_otp_version)
- Changed the supervisor to get HTTP port value from the [environment](https://github.com/cstar/nitrogen-on-heroku/blob/master/src/nitrogen_sup.erl#L33)

Feel free to adapt to your own liking.

Note that deployment fetches and rebuilds all the dependencies. Everytime. I do have a fork of the "official" erlang buildpack which stores deps in the Heroku cache. [Fetch it at your own risk](https://github.com/cstar/heroku-buildpack-erlang), as it's outdated.

Thank you for your visit!



