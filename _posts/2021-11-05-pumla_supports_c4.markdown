---
layout: post
title:  "New pumla release v0.9.0 with support for C4 model!"
date:   2021-11-05 14:45:54 +0200
categories: pumla
published: true
---

I just released the second major beta version of my spare-time project [**pumla**, **Release v0.9.0**]():

[https://github.com/DrMarkusVoss/pumla/releases/tag/v0.9.0](https://github.com/DrMarkusVoss/pumla/releases/tag/v0.9.0)

[**pumla**](https://github.com/DrMarkusVoss/pumla) transforms and extends the *diagrams-as-code* approach
of [PlantUML](https://plantuml.com/de/) and enables a *model-as-code*
approach that allows re-use of once modelled aspects in several diagrams.

With **pumla v0.9.0** the following new features got implemented compared to 
v0.8.0:
- [C4 model](https://c4model.com) support: re-usable C4 model assets (elements & relations) extending the 
  [C4-PlantUML extenstion](https://github.com/plantuml-stdlib/C4-PlantUML)
- Cheat Sheets to show tagged values on elements, relations and connections
- CLI providing access to the model repository in JSON format for easy integration into
  other tools
- project-specific global variable defaults
- stable installation procedure with built-in version consistency checks
- stable deployment procedure that decouples your modelling projects from 
  the pumla tool installation

Here is an advanced C4 example modeled with pumla in a re-usable way:

[https://github.com/DrMarkusVoss/pumla/blob/main/test/examples/C4example/pumlaC4Example.md](https://github.com/DrMarkusVoss/pumla/blob/main/test/examples/C4example/pumlaC4Example.md)

Enjoy,

Markus
