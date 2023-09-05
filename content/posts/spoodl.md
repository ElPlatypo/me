---
title: "Spoodl"
date: 2023-05-13T09:51:39+02:00
featuredImagePreview: "/videos/mixxx.gif"
featuredImage: "/videos/mixxx.gif"
---

I recently started playing around with a dj consolle as a hobby, i've always listened to a lot of music so i've been curious to try this out for some time.
One thing that i immediately realized is that in order to use any mixing software one needs "phisical" .mp3 (or similar) files, streaming them directly from places like spotify or apple music is just not possible. The problem was that i've been using spotify for many years at this point, so i stopped collecting mp3 files long ago and i needed a way to fix this issue in an easy and automated way, There just arent good tools online to do this task already, and this is why i started working on this project.

# Introducing Spoodl

![Spoodl in action](/videos/spoodl.gif)

Spoodl is a simple python script that aims to solve this very problem, it's use is to syncronize playlists on spotify with a local folder of .mp3 files. To use it, simply copy-paste the link to a spotify playlist on the correct .txt file and Spoodl will start using spotify public API's (This is the reason a spotify developer account is needed, for more info visit https://developer.spotify.com/documentation/web-api) to fetch metadata from every song in the playlist and use that metadata to compile a search query on youtube, find all possible matches on youtube and prompt the user on what version to select, download and convert the selected video to an audio and finally apply all the song metadata gathered from spotify to the correct tags on the .mp3 file.

Each time the script is run it will detect changes done on the spotify playlist and ask the user to delete/download new songs if needed. making sure that the local files are an exact copy of the selected playlists

Check it out on [GitHub!](https://github.com/ElPlatypo/spoodl)

<a href="https://github.com/ElPlatypo/spoodl">
  <img src="/images/spoodl.png" alt="ElPlatypo/spoodl - GitHub" height="90">
</a>