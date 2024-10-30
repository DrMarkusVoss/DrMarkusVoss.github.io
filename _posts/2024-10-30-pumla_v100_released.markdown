---
layout: post
title:  "pumla v1.0.0 released!"
date:   2024-10-30 06:45:54 +0200
categories: pumla
published: true
---

Yesterday I came to the conclusion that pumla, my spare time project that enables "re-usable models as code", in its current state has all the features to fulfill
the indended use cases. Furthermore, also no bugs have been found for quite some time. Therefore I released now its
first "production ready" version:  **pumla**, **Release v1.0.0**:

[https://github.com/DrMarkusVoss/pumla/releases/tag/v1.0.0](https://github.com/DrMarkusVoss/pumla/releases/tag/v1.0.0)

With pumla, it is possible to work with a git-based workflow, model or document architecture with PlantUML and still be
able to re-use once modelled aspects. The goal is achieved.

On the other hand, there are some drawbacks to this solution:
- the visualization, that is still based on PlantUMLs diagram generation, does not always meet high expectations
and especially when diagrams become bigger with more dedicated "arrows" starting from "ports" the layout is lacking and
there are no sufficient mechanisms at hand to easily fix these shortcomings manually
- the "language" you have to use, is a bit ugly and therefore not always straight forward easy;
 it is a mix of PlantUML (which in itself is not so consistent with its lots of possibilities for shortcuts, which
you should not use (see [pumla Modelling Guideline](https://github.com/DrMarkusVoss/pumla/blob/main/ModellingGuideline.md))
 and the pumla Macros that form the language for re-use

SysML v2 is on the horizon, that would solve the language problem. At the same time I do not yet see how it will solve
  the re-use problem in a git-based, distributed docs-as-code approach. I am not sure if and how this use case will
 be addressed by the standard or whether different tool vendors will come up with solutions (maybe similar to what pumla
is doing). The visualization issue might be solved, as potentially the tool vendors could offer their visualization generators
 for SysML as commercial separate tools or plugins for IDEs like VSCode.

There are still some ideas for further releases for pumla, but time is limited, so these will come drop by drop and as my time allows
for it. Any help or contribution is highly welcome.

Enjoy,

Markus
