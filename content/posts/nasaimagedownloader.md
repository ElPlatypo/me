---
title: "Nasa Image Downloader"
date: 2022-05-12T02:34:25+02:00
featuredImagePreview: "/videos/orbit.gif"
featuredImage: "/videos/orbit.gif"
---

This project started a few years ago when I wanted a new animated wallpaper for my desktop, and I fell down the rabbit hole of how to source and group images taken from space.
My research started by looking for high-quality videos that I could directly use, but there didn't seem to be any good ones around. The next best thing I could do was compile a time-lapse of photos taken in succession from space, and luckily for me, the International Space Station, or ISS, has been doing just that for many years.
There is a HUGE database of images that can be publicly and freely accessed over at [jsc.nasa.gov](https://eol.jsc.nasa.gov), but unfortunately, the included search feature was not capable enough to fetch the kind of image sequences I was looking

![Search feature](/images/nid-site.png)

I then whipped up a simple Python script that will first download and build a local copy of the database on the site, but just with image metadata, to save on bandwidth, space, and time. Once the local database is built, the script allows the user to look for sequences of photos of at least a set length and taken at a specific delay from each other, offering to download a preview of the first image to rapidly gauge if the photos were taken at an interesting time.

![Project](/images/nid-proj.png)

This is done because the cameras aboard the ISS arent always rolling, there might be a significant time skip between photos, and because the cameras are not always pointed at the earth, but searching for this kind of sequences was just not possible on the site.

![Previews](/images/nid-previews.png)

Once we select a sequence we like we can easily download it and compile it in a timelapse with the video editing software of choice. \
Here is one of the timelapses I compiled, with the ISS going over central Asia

{{< rawhtml >}} 
    <video width=100% controls loop autoplay>
        <source src="/videos/orbit.mp4" type="video/webm">
        Your browser does not support the video tag. 
    </video>
{{< /rawhtml >}}

The source code is aviable at [GitHub](https://github.com/ElPlatypo/nasa-image-downloader)

<a href="https://github.com/ElPlatypo/nasa-image-downloader">
  <img src="/images/nasa-image-downloader.png" alt="ElPlatypo/nasa-image-downloader - GitHub" height="90">
</a>