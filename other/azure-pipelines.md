---
description: My notes on how Azure Pipelines works and what is possible with it.
---

# Azure pipelines

[Documentation](https://docs.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops)  \|  [YAML reference](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema?view=azure-devops&tabs=schema%2Cparameter-schema) \| [Predefined variables](https://docs.microsoft.com/en-us/azure/devops/pipelines/build/variables?view=azure-devops&tabs=yaml)

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

### Variables

These are confusing enough to require a page titled ["Understand variable syntax"](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/variables?view=azure-devops&tabs=yaml%2Cbatch#understand-variable-syntax). There are

* `${{ parameters.var }}` for templates. These are substituted when templates are compiled.
* `$[variables.var]` for runtime use. According to docs designed for conditions and expressions.
* `$(var)` for other \(general\) runtime use.

![A table aiming to explain the variable syntaxes](../.gitbook/assets/image%20%281%29.png)

### Conditions

```text
# Job condition with a template or pipeline parameter
job: Job
condition: eq('${{ parameters.release }}', 'false')
```

### Things that may trip you

#### Checkout

* If you checkout one repository, it's checked out to your working directory. If you checkout multiple repositories they go to folders with the name of the repository.
* With single checkout the working directory will be the checked out directory \(even with using path\)
  * With multiple checkout it will be the sources directory \(that contain the repo directories\)

#### Yaml reference

* The YAML reference is incomplete. E.g. at the time of writing \(23.2.2021\) it doesn't show that you can specify `pool` at the stage level, although the [stage documentation](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/stages?view=azure-devops&tabs=yaml) shows you can.

#### Variable substitution syntax

* The runtime variable syntax `$(varName)` is unfortunate as it clashes with bash command syntax

### Best practices

Define all your resources in your pipeline main file. Then build templates that make assumptions on what resources \(e.g. repositories\) are available. Document these well into your templates. 

For instance to extract an output variable from a template step/job/stage, you need to know the name of the stage/job/step to access it.

Do not treat templates as if they were functions. They really are just compiled to be a single pipeline file.

Use stages or jobs to branch out and funnel back in the pipeline.

### Starting Jenkins builds

Jenkins builds can be started from Azure DevOps with the `JenkinsQueueJob` . You need to create a service connection for Jenkins in Azure DevOps. Then in your pipeline simply:

```text
  - job: triggerJenkinsBuilds
    displayName: Trigger Jenkins builds
    # This is here just for the sake of an example, a dependency to a previous job
    dependsOn: DependencyJob
    variables:
      version: $[ dependencies.DependencyJob.outputs['step_name.var_name'] ]
    steps:
      - task: JenkinsQueueJob@2
        displayName: Build windows installer
        inputs:
          serverEndpoint: jenkins-service-connection-name
          jobName: jenkins-job-name
          #isMultibranchJob: # Optional
          #multibranchPipelineBranch: # Required when isMultibranchJob == True
          #captureConsole: true
          #capturePipeline: true # Required when captureConsole == True
          # This is important to be correct if the job is parametrized
          isParameterizedJob: true
          jobParameters: |
            VERSION=$(version)

```

### Enabling Git commands

You need to [set permissions](https://docs.microsoft.com/en-us/azure/devops/pipelines/scripts/git-commands?view=azure-devops&tabs=yaml) to enable Azure pipeline git account to make changes to the repository. In addition, in the checkout step, you need to persist the repository access token with:

```text
steps:
- checkout: self
  persistCredentials: true
```

Finally in the pipeline code, you need to make sure you have provided identity information for git that will show up e.g. in commits. This can be done with:

```text
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

### Useful links:

{% embed url="https://stackoverflow.com/questions/61729574/azure-devops-multistage-pipeline-yaml-how-to-checkout-multiple-repos" %}

{% embed url="https://stackoverflow.com/questions/64690588/how-to-use-template-with-references-to-script-in-another-repository-within-azure" %}

{% embed url="http://thecodemanual.pl/2020/05/05/cross-stage-variables" %}



