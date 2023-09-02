---
title: "Particle simulation"
date: 2023-08-28T11:52:38+02:00
featuredImagePreview: "/images/gridinit.png"
featuredImage: "/images/gridinit.png"
---

This project was part of a course i took at university on physics simulation theory. The goal was to code a program that used montecarlo's alorythms and Markov chains to accurately replicate the real behaviour of a cloud of euqlly charged particles, able to affect up to one-distance neighbours and with continuity conditions at the borders.
I specifically looked at some parameters of the system that described it's behaviour in an intuitive way:

- Total system energy is the first one, if we imagine two particles that repel eachother we can intuitively guess that when we bring those particle close to eachother they will gain a certain amount of potential energy ready to be released as soon as we let them go. We can then calculate the total potential energy of the system as a simple sum of every particle's.

- System order is a parameter that is dependant on the geometry of the system and can assume specific values indicating that the system settled on a base-state of minimal energy. In our case it can be either one of three values, representing the disposition in an hexagonal grix exemplified by the following image.

![base-states](/images/bstates.png)

# Implementation

Since there was no specific language requested to create this program i decided to use this occasion to learn the basics of [Rust](https://www.rust-lang.org/), a modern language that promises to be incredibly fast if coded correctly. 