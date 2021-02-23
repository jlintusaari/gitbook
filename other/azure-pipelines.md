---
description: My notes on how Azure Pipelines works and what is possible with it
---

# Azure pipelines

### Organization of work

All work happens in **steps**. Steps happen sequentially one after another. 

Steps belong to **jobs**. Jobs can happen in parallel. A single job runs in the specified pool \(worker\). It seems you cannot run two jobs in the same worker.

Jobs can be grouped into **stages**. Stages have an inbuilt support for branching out and funneling back in.

Finally stages belong to **pipelines**. Pipeline is contained in a `.yml` file. Pipelines can trigger other pipelines but

* There is no easy way to pass parameters from one pipeline to another
* There seems to be no easy way to funneling multiple pipelines into one \(i.e. wait for n other pipelines to complete\).

### Templates

These allow you to attach a stage, job, or step partials into your pipeline. They seem to be rendered as if the pipeline was in a one big file. This means

* You cannot define resources \(e.g. repositories\) in your template
  * You can checkout repositories, but they have to be defined in the main template file

The notation `${{ variable }}` is rendered during template rendering and must be available at the template render time.

### Things that may trip you

* If you checkout one repository, it's checked out to your working directory. If you checkout multiple repositories they go to folders with the name of the repository.

### Best practices

Define all your resources in your pipeline, and checkout all the needed repositories there. Then build templates that make assumptions on what resources \(e.g. repositories\) are available in the pipeline and document them well.

Do not treat templates as if they were functions. They are too limited to work like that.

Use stages to branch out and funnel back in the pipeline.

### Useful links:

{% embed url="https://stackoverflow.com/questions/61729574/azure-devops-multistage-pipeline-yaml-how-to-checkout-multiple-repos" %}

{% embed url="https://stackoverflow.com/questions/64690588/how-to-use-template-with-references-to-script-in-another-repository-within-azure" %}



