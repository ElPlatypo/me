---
title: "Spoodl"
date: 2023-05-13T09:51:39+02:00
featuredImagePreview: "/videos/mixxx.gif"
featuredImage: "/videos/mixxx.gif"
---

I recently started playing around with a DJ console as a hobby. I've always listened to a lot of music, so I've been curious to try this out for some time.
One thing that I immediately realized is that in order to use any mixing software, one needs "physical" .mp3 (or similar) files, streaming them directly from places like Spotify or Apple Music is just not possible. The problem was that I've been using Spotify for many years at this point, so I stopped collecting mp3 files long ago, and I needed a way to fix this issue in an easy and automated way. There just aren't good tools online to do this task already, and this is why I started working on this project.

# Introducing Spoodl

![Spoodl in action](/videos/spoodl.gif)

Spoodl is a simple Python script that aims to solve this very problem. Its use is to synchronize playlists on Spotify with a local folder of .mp3 files. To use it, simply copy-paste the link to a Spotify playlist on the correct .txt file, and Spoodl will start using Spotify public APIs (this is the reason a Spotify developer account is needed, for more info, visit https://developer.spotify.com/documentation/web-api) to fetch metadata from every song in the playlist and use that metadata to compile a search query on YouTube, find all possible matches on YouTube and prompt the user on what version to select, download and convert the selected video to an audio, and finally apply all the song metadata gathered from Spotify to the correct tags on the .mp3 file.

Each time the script is run, it will detect changes made to the Spotify playlist and ask the user to delete or download new songs if needed. Making sure that the local files are an exact copy of the selected playlists

Check it out on [GitHub!](https://github.com/ElPlatypo/spoodl)

<a href="https://github.com/ElPlatypo/spoodl">
  <img src="/images/spoodl.png" alt="ElPlatypo/spoodl - GitHub" height="90">
</a>