---
title: IBSLover1.0
date: 2024-04-01 19:56:46
categories:
  - App Develop
tags: 
  - React
  - React Native
  - Google Maps API
---

Now all the basic features of this app are fully developed. Here are some instructions on how to use this app.

## Basic UI

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/simulator_screenshot_C229F6C0-7C25-4E9E-8B58-0CECC126A0AA.png" alt="simulator_screenshot_C229F6C0-7C25-4E9E-8B58-0CECC126A0AA" style="zoom:25%;" />

## Features

### PANIC! — Find the Nearest Toilet

By clicking this button at the bottom, your map will quickly navigate you to the nearest toilet (currently only searched by the Google Maps API, without user-created positions).

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401201458130.png" alt="image-20240401201458130" style="zoom:33%;" />

After clicking:

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401201525864.png" alt="image-20240401201525864" style="zoom:33%;" />

### All Places with Toilets Shown on Map

All of the places with toilets nearby will be displayed on the map.

- A red marker indicates the location has been queried by the Google Maps API, which is usually more precise.
  ![ToiletMarker0](https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/ToiletMarker0.png)

- A blue marker indicates the location has been added by a user with an associated vote count.
 ![ToiletByUser](https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/ToiletByUser.png)

Clicking on these markers will provide detailed information about the location.

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401201130130.png" alt="image-20240401201130130" style="zoom:33%;" />

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401201150359.png" alt="image-20240401201150359" style="zoom:33%;" />

You can select `Click to navigate` to get directions to the chosen location, similar to using the `PANIC!` feature.

### ListView

Users can opt for a list view to see places with toilets. The list can be hidden if not needed. The places are sorted in ascending order of their distance from the user.

Showing the list -> Hiding the list:

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401200256391.png" alt="image-20240401200256391" style="zoom: 33%;" />

Hiding the list -> Showing the list:

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401200314839.png" alt="image-20240401200314839" style="zoom:33%;" />

Clicking an item in `ListView` will yield the same result as selecting the location directly.

### Current Location

This feature allows users to return to their current location on the map if they lose track of where they are.

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401200607890.png" alt="image-20240401200607890" style="zoom:33%;" />

After clicking:

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401200629314.png" alt="image-20240401200629314" style="zoom:33%;" />

### Add Toilet

Users can add a new toilet location, making it public to all users. Some measures have been taken to ensure accuracy. When adding a new location, if it's close to an existing one on the toilet list, it will be considered the same location, and the vote count will increase by one. The user's position is added to the toilet list, and the location is updated to the **average position** of all contributors. Currently, `Name` and `Description` are not being utilized effectively (That's probably not a good solution, I'm still figuring how to make this better, maybe adding that to DB as well and even voting for the Name??? that's a little bit insane).

Adding a toilet that is already on the list:

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401202551791.png" alt="image-20240401202551791" style="zoom:33%;" />

Before adding:

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401202857205.png" alt="image-20240401202857205" style="zoom: 50%;" />

After adding (voting):

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401203035773.png" alt="image-20240401203035773" style="zoom:33%;" />

### Filters

Users can apply two types of filters to streamline their search:

#### General Filter

- Exclude specific locations from the map display by selecting them in the filter settings.

#### Voting Count Filter

- Set a minimum vote count threshold to assess the reliability of a toilet location.
- Locations with a vote count below the threshold will not appear in the search results.

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401203229720.png" alt="image-20240401203229720" style="zoom:33%;" />

Before filtering:

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401203309545.png" alt="image-20240401203309545" style="zoom:33%;" />

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401203326784.png" alt="image-20240401203326784" style="zoom:33%;" />

After filtering:

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401203356523.png" alt="image-20240401203356523" style="zoom:33%;" />

### Refresher

A simple refresh function—nothing special to mention here.

### Toggle Bar

A toggle bar contains all the features listed above for easy access.

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401203600125.png" alt="image-20240401203600125" style="zoom:50%;" />

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401203616666.png" alt="image-20240401203616666" style="zoom:50%;" />

## Limitations

### Location accuracy

Location accuracy issues have been noted on real iPhones, particularly with Expo's location services in China. Various platforms, including StackOverflow and GitHub, have not provided solutions that address this issue. It appears that Expo's location services may not be reliable in China, which has hindered testing on an actual iPhone.

On my iPhone 11 (not accurate):

<img src="/IMG_7165.PNG" alt="IMG_7165" style="zoom:33%;" />

On a simulator iPhone 15 (accurate):

<img src="https://github.com/xxLovy/BlogRepo/blob/main/HexoBlog/source/img/image-20240401204820793.png" alt="image-20240401204820793" style="zoom:33%;" />

### Incomplete Keyword Range

The current compendium of keywords is somewhat limited, only enabling the query of certain likely toilet locations. This decision was taken to conserve the number of queries made to the Google Maps API, with an eye to efficiency and cost-effectiveness. Future updates are expected to broaden this keyword list.
