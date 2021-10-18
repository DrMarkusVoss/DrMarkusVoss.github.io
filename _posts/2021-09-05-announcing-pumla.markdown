---
layout: post
title:  "pumla: re-usable models as code"
date:   2021-09-05 22:05:55 +0200
categories: pumla
---

Do you like PlantUML but are not happy with it regarding the re-use of once modeled elements?

I may have a solution for you. If you can’t wait, directly see the solution here:

[https://github.com/DrMarkusVoss/pumla](https://github.com/DrMarkusVoss/pumla)

![](/assets/images/pumla_logo.png){:class="img-responsive"}

If you have some time, here is the story:

I worked on one of my „longterm spare-time projects“, a music composition software with a different workflow than the products on the market. I regularly try out new architecture tools, so that time I was trying to use PlantUML to document my ideas and architecture.

PlantUML is a tool to describe your architecture in UML (and now also a lot of other domain-specific languages like e.g. gantt charts for project planning) with a text/ASCII-based description. But in fact, you are actually describing the diagrams that you want to see in the end rather than describing an architectural model. If you have a detailed diagram where you modeled an element with all its details, and you want to re-use it on another diagram, but maybe with less detail, basically you „model/code“ that architecture element again on a new diagram in a new file. The re-use mechanisms that PlantUML offers via its pre-processor (e.g. !include, !includesub) are very limited and along with the other limitations of PlantUML (e.g. regarding mixing of different element types like classes and components) it becomes pretty harsh, up to impossible, to systematically build up a repository of re-usable architecture elements described with PlantUML, that can be re-used in different diagrams and views with different aspects.

As I liked the broad variety of diagram possibilities of PlantUML, I decided to extend PlantUML by an own development to overcome the limitations regarding the re-use. That led to another „longterm spare-time project“ being born: pumla.

pumla allows for systematic architecture modeling and model re-use in a git-based development workflow using the full power of PlantUML.

After more than 6 months of spare-time-development with more than 190 commits, I am proud to announce that pumla has reached the beta phase with a complete and consistent set of API (or better „AMI“ = application modeling interface), templates, examples, User’s Guide and Modeling Guideline.

If you are interested, check out the pumla project on GitHub here:

[https://github.com/DrMarkusVoss/pumla](https://github.com/DrMarkusVoss/pumla)

I am always interested in feedback, so feel free to contact me.

Have fun,

Markus


