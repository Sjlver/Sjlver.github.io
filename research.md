---
layout: page
title: Research
permalink: /research/
---

I completed my PhD at the [Dependable Systems Lab][dslab], under the supervision
of George Candea.

My work focused on *Elastic Program Transformations:* flexible techniques to
increase the reliability of software. This [30-minute talk][ept_talk] gives an
overview of Elastic Program Transformations and their applications.

[Publications](https://scholar.google.ch/citations?user=NnX4nLIAAAAJ) |
[CV](https://blog.purpureus.net/assets/documents/cv_jonas_wagner.pdf) |
[three-minute video overview of my research](https://www.youtube.com/watch?v=h5z7BBbvPK0)

Research Interests
------------------

My aim is to *build tools that help developers create better software.* My
projects automatically transform programs to make them more secure, and help
developers discover unexpected inputs that cause their programs to crash. I want
my work to handle both the scale and the performance requirements of large
programs, and I evaluate it on real-world software systems.


Projects
--------

During my PhD, I built FUSS, a technique to test programs with randomly
generated inputs, and quickly find those inputs that trigger bugs in the
software. Key to its success is FUSS's ability to obtain feedback from the
program without unnecessarily slowing down the testing process.

I am the main author of ASAP. This project empowers developers to use the
instrumentation tools they love &mdash; data race detectors, memory safety
enforcement, tracing and logging tools &mdash; without suffering from high
performance overhead. [ASAP is free software][asap].

Previously, I have worked on automatic bug finding. I have explored how
information from static program analysis can improve dynamic symbolic
execution. For example, I found that choosing the right program transformations
at compile-time can make symbolic execution an order of magnitude faster, and
so I developed the [<span style="font-variant: small-caps;">-Overify</span>][overify]
compiler flag that optimizes software for verification and bug finding.


Biography
---------

I did my PhD at the [Dependable Systems Lab][dslab] at EPFL, researching tools
for software developers. During my PhD, I spent one summer as an intern at
[Google](https://google.com/), analyzing security vulnerabilities in Android
apps. In 2011, I obtained a Master's degree in Communication Systems from EPFL.
My master thesis on measuring the performance of VPN tunnels was developed at
[Open Systems AG](https://open.ch/). During my studies, I was an intern at
MadeinLocal.com and [Bucher &amp; Suter AG](https://www.bucher-suter.com/), and
spent an exchange year at NTU in Singapore.

[dslab]: https://dslab.epfl.ch/
[ept_talk]: https://www.youtube.com/watch?v=G_sYs5evS-g
[asap]: https://dslab.epfl.ch/research/asap/
[overify]: https://infoscience.epfl.ch/record/186012/
