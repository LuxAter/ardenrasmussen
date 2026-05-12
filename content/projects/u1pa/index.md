---
date: 2025-05-09
title: "Astri"
cover:
    image: 20260508104357.png
---

Astri is a satellite tracking and visualizer. It automatically pulls the list of
all publicly tracked satellites from [CelesTrak](https://celestrak.org/) (as of
writing $\sim 15,000$ satellites). Then using the Simplified General
Perturbations-4 (SGP4) model developed by the United States Department of
Defense (DoD) for predicting satellite position and velocity for any given point
in time.

Astri also includes an interactive user interface, which renders simplified
models for each of the satellites and visualizes their position relative to the
earth and the other satellites. The user interface includes an explorer list for
sorting and filtering the satellites and controlling which ones are displayed.
And it automatically groups satellites into their constellations both in the
explorer list and using the same colors to represent satellites from the same
constellation.

## Satellite Prediction Model

Some of the SGP4 publications provides an implementation of the algorithm in C.
However the included source code is not cross platform (it depends on Windows
specific headers) and doesn't follow modern development standards. I have
re-implemented the SGP4 algorithm in C++ while leveraging more modern practices.
Modifying functions that took $>80$ individual variables to grouping those
variables into data structures or arrays where applicable. Renaming the
mathematically oriented variable names into more descriptive identifiers (e.g.
`argpp` to `arg_of_periapsis`) to make the code more readable.

This reimplementation of the SGP4 algorithm is available as a standalone
library so that it can be reused in any context. And has minimal dependencies
beyond the standard library and a logging library. It implements the required
logic for parsing the TLE (Two-Line Element) sets, and initializing and
calculating the satellite position and velocity for any given point in time.

## Astri Application

{{< video src="https://media.githubusercontent.com/media/LuxAter/ardenrasmussen/refs/heads/main/content/projects/u1pa/20260508104525.webm" >}}

The Astri application is also written in C++ using
[OpenGL](https://www.opengl.org/) for rendering the earth and satellites.
[ImGui](https://github.com/ocornut/imgui) is used for handling and rendering the
user interface. To improve performance the satellites are handled using an
Entity Component System (ECS) [flecs](https://www.flecs.dev/flecs/), and is
easily able to handle the ~50k satellites without dropping frames. 

The application includes a basic camera for orbiting around the earth and
zooming in and out. With keybindings the user can speed up or slow down the
simulation, and increase or shrink the size of the satellite models to make them
easier to see.

And through the builtin explorer list the user can filter and sort the
satellites by their name, or id, and enable or disable the rendering of specific
satellites.
