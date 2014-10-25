---
title: Usage and analysis ideas
permalink: /Usage_and_analysis_ideas/
---

Brainstorm / Visualization / Analysis / Data Usage Breakout Session

Future-looking discussion of advanced applications for 311 services. The assumption is that the data (including near-realtime data) is available from the 311 system.

Summary:
--------

1.  Digg style prioritization service, reputation layer optional
2.  blame.us - who's responsible, accountable - chain of blame for problems - and who can fix this?
3.  Public SR history - surfacing history of SR (and the related entities)
4.  Noisescore - realtime reporting of decibel levels
5.  Open Geo Stack - for the city (SaaS)
6.  Activity Streams - social and firehose
7.  Public Sidebar/ShiftSpace/OpenLayers - map layer
8.  Heart.us - neighborhoods competing to care the most about the neighborhoods
9.  .org+.gov matching system
10. Hyperlocal dashboard - visualization of everything going on in a several block area
11. 311 for engagement - opt-in for hearing about city announcements etc when you contact
12. Elected officials visualization

**More Notes:** Assume: bidirectional comm/lifecycle tracking for SRs

**Weighting/reputation for prioritization of requests**

-   intelligent triaging of dupes; additional permissions based on karma/sincerity
-   full history tracking

**lobb.ly, blame.us**

-   reports - information of agency in charge, elected representatives, etc. etc.
-   where to cast blame? who is responsible? more importantly, who can \*fix\* this

Also, public history? ex.: perpetual pothole on the street getting local community to petition service request vs capital project - can 311 help w/ strategic/political decision making (bigger picture)? by making it available to the public open up requests, a more informed public bicycle crash report - case history?

**using 311 reports to publicize - state issues**

-   building political will across jurisdictional boundaries
-   sunlighting - seeclickfix examples: CT traintracks

**NYC 311 - Analytics**

-   internal BI system - access to anyone in govt who asks
-   star schema - 311 middle - points - building inspection, sewage maintenance
-   sensitive data - usually not?
-   some of the most useful data for public is the least sensitive
-   inspector reporting conditions on the street (telnav input)
-   on nyc.gov, but data feeds not available

**analytics/visualization** if you have the data, being able to slice/query/visualize:

-   types of reports, reporters, open requests
-   time to resolution, accounting by reporting channel, geography, socio-economic lines etc
-   overlaying requests to funding
-   view trends over time

**City run, publicly available opengeo platform**

-   annotations, histories ACLs (anecdote)
-   privately developed by nyu/columbia urban studies
-   deemed classified information post 9/11 (heights etc compiled from public data)
-   citymap - security, privacy levels

**challenges:**

-   not enough resources at the state level to create a unified standard
-   counties doing their own stuff based on their own expertise (HAVA compliance)

Timeliness is an issue - is the data propagating? is the entry better (the iPhone app being slowere than the old text only version)

**surfacing public activity streams**

-   PuSH - firehose - stream not dumps
-   social - social activity stream (opting in)
-   logging in link FB? is that identity - per item basis
-   PuSH + Salmon - private conversations back up
-   achievements, announcements: pothole fixed thanks to @a @b @c!

**heart.us**

-   311 as proxy for how much people care about a neighborhood
-   scoring/game dynamics
-   prompts behavior (simple numbers, see if it helps or make things worse -- unfortunately long term effects)
-   aligning social incentives, stats, engagement
-   311 as strategy game, online game
-   make it fun?

**Civic Sidebar Wikipedia**

-   Google Sidebar - won't or can't respond to.
-   Map Layers - shiftspace

**passive sensing**

-   dash style - can there be problems reported passively using mobile sensors
