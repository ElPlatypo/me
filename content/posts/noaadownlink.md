---
title: "Recieving images directly from satellites"
date: 2023-08-31T17:10:13+02:00
featuredImagePreview: "/videos/noaa.gif"
featuredImage: "/videos/noaa.gif"
---

# Getting images straight from polar orbiting satellites

A while ago while browsing the internet i found out that nowadays, with a cheap software defined radio or SDR and some knowhow, it is possible to recieve signals directly from satellites and actively pull real time data from them.
Space being one of my biggest interests i immediately got to work to find out more on how to do it, and i'm going to report my findings and experiments in this post.

# Theory

As the name might suggest polar orbiting satellites are ones that orbit the earth from nord to south, instead of a more classical orbit around the equator. This is done because while the satellite goes around, the earth spins "horizontally", letting the satellite pass over almost any point on earth in a limited amount of orbits. This allows for example imaging staellites to take new pictures of the entire surface of the earth every few days, and this is exactly the kind of satellite i wanted to pull data from. Here's an old video that explains visually what am i saying:

{{< youtube y_jM_BxQGvE >}} 

Now the specific satellites i am interested to track are the ones operated by [NOAA](https://en.wikipedia.org/wiki/National_Oceanic_and_Atmospheric_Administration), wich beam unencrypted imaging data for anyone to listen and download. Even today most of the weather forecast providers use this system to gather data for their weather models because it is essentially like receiving real-time photos from space, free of charge on top of that. 

As said before NOAA sats are in a polar orbit about 800Km from sea level, and for this reason for someone standing in the same spot on earth they will appear to come up from below the horizon and make an arc in the sky, just like the sun and moon, but from north to south. Theese windows where one can have direct  line of sight with the sat are the ones where their signal is actually receivable and last about 15 minutes each. One way to quickly find out when and where a NOAA sat will pass over your location is using apps like [Look4Sat](https://github.com/rt-bishop/Look4Sat).

NOAA sats transmit mainly two streams of data, a low-resolution low-frequence signal at around 137MHz encoded with a standard called [APT](https://en.wikipedia.org/wiki/Automatic_picture_transmission), and a high-resolution high-frequency signal at 1.7GHz with [HRPT](https://en.wikipedia.org/wiki/High-resolution_picture_transmission), we are interested in the first one since it's the easyest to recive and doesn't need the contruction of a complex tracking antenna. Many tutorials and videos already exist on how to design and build an antenna for correctly receiving an APT signal but it seems that the consensus is that a basic V-shaped dipole antenna will work just fine, i'll leave here a [Post](https://www.rtl-sdr.com/simple-noaameteor-weather-satellite-antenna-137-mhz-v-dipole) that goes more in detail.

The antenna alone isnt enough to recieve radio signals, a software defined radio is also needed to decode the analog radio signal to a digital stream that can be processed by a computer, and one of the reasons i held out for a while before starting this project is because just recently simple kits like an RTL-SDR have become incredibly cheap (about 50 Euros or so). And lastly as far as software goes there are two requrements, something to find and demodulate the recived signal like [SDR++](https://www.sdrpp.org) an open software solution to drive sdr's and something to convert the recieved audio to an actual image, i used [noaa-apt](https://noaa-apt.mbernardi.com.ar).

# Findings

After i got my sdr from amazon i immediatelly used it to scan for frequencies around me with the included antenna and started to familiarize with SDR++, here you can see how easy it is to recieve standard radio stations while near a city

{{< rawhtml >}} 
    <video width=100% controls>
        <source src="/videos/sdr-radio.mp4" type="video/webm">
        Your browser does not support the video tag. 
    </video>
{{< /rawhtml >}}

while exploring other frequencies i came across someone transmitting morse code on a public band:

{{< rawhtml >}} 
    <video width=100% controls>
        <source src="/videos/sdr-morse.mp4" type="video/webm">
        Your browser does not support the video tag. 
    </video>
{{< /rawhtml >}}

I decoded that message as `vvv de ik1fjib b ik1fji b jn44mj jn44mj 10 watts erp kkk` if you have any idea what could it mean let me know!

I live near a city with a big commercial harbour for cargo ships and an airport, by tuning in to the right frequencies it is even possbile to listen to automatic telemetry broadcasts from ships and the chatter of airplane pilots to the control tower during landings and takeoffs.

We're not here for that tho, so after a few attempts i managed to recieve the APT signal i was looking for during a window around 14:00, the signal is incredibly dirty and drowned in noise, you can barely hear the satellite's beeping under the static so it is clear that something wasnt completely right in my setup.

{{< rawhtml >}} 
    <video width=100% controls>
        <source src="/videos/sdr-aptdirty.mp4" type="video/webm">
        Your browser does not support the video tag. 
    </video>
{{< /rawhtml >}}

This beeping was enough to produce this image, there's clearly a lot of noise and italy's barely visible in the photo.
![Noaa-original](/images/NOAA18-20230830-1233.png)

here's the same image but with country borders oerlayed, to see more clearly.
![Noaa-original](/images/NOAA18-20230830-1233-overlay.png)

Nevertheless this was a huge success, i managed to pull my first image drom a satellite! now it was just a matter of refining my setup to better recieve the signal.