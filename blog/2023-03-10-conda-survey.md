---
title: "Conda survey results"
slug: "2022-03-10-conda-survey"
tags: [conda]
tease: "Conda users! We got your input on future directions for conda."
---

Anaconda [surveyed the conda community in late 2022](https://conda.discourse.group/t/tell-us-how-you-use-conda/113). This post reviews what we learned from that survey and how it is impacting the future directions of conda.

Around the same time, the Python Software Foundation [published the results of their (much, much bigger) Python Packaging Survey](https://drive.google.com/file/d/1U5d5SiXLVkzDpS0i1dJIA4Hu5Qg704T9/view).  The two surveys asked some similar questions and some distinct ones.  We include insights from the PSF survey when they are particularly relevant to the conda community.

<!-- truncate -->

The conda survey had 72 responses.  That's not huge, but it's not small either. PSF received 8774 responses.

The summary has several sections:

* **How happy are people with conda?**
* **What needs improvement?**
* **When is conda used?**
* **What is conda used with?**
* **Who uses conda?**

Many thanks to [Luc (Boaz) Douyon of Anaconda](https://www.linkedin.com/in/luc-douyon-b97125164/) for the conda survey, and [Shamika Mohanan of the PSF](https://pyfound.blogspot.com/2021/08/shamika-mohanan-has-joined-psf-as.html) for the Python packaging survey summary.

Dave Clements, on behalf of the Conda Communications Team

---

# How happy are people with conda?

The conda survey asked 4 questions that we'll throw into the "happiness" bucket:

[![Conda is my preferred package manager](/img/2023-03-10-conda-survey/conda-is-my-preferred-package-manager.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1699334366)
[![I can access my desired packages](/img/2023-03-10-conda-survey/i-can-access-my-desired-packages.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1192657027)
[![I can integrate conda with my workflow](/img/2023-03-10-conda-survey/i-can-integrate-conda-with-my-workflow.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1595912193)
[![I am satisfied with conda](/img/2023-03-10-conda-survey/i-am-satisfied-with-conda.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1582523399)

The news here is mostly good, but the results also highlight that things still need to be improved. For example, in "Conda is my preferred package manager" 61% had "happy" responses, but 25% were neutral, and almost 14% had "unhappy" responses.  That's 39% who can't say they are in the "happy" bucket.  For the other three questions the numbers outside the "happy" categories are 28%, 24%, and 32%.  Those are better, but still not where we want them.  See the specific feedback below for some reasons behind these numbers.

# What needs improvement?

The survey asked respondents what changes should be prioritized going forward.

[![Desired conda changes](/img/2023-03-10-conda-survey/desired-conda-changes.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1229097249)

## Speed

The need for speed was the most prominent theme:

* 71% prioritized speedups
* 60% use mamba, which is known for being very fast compared to the standard conda solver.

Some individual responses:

* "just make libmamba the default solver already!!!!"
* "Nearly 100% use Mamba nowadays due to speed, only fallback to Conda when something is going wrong"
* "*Dear Goddess make the solver faster out of the box.*"

This survey was taken in November and December 2022, which we feel was an inflection point in conda's performance profile.  The [22.11.0 conda release], which came out towards the end of the survey window, implemented parallel package download and extraction, and dropped the `experimental` tag from the `conda-libmamba-solver` (the solver was added in the March 2022 release). At the time of the survey, [only 19% of respondents were using conda-libmamba-solver](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1650032116).

These changes are representative of a multi-year, and continuing effort to improve the speed of conda.  Our next survey will tell us if conda is succeeding at speeding things along...

## Better error messages

Close behind speed was *more helpful error messages* with 65% of respondents.

Some individual feedback

* "when it works, it's fantastic. when it doesn't, it's really painful to diagnose dependency resolution issues and discover what's happening, resulting in ad hoc tools like parsing json into networkx or something for exploration."
* "Explorability of dependency resolution conflicts"

The conda-libmamba-solver error messages will improve shortly [as the latest version of the solver gets integrated into conda](https://github.com/conda/conda-libmamba-solver/issues/102).

## Better interoperability

*Improved interoperability with other package managers* was prioritized by 62% of respondents. This message is reinforced by how frequently people use more than one package manager.

[![Which additional package managers do your use, top](/img/2023-03-10-conda-survey/which-additional-package-managers-do-you-use-top.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1102296811)

79% of conda survey respondents use other package managers in addition to conda.  75% of all respondents also use pip, and 55% use mamba.

The PSF survey asked "What Packaging tools do you use?"  They blended together package and environment management (as does conda itself):

[![PSF: Which Python packaging tools do you use?](/img/2023-03-10-conda-survey/psf-which-python-packaging-tools-do-you-use.png)](/img/2023-03-10-conda-survey/psf-which-python-packaging-tools-do-you-use.png)
(Note: PSF survey results are shown with a blue outline.)

In this survey conda is used less frequently than 6 "standard" (and highly overlapping) entries (pip, venv/virtualenv, PyPI, setuptools, and wheel), and by poetry. pip has almost twice as many users as venv, the second most popular response. conda is followed closely by pipenv and twine.  conda-build is listed in the bottom half with 4-5% of respondents using it.

(This is only one snapshot in time, so we can't say if the conda ecosystem is gaining or losing mind-share in the Python ecosystem.)

The PSF survey asked several questions specifically related to interoperability.

[![What should the packaging ecosystem do to be an "ecosystem for all"](/img/2023-03-10-conda-survey/psf-what-should-the-packaging-system-do-to-be;-an-ecosystem-for-all.png)](/img/2023-03-10-conda-survey/psf-what-should-the-packaging-system-do-to-be;-an-ecosystem-for-all.png)

When PSF asked their respondents to rank these 4 priorities the highest ranked (by far) is "Support more interoperability between Python packaging tools."  At the very bottom was "Support interoperability between Python packaging and packaging tools for other languages."

Several other questions revealed a strong preference for just one tool/workflow for package management.

[![How much do you agree with these statements?](/img/2023-03-10-conda-survey/psf-how-much-do-you-agree-with-these-statements.png)](/img/2023-03-10-conda-survey/psf-how-much-do-you-agree-with-these-statements.png)

The first question is "I prefer to have a clearly defined "official" workflow" which 75% agreed with.  A second similar (but inversely worded) question asks if "The existence of multiple tools is beneficial for the Python packaging ecosystem.  Here 46% disagree with the statement, and 23% are neutral

**What do we do with all this?**

Let's start by noting that the Python community strongly prioritizes interoperability between Python packaging tool, but that support for multiple languages is at the bottom.  This is good news and bad news for conda.  Conda already works well with Pip.  The downside is that most PSF respondents don't prioritize support for multiple languages, which is one of conda's superpowers.

PSF respondents would also clearly prefer to have a single packaging toolkit.  This is not necessarily bad news for conda, as the conda ecosystem addresses concerns that Pip does not.  The PSF survey does not ask "What toolkit would you prefer that to be." However, given the Python community's current usage of Pip/Venv our guess is that they would say "Pip/Venv", and that is a challenge we need to address.  We hope the current much wider us of Pip/Venv is merely a byproduct of the wide range of Python packages available via Pip and that this is a Python community survey, rather than a widespread preference for the capabilities of Pip/Venv over conda.  But, from these surveys we can't tell that.

# When is conda used?

## Industries and Ambits

[![Top industries](/img/2023-03-10-conda-survey/industries-top.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1700458323)

Just over 40% of respondents are connected to *academia*. Since the student plus professor/instructor pool adds up to less than 25%, a significant slice of these academics come from other job functions. Specific domains make up the long tail of responses.

When asked in [what settings participants use conda](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=720256469) 81% said *at work*, while only 18% said *school-related.*  72% use conda on *open-source* projects.  53% use if for "personal* projects.

## Domains

The survey used the [categories from the packages directory on the Anaconda Nucleus site](https://anaconda.cloud/package-categories) to ask in what application areas conda is used in

[![What types of applications do you use conda in?](/img/2023-03-10-conda-survey/what-types-of-applications-do-you-use-conda-in-top.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1170448145)

Data Usage & ETL (67%, Extract, Transform and Load) and Machine Learning & AI (63%) were the most common applications.  Visualization (54%), Packaging (54%) and Scientific (53%) make up the next largest groups.

# What is conda used with?

## Packages

The conda survey asked people to list their top 5 packages.

[![Top 5 packages](/img/2023-03-10-conda-survey/top-5-packages.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=968125862)

This question had a few clear leaders with Numpy and Pandas used by over half of respondents.  Matplotlib, Scipy, and Scikit-learn were used by 1/4 to 1/5 of respondents.

## Compute Environments

Linux was the [dominant operating system](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1402353521) with almost 70% use, but macOS and Windows weren't that far behind, both in the neighborhood of 50%. VS Code was the clearly [preferred IDE](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1423420551) with 70% use.  The Jupyter platforms came in next, with both in the mid 40 percents.  PyCharm was used by 1/3 of paricipants.

[![Programming languages, top](/img/2023-03-10-conda-survey/programming-languages-top.png)]
(https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=681062781)

Python was the most widely used programming language by far, with almost 100% use.  Shell, C/C++, R and SQL had 1/3 to 1/4 as many users as Python.

There is also data about [framework tools](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1602748522), [CI tools](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=374176396), [machine learning frameworks](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1065357430) and [ML operations](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=2146408368).

## Data

Respondents [used open and proprietary data equally](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=937856418), with both garnering close to an 80% response rate.

[![Data formats, top](/img/2023-03-10-conda-survey/data-formats-top.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1927071597)

Over 33 data formats were listed as being used. CSV and JSON were the most popular with 6 out of every 7 responders using CSV.

[![Databases, top](/img/2023-03-10-conda-survey/databases-top.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1314196509)

Respondents listed 13 database management systems they use.  SQLite (36%) and PostgreSQL (32%) led this group, followed by MySQL (19%).

## Tools

[![Statistical analysis tools, top](/img/2023-03-10-conda-survey/statistical-analysis-top.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1524339820)

Microsoft Excel (35%) and R (31%) were the two most popular tools in the statistical analysis tools category.

[![ETL Tools, top](/img/2023-03-10-conda-survey/etl-tools-top.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1574024089)
[![Data visualization tools, top](/img/2023-03-10-conda-survey/data-visualization-tools-top.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1532616702)

The survey asked specific questions about ETL and data visualization tool use.  20 ETL tools had users, but only Pandas (54%), Apache Airflow (10%) and Apache Spark (10%) had more than one or two.  Jupyter (67%) was the clear leader in data visualization responses, with Plotly (35%) following.  23 other visualization tools were listed, most with only one or two users.


# Who uses conda?

71 of 72 responders write some code as part of their work.

## Participant experience

Both the conda and Python groups had similar levels of experience. [68% of conda respondents had 4+ years of experience with conda](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1883612863), while 66% of Python respondents has 4+ years of experience with Python.  The conda survey asked participants about their job functions, industries and Project types.

## Job Functions

[![Job functions](/img/2023-03-10-conda-survey/job-function-top.png)](https://docs.google.com/spreadsheets/d/1rpWN6atSEsALvStPtAVIf_WMTxXXKaDKYpKRsvMpbOo/edit#gid=1839470285)

The most common role was *Developer*, followed closely by *Research Scientists.* The top 12 roles can be roughly grouped:

* *Developer* (29.2%)
* *Research Scientist* (27.8%) and *Applied Scientist* (15.3%)
* *Data Scientist* (22.2%), *Data Engineer* (15.3%), and *ML Scientist* (12.5%)
* *Professor/Instructor* (12.5%) and *Student* (11.1%)
* *ML Ops* (6.9%), *DevOps* (5.6%), and *System Administrator* (4.2%)
* *Project Manager* (4.2%)

People could select more than one job function.