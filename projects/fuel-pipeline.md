---
layout: page
title: Fuel Pipeline
---

The Fuel Pipeline application was built to model fuel consumption and transfer across the UK government’s [fuel pipeline system](https://en.wikipedia.org/wiki/Exolum_Pipeline_System). The application enables users to calibrate storage facility and pipe parameters, modify network priorities, and run comprehensive what-if scenarios. The tool provides critical insights into network operations, helping to optimise fuel distribution and enhance decision-making processes.

![Fuel Pipeline Auto Play](/projects/fuel-pipeline/auto-play.gif)

{::nomarkdown}
<br />
{:/nomarkdown}

## Problem

The Government Pipeline and Storage System (GPSS) is a 2500km network of underground pipes delivering fuel to significant military airfields across the UK as well as civilian airports like Heathrow. Once publically owned, the pipeline is now under private ownership who are contracted by MoD to continue to supply fuel to the connected facilities.

Logistics planners need a way to model the impact of what-if scenarios on the network, such as pipes failing or undergoing periods of maintenance, and facilities having temporary spikes in demand. They also need to find ways to mitigate these impacts and model the time taken for the network to recover.

{::nomarkdown}
<br />
{:/nomarkdown}

## Solution

In just 8 weeks, the team put together a full stack demonstrator application where the user can run long-term simulations end-to-end using a clean and intuitive UI. A subset of publically available real world data was overlaid with synthentic data to produce a representive set of attributes, rates and thresholds for each facility and pipe.

A map component was produced to display this network. All facilities and pipes could be selected, viewed and have high level adjustments made to their base data, as well as calibrations at the day level.

![Fuel Pipeline Auto Play](/projects/fuel-pipeline/calibration.png)

User could also modify the length of time to model and the network priorisation. This data was then fed into a model to calculate the necessary fuel transfers to keep facilities above required thresholds in priority order.

An autoplay feature was added (see animation above) to show the model output as annotations on the map on a day-by-day basis, including facility fuel levels, resupply events and pipe transfer amounts. This model output was also made available as visualisations in the form of a dashboard and a set of reports.

![Fuel Pipeline Auto Play](/projects/fuel-pipeline/dashboard.png)

{::nomarkdown}
<br />
{:/nomarkdown}

## Technical Details

The application was built in the **Remix** framework with a **Node.js** backend and a **PostgreSQL** database. The map component used tiles from **Esri** and components from **React Leaflet**. **MaterialUI** was used for most of the remaining UI components, as well as **Recharts** for charting and **Material React Table** for reports and editable tables.

The model was written in **TypeScript** and embedded in the application running on the Node.js server. The model used [Dijkstra's algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm) for each facility in priority order to iteratively find the next shortest path to another facility that can make a transfer. Optimisation techniques to improve efficiency included caching the results of running Dijkstra's algorithm since the implementation ran in O(n^2) time. The model was benchmarked on a 1x 512MB memory VM as generating a year's worth of data in ~150ms. This efficiency allowed the model to be rerun whenever the user made any data changes, providing immediate feedback.

Tests were written in **Jest** and **Playwright**.

The demonstrator application was deployed to **Fly.io** via **GitHub actions**.
