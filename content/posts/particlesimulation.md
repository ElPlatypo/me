---
title: "Particle simulation"
date: 2023-08-28T11:52:38+02:00
featuredImagePreview: "/images/gridinit.png"
featuredImage: "/images/gridinit.png"
---

This project was part of a course I took at university on physics simulation theory. The goal was to code a program that used Montecarlo's algorithms and Markov chains to accurately replicate the real behavior of a cloud of equally charged particles, able to affect up to one-distance neighbors and with continuity conditions at the borders.
I specifically looked at some parameters of the system that described its behavior in an intuitive way:

- Total system energy is the first one. If we imagine two particles that repel each other we can intuitively guess that when we bring those particles close to each other they will gain a certain amount of potential energy ready to be released as soon as we let them go. We can then calculate the total potential energy of the system as a simple sum of every particle's.

- System order is a parameter that is dependent on the geometry of the system and can assume specific values, indicating that the system settled on a base state of minimal energy. In our case, it can be either one of three values, representing the disposition in a hexagonal grid exemplified by the following image.

![base-states](/images/bstates.png)

# Theory

The objective is to evolve a system of particles that move randomly, and for a given number of particles we can define N states that represent any possible configuration of particles in the system. given {{< raw >}}\(P^{0}\){{< /raw >}} a state at the timestep 0 and {{< raw >}}\(\Pi\){{< /raw >}} the matrix that contains any possible future state starting from the current one we want a system that evolves like:

{{< raw >}}\(\lim_{m\to\infty} P^{(0)}\Pi^m = P^{eq}\){{< /raw >}}

Where {{< raw >}}\(\Pi\){{< /raw >}} must be [ergodic](https://en.wikipedia.org/wiki/Ergodicity):

{{< raw >}}\((\Pi^m)_{ij} > 0 \textrm{   e   } (\Pi^n)_{ji} > 0\){{< /raw >}}

wich basicly means that from any given state i we can reach any other state j

It must also be Aperiodic:

{{< raw >}}\(\Pi_i = 1 \textrm{ wich means } \Pi_{ij} = 0 \textrm{ for any } i \not = j\){{< /raw >}}

Given theese conditions we can model our system so that:

{{< raw >}}\(P^{eq}_i = \alpha e^{-\frac{E_i}{K_bT}}\){{< /raw >}} 

Where {{< raw >}}\(\alpha\){{< /raw >}} is a constant, {{< raw >}}\(E_{i}\){{< /raw >}} is the energy at the current configuration, {{< raw >}}\(K_bT\){{< /raw >}} is a parameter that controls that disorder predesposition of the system, we can manually change this parameter to observe how easily the system can reach a locally-ordered state.


# Implementation

Since there was no specific language requested to create this program i decided to use this occasion to learn the basics of [Rust](https://www.rust-lang.org/), a modern language that promises to be incredibly fast if coded correctly. 

It didnt disappoint, i originally started working on a python implementation but when i switched to rust i immediately noticed a 10-100x improvement on execution time, so i was satisfied with my choice and i decided to press on. A more in depth look at the implementation can be found in the GitHub [page](https://github.com/ElPlatypo/particle-simulation)

For a more detailed look at the code you can check out the source code on [GitHub!](https://github.com/ElPlatypo/particle-simulation)
<a href="https://github.com/ElPlatypo/particle-simulation">
  <img src="/images/particle-simulation.png" alt="ElPlatypo/particle-simulation - GitHub" height="90">
</a>

# Results

Once the program was done i run some tests to see if everything worked correctly. Here you can see a plot of the total enegy of the system over time.

![Energy](/images/energy.png)

Its clear how the system initially moves very quickly to a lower energy state and then it becomes harder and harder to find a global minimum, so it continually gets stuck in local minimi.

If we instead look at the order parameter we can see how after some initial instability the system settles on a specific base-state and sticks to it.

![Order](/images/order.png)

One of the more interesting thing to observe tho is how easily the system reaches an ordered state depending on the {{< raw >}}\(K_bT\){{< /raw >}} parameter:

![Betaj](/images/betaj.png)

This image contains a batch of different runs, each encoded with a color from blue to red. We can easily see how the system is able to reach an ordered state (indicated by one of the 3  possible sub-states per run reaching a value close to 1 and the other 2  going to 0) only when we set a {{< raw >}}\(K_bT\){{< /raw >}} (or betaj) value greater than 2.9, wich reflects it's real life counterpart, signifying that a correct abstraction of reality was achieved in the program.