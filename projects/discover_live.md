---
layout: page
permalink: projects/discoverlive/
title: Discover Live
tagline:
tags: []
modified: 06-12-2018
image:
  feature: discover_live_banner.png
---


Discover Live is a Music Discovery Service that helps connect people with upcoming concerts in their area. The concept of an app telling you when the bands you like are coming to town has been beaten to death by BandsInTown, Spotify, and more. But have you ever felt the desire to go to a concert this weekend but you scroll through a list of who's playing and haven't heard of any of them? Head over to [Discover Live](http://discoverlive.speal.ca) to automatically generate a Spotify playlist of the bands playing near you this week. Listen to it while you're in the car, going for a run, or otherwise passively listening, and if you discover something you love you can head to the show!

## How it works

The application is mostly a backend service built using Python and Django. It uses the [Eventful API] to search for upcoming concerts in a particular area and gets back a list that is way too long, containing concerts and all sorts of other events. For each event title, we search Spotify as if it's an artist and discard the events for which there is no match. For matching artists, Spotify allows us to look up list of their most popular songs. Our users authenticate with Spotify (using Oauth2), and grant us access to create a new playlist in their account with all these songs.

The first implementation of this workflow made it clear that the process was I/O-constrained. Many hundreds of API requests to Eventful and Spotify need to be made in order to populate a playlist, and this originally took several minutes. I used Redis to parallelize these requests and websockets to provide realtime feedback to the user as concerts, artists, and eventually songs accumulate.

The source code for the [front-end](https://github.com/nickspeal/musicthisweek-client/) and [back-end](https://github.com/nickspeal/musicThisWeek/) is available on GitHub.

#### [Check out the app here!](http://discoverlive.speal.ca)
