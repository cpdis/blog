---
title: Folder Structure and Workflow
layout: post
date: 2018-01-08 22:00:18 -0600
image: /assets/images/
headerImage: False
tag:
- workflow
- yearofml
star: False
category: blog
author: cpdis
description: Workflow and folder structure for working through papers and other projects.
---

There are two categories of projects that I’ve collected: ML papers and tutorials/working examples. For both of these I want a consistent workflow that allows me to present summaries in an quick and efficient manner and to reference in the future.

## Papers
I think that I have come up with a decent template for presenting a summary of each of the papers that I read as well as describe how they might be useful. There will be four sections: _Summary_, _Notes_, _Research Method_, and _Resources_. The _Summary_ section will include a brief summary in my own words along with a concise summary quote from the paper itself. The _Notes_ section is pretty self explanatory but I will try to make it verbose enough that it can stand on its own. The _Research Method_ section will follow this format:

1. Read the introduction and summarize.
2. Identify the big question or hypothesis.
3. Summarize the background in five sentences or less.
4. Identify specific questions.
5. Identify the approach.
6. Read the Methods section and diagram the experiment (this will vary widely based on the paper).
7. Summarize the findings of each result.
8. Do the results answer the specific questions asked above?
9. Read the conclusion and summarize.
10. What are others saying about this paper?

Finally, the _Resources_ section will link to any additional information about the paper such as code repositories, datasets, subsequent papers, and projects based on the results of the paper. 

## Tutorials and other code based projects
My goal when working through tutorials or trying to reproduce models is to have a consistent and efficient workflow that makes it simple to replicate across projects. An efficient workflow makes it easier to understand the scope of the project and return to it at a later. At work, despite our best intentions and templated folder structure, our projects inevitably end up as a labyrinth of cryptically named folders full of unlabeled data and results. I hope that starting this project with a carefully considered organizational philosophy will help in the weeks and months to come. A few requirements that went into building my final workflow:

**Always use version control.**

This is important because it makes it easier to work from multiple computers (and iPads), makes it easier to share and collaborate with others, and makes it easier to replicate results.

**Separate code from data.**

This is especially important in machine learning projects since datasets can be very, very large. In addition, it makes it easier to swap between datasets and share code with others.

**Separate raw, working, and processed data.**

 I think it’s useful to separate data into a few different sources:
 
* **Raw** data is the original, immutable data.
* **Interim** data is the working data that is being transformed.
* **Processed** data is the final dataset being used for modeling.
* **External** data is from third party sources.

Organizing the data this way allows you to know when you can safely delete and move files. 

Given those requirements I went about building my folder structure and workflow. Quickly, though, it dawned on me that there are thousands of teams and tens of thousands of practitioners working on real, in-production problems that have most likely optimized their workflows for maximum efficiency. With that, I went in search of the perfect folder structure and research workflow. While I’m pretty sure I didn’t find exactly that, I found something that fits all the requirements above and is automated as well. 

The [Cookiecutter Data Science](http://drivendata.github.io/cookiecutter-data-science/)  project structure is _a logical, reasonably standardized, but flexible project structure for doing and sharing data science work._ Cookiecutter Data Science is built on [Cookiecutter](http://cookiecutter.readthedocs.io/en/latest/readme.html) which is a command-line utility that creates projects from templates (cookiecutters). The creators of Cookiecutter Data Science summarize it like this:
> When we think about data analysis, we often think just about the resulting reports, insights, or visualizations. While these end products are generally the main event, it's easy to focus on making the products _look nice_ and ignore the _quality of the code that generates them_. Because these end products are created programmatically, code quality is still important! And we're not talking about bikeshedding the indentation aesthetics or pedantic formatting standards — ultimately, data science code quality is about correctness and reproducibility.  
>   
> It's no secret that good analyses are often the result of very scattershot and serendipitous explorations. Tentative experiments and rapidly testing approaches that might not work out are all part of the process for getting to the good stuff, and there is no magic bullet to turn data exploration into a simple, linear progression.  
>   
> That being said, once started it is not a process that lends itself to thinking carefully about the structure of your code or project layout, so it's best to start with a clean, logical structure and stick to it throughout. We think it's a pretty big win all around to use a fairly standardized setup like this one.  

I think that the template based approach is great. I have already modified the directory structure and some make files that I don’t see myself using initially. As the weeks pass and I refine my workflow, I’m sure that I will be modifying or creating new cookiecutters (you can have multiple templates that are called from the command line). 

I’m looking forward to my research workflow being refined over time and becoming more robust and efficient—hopefully the process described above is a good starting point.


