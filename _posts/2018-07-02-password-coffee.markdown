---
title: password.coffee ☕
layout: post
date: 2018-07-02 11:00:00 -0500
image: /assets/images/
headerImage: False
tag:
- Glitch
- Mapbox
- Netlify
star: False
category: blog
author: cpdis
description: A fast way of showing location-tagged coffee shops on a Mapbox map. The main goal is to have a central repository of SSID and password data.
---
I had a problem. I would go to a coffee shop, maybe [Blacksmith](https://www.blacksmithhouston.com/) or [Morningstar](https://www.instagram.com/morningstarhou/?hl=en), sit down, and realize that somehow I did not have the WiFi password. As I discreetly looked around for the username and password I’d inevitably come to the conclusion that I should just ask the barista as I picked up my drink. Social interaction isn’t the worst thing in the world but it usually results in a finger pointing to a sign, in plain view, that I had somehow missed.

In order to avoid the situation described above I could just keep a running list of places I’ve visited with their associated WiFi networks and passwords. Or I could scour Foursquare for the comment with the password in it (probably from two years ago). Or I could build a single page website with a nice little 🗺 that holds all the information I need.

## Glitch

Glitch was announced back in the December 2016. [Anil Dash](https://anildash.com/) (who at the time had just become CEO of [Fog Creek](http://www.fogcreek.com/)) describes it best:

> Many geeks of my cohort came of age building things on the desktop using HyperCard or Visual Basic, or by using View Source in their browser to tweak HTML pages that they uploaded to Geocities. The web’s gotten a lot more mature and a lot more powerful, but the immediacy of that kind of creation has been lost. Today, even if you’re a skilled developer, the starting point you’re working from is usually a pile of unassembled parts.

> Glitch lets you start from a working app (or bot, or site, or whatever) and then remix it into exactly the app of your dreams.

It’s an excellent place to take someone else’s template and modify it or host a prototype of an idea you have.

![Glitch homepage](/assets/images/30-06-18/glitch_website.jpeg "Glitch homepage")

I chose to remix an existing template that was setup to use [jquery-csv](https://github.com/evanplaice/jquery-csv) and a simple [Mapbox](https://www.mapbox.com/) map.

I added some text, modified the CSS a little, adjusted the size of the map on the page, added extra JavaScript from Mapbox for additional functionality, and populated the map with a decent initial cohort of coffee shops.

![Glitch detail](/assets/images/30-06-18/glitch_detail.jpeg "Glitch detail")

At each step, Glitch automatically updates your site (`insert-whimsical-name.glitch.me`) so you can see what you’re changing in real-time. This removes the headache of setting up a local testing environment and allows you to just build something 💯

## Mapbox

I’ve always been impressed with Mapbox. Like with most of the top-tier internet companies started in the last decade, they’ve taken something would be very difficult for individual developers to implement over and over and simplified it down to a few short code snippets on a web site. In addition, [Mapbox Studio](https://www.mapbox.com/mapbox-studio/) allows anyone to infinitely customize their maps. 

I experimented with several different map styles but ultimately returned to the standard Streets style. It looks most similar to the Google and Apple Maps style and the usability is 👌🏼. 

```js
// Details on the Mapbox API here: https://www.mapbox.com/mapbox-gl-js/api/#map
var map = new mapboxgl.Map({
    container: 'map',
    style: 'mapbox://styles/mapbox/streets-v9',
    zoom: 13
});
```

I wanted zoom controls to overlay the map. Zooming in and out of a map on a mobile webpage is sometimes a little difficult and controls alleviate this slightly.

```js
// Add zoom and rotation controls to the map.
var nav = new mapboxgl.NavigationControl();
```

In case the map is not automatically centered on the user, a geolocation button was also added.

```js
map.on('load', updateGeocoderProximity); // set proximity on map load
map.on('moveend', updateGeocoderProximity); // and then update proximity each time the map moves

function updateGeocoderProximity() {
// proximity is designed for local scale, if the user is looking at the whole world,
// it doesn't make sense to factor in the arbitrary centre of the map
    if (map.getZoom() > 9) {
        var center = map.getCenter().wrap(); // ensures the longitude falls within -180 to 180 as the Geocoding API doesn't accept values outside this range
        geocoder.setProximity({ longitude: center.lng, latitude: center.lat });
    } else {
        geocoder.setProximity(null);
    }
}

// Add geolocate control to the map.
var geo = new mapboxgl.GeolocateControl({
    positionOptions: {
        enableHighAccuracy: true
        },
        trackUserLocation: true
      });
```

Finally, I added a search box because I would expect that on any map that I’m viewing. In the future I would like to add driving or walking directions from the current user location ☑️

```js
// Add search box
var geocoder = new MapboxGeocoder({
   accessToken: mapboxgl.accessToken
});
```

## Netlify

I bought the [password.coffee](https://password.coffee) domain on [Google Domains](https://domains.google) early on and knew that I wanted to eventually move off of Glitch. I briefly considered hosting on [Linode](https://linode.com) but decided the easiest route was using Github as the server. It’s relatively simple to set up a custom domain using Github Pages but there are always a few quirks.

I don’t know when I first came across [Netlify](https://www.netlify.com/) but for whatever reason I came back to it for this. It was far better, faster, and easier than I remembered. Provided you have all the necessary files to build a functioning website, the process of setting up continuous deployment takes under a minute. Really incredible for a site hosted on GitHub, Gitlab, or Bitbucket.

It takes three screens to get set up. You connect your Github (in my case) account and choose the correct [repository](https://github.com/cpdis/password-coffee).

![Choose repository for site](/assets/images/30-06-18/new_site_netlify.jpeg "Create a new site on Netlify")

Then you select any build options, like `jekyll build` for Jekyll, and click *Deploy Site*.

![Deploy site ](/assets/images/30-06-18/deploy_site_setup_netlify.jpeg "Deploy site using Netlify")

It took just a few more minutes to setup the custom domain, change nameservers, and enable HTTPS by default. Most of that time was waiting for DNS to propogate.

## End

Overall, I'm pretty satisfied with this first iteration. If you'd like to check it out, just go to https://password.coffee. And if you want to update an existing location or add a new one you can do that [here](https://passwordcoffee.typeform.com/to/tXXeRP).