---
layout: page
title: Desk Booking
---

The Desk Booking application was built as a demonstrator application for employees in an office to book their desk from any web-connected device. The application lets users clearly see which desks are available, find where their co-workers are sat, and make their bookings ahead of time or on the same day (if there's anywhere left to sit!)

![Floorplan](/projects/desk-booking/booked.png)

{::nomarkdown}
<br />
{:/nomarkdown}

## Problem

In an office with hybrid working patterns and hot desking, employees need to book their desk ahead of time (or at the last minute) to guarantee a place to work. They need to know where their colleagues are sat to enable collaborative working. Human Resources need to gain insights into office utilisation and whether there are sufficient first aiders and fire marshals in attendance each day. Some users need the ability to book seats for guests. The application needs to be accessible on mobile devices so that users can make a booking or check their booking on the commute into the office.

{::nomarkdown}
<br />
{:/nomarkdown}

## Solution

In 2-3 months the team built a full stack application capable of reuse by any office. The demonstrator was seeded with data relating to the floor plan of their own company office and org structure, as well as synthetic data for employees and bookings. The design was responsive to render the booking form as a sidebar on large screens and as a draggable drawer on smaller devices, as well as hiding or compacting less essential content on smaller screens such as utilisation metrics.

Desks and bookings were visible both through the floorplan view as well as a filterable list view. Users and admins could manage their own and all bookings respectively via reports. An analytics dashboard showed various KPIs and charts to give insights into how the space was being utilised by roles, teams and individuals.

![Floorplan](/projects/desk-booking/dashboard.png)

Admins had the ability to mark desks as reserved or add key pieces of information to desks such as having a broken USB port that may influence a user's decision to book.

{::nomarkdown}
<br />
{:/nomarkdown}

## Technical Details

The application was built in the **Remix** framework with a **Node.js** backend and a **PostgreSQL** database.

The floorplan component was built from a **Figma** design exported as an SVG. This was overlaid with additional components customised from **MaterialUI** such as user avatars as well as click handlers to select desks.

Charting components were built from **Recharts** and reports from **Material React Table**.

Microsoft AAD federated authentication was implemeted for SSO.

Tests were written in **Jest** and **Playwright**.

The demonstrator application was deployed to **Fly.io** via **GitHub actions**.

{::nomarkdown}

<div class="project-pagination">
    <a href="{{ site.baseurl }}/projects/amoeba">← Amoeba</a> 
    <div /> 
  </div>
{:/nomarkdown}
