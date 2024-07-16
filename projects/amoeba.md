---
layout: page
title: Amoeba
---

The Amoeba application was built to generate air and maritime isochrones from any point on Earth. An isochone is a boundary line representing the threshold of the maximum distance that can be reached from a starting point in a fixed amount of time. The application enabled users to add no fly/sail zones and to open/close canals to see the impact on the isochrones generated. The output fed decision making in an operational scenario at a high-level.

![Satelitte View](/projects/amoeba/anti-access-zones.png)

## Problem

The mercator projection of the world map can lead to misconceptions about the sizes of and distances between certain parts of the earth. For example: Greenland on a standard world map appears the same size as the continent of Africa, though it is actually nearly 15 times smaller; Iceland is closer as the crow flies to Alaska than it is to Cyprus, since the flight path crosses the North Pole which is heavily distorted and cropped on a map.

Additionally the irregular shape, size and distribution of land masses can make a journey many times longer than the line as the crow flies, for example the sailing distance from the Strait of Gibraltar through the North Sea to the coast of Norway is shorter than it is through the Mediterrean to the Black Sea. No fly/sail zones, such as in times of war or conflict, and the closure of canals can alter journey times drastically, as was seen in recent times during the 2021 Suez Canal obstruction.

In stratetic operational planning and wargamming it is a common requirement to model journey times in what-if scenarios. It is also a common requirement to position a strategic base such as a hospital at a roughly equal journey time to all other bases in theatre.

## Solution

In 3-4 months the team put together a fullstack demonstrator application with rapid isochrone generation for air and sea. Users could pick a starting point on a fullscreen map, input a speed and one or more durations, and quickly generate a set of overlaid isochrones e.g at 1, 2, 5, and 10 days travel by sea.

Since the tool would be used to model long journeys lasting several days and potentially covering several continents, the model needed to account for the curvature of the Earth, as well as allowing isochrones to cross the poles.

![Crossing the Poles](/projects/amoeba/poles.png)

Significant effort was placed into making the tool easy-to-use with no training required nor the need to read guides. For example, we minimised the number of controls made available including abstracting low-level accuracy considerations into a simple low/medium/high control.

For maximum flexibility the application included a freehand drawing tool to define no fly/sail zones, as well as the ability to select countries specifically. The ability to open/close canals enabled users to model the impact on journey times if for example the Suez Canal was inaccessile, thus requiring sailing around the entire continent of Africa.

## Technical details

The application was built in the Remix framework with a Node.js backend and a SQLite database. The map component used tiles from Esri and components from React Leaflet. The Intelligence Community Design System was used for most of the remaining UI components, as well as additional Leaflet libraries for specific functionality such drawing polygons on the map.

The isochrone calculation model was written in TypeScript and embedded in the application running on the Node.js server. The model relied on the use of visibility graphs to generate lines of sight between points (via the visibility-graph.js library). For maritime this included points on land masses as well as canals an no-sails zones. For air it just included no fly zones.

![Visibility Graph](/projects/amoeba/visibility-graph.png)

Dijkstra's algorithm was then used to calculate the shortest path from the starting point to every other point within range. The region bounded by these points intersected with the region bounded by the maximum possible distance gave the theoretical region that could be reached. These calculations relied heavily on the use of the Turf.js geospatial library.

![Shortest Path](/projects/amoeba/shortest-path.png)

For small and medium distances the model was able to calculate the isochrones in seconds; for large distances such as a crossing several continents, the model could take minutes due to the increased number of data points. Much effort was dedicated to reducing the runtime, including reduced resolution data sets of land mass points, caching results of Dijkstra, and avoiding unnecessary calculations wherever possible.
