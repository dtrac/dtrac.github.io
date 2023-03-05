+++ 
draft = false
date = 2023-03-04T20:34:12Z
title = "using mermaid diagrams in hugo"
description = ""
slug = ""
authors = ["dan"]
tags = ["web", "development", "hugo", "mermaid"]
categories = ["web development"]
externalLink = ""
series = []
+++

Anyone that knows me, knows that my memory can be....sub-optimal.  Therefore a key part of studying for my upcoming [Microsoft Certified Cybersecurity Architect Expert](https://learn.microsoft.com/en-us/certifications/cybersecurity-architect-expert/) exam, was to create a mindmap of the subject matter.

I'd heard good things about the [Mermaid](https://mermaid.js.org/) Diagramming and charting tool, which renders markdown to create and modify diagrams dynamically.   As I have chosen to use the [Hugo](https://gohugo.io/) framework for my blog site (which also leverages the power of markdown...), the two seemed a good fit.

To get things rolling I first had to install the Mermaid library into my site's theme layout **themes/hugo-coder/layouts/partials/head.html** file:

        <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
        <script>mermaid.initialize({startOnLoad:true});</script>


...This then allows me to use the {{ mermaid ]} shortcode to add diagrams in Mermaid syntax and have them rendered directly within blog posts.

Which means, that code like this:

        
        mindmap
        root((Azure SC-100 Exam Objectives))
            Design a Zero Trust strategy and architecture
            Evaluate Governance Risk Compliance technical strategies and security operations strategies
            Design security for infrastructure
            Design a strategy for data and applications
            Recommend security best practices and priorities 

...makes lovely mindmap diagrams like this:

{{<mermaid>}}
mindmap
  root((Azure SC-100 Exam Objectives))
    Design a Zero Trust strategy and architecture
    Evaluate Governance Risk Compliance technical strategies and security operations strategies
    Design security for infrastructure
    Design a strategy for data and applications
    Recommend security best practices and priorities 
{{</mermaid>}}

It's a start.