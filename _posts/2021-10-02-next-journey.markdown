---
layout: post 
title:  "Moving Forward!"
date:   2021-10-02 
categories: watchbill journey
---
So now I have an MVP for the Path of Exile – Acolyte project. The minimum features work although there is plenty of
optimization left to be done. All the new features that I would want to implement are either going to require web API
calls to the Grinding Gear Games servers using OAuth and/or some fancy graphical capture to determine stateful
information (i.e., is the trade window open, is the correct currency placed in, automatically adjust UI elements based
on the game client). While all of that is useful to a small degree, it is not necessarily going to get many brownie
points for future job searches (except for utilizing web APIs of course).

Being in the service, there has always been a need for software/tools to help to make “watchbills.” While there is plenty
of apps for workforce management, either they are paid (which none of the worker bees want to shell out money for) or
unable to be utilized on the NMCI network which by design is massively locked down for security reasons. Ultimately, the
only things that can be used are MS Office products including access (sans any add-ins) or websites, possibly mobile
apps. My next project will be learning the pipeline necessary to deploy a website and possibly a mobile app that would
solve this problem.

Coder Foundry, Tim Corey and multiple other coding YouTubers mention the key skills for entering the software developer
market are going to be: database CRUD, APIs (REST), cloud technologies (AWS/Azure), frameworks (.Net/Angular/React etc)
and responsive design (mobile/tablet/web). My plan is to start small and build/branch out to each of the technologies as
I increase the scope or functionality of my next project named “MyNavySchedule.”

## What problem is this solving ##

As early as E-4, Sailors and sometimes civilians will be tasked with managing another’s schedule for work or watch
standing. The latter is driven off a specific type of schedule called a watchbill which can group individuals outside
their work center, division or sometimes even commands for assigned duties. When allocating the “watch” multiple factors
must be considered: qualifications, normal work schedule, leave/training and various one-off scenarios such as
supernumerary lists, light duty, or one-time events. There is often a communication gap between the individual, their
supervisor, the watch coordinator and/or others within the scheduling pipeline, and although we are “Semper Gumby”,
de-conflicting a schedule takes more than a small amount of mental power and a huge amount of intellectual organization.

## How to solve the problem ##

Just as I did before, I will create a written specification for scenarios to account for, a broad overview of the
structure/design and a features list sorted by necessity. At a minimum, the program needs to:
- Hold a list of personnel 
  - Assign their responsibilities 
  - Maintain a correlation of a duty to a qualification
- Maintain a calendar of daily duties/work duties/time off/LLD etc. 
- Group individuals by "section" or as a standalone group 
- Identify scheduling conflicts
- Daily/Weekly/Monthly/Custom reporting of schedules
  - Filters for sections/watches

## Steps to MVP ##

Since this will be data driven, I will first prototype the design in MS Access (with minimal forms/functionality) then
migrate to a cloud hosted database on AWS (most likely SQL Server). From there, I will learn the necessary
C#/.Net/ASP.Net/etc. pipeline for having a data driven site and build out a minimal front end. Authentication will start
with a simple username/password but extensible enough to use OAuth/SSO later. At this point I would have a MVP and will
revise/implement the features list based on any lessons learned.



