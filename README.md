# Terraform-Integration-With-GitHUb-Action


<p align="center">
  <img width="1000" height="500" src="https://miro.medium.com/max/3840/1*0afXWVL2HMfRdYi0sijkcw.gif">
</p>



## Introduction to GitHub Actions

GitHub Actions help you automate tasks within your software development life cycle. GitHub Actions are event-driven, meaning that you can run a series of commands after a specified event has occurred. For example, every time someone creates a pull request for a repository, you can automatically run a command that executes a software testing script.

### The Components of GitHub Actions:

## Workflows
The workflow is an automated procedure that you add to your repository. Workflows are made up of one or more jobs and can be scheduled or triggered by an event. The workflow can be used to build, test, package, release, or deploy a project on GitHub.

## Events
An event is a specific activity that triggers a workflow. For example, activity can originate from GitHub when someone pushes a commit to a repository or when an issue or pull request is created. You can also use the repository dispatch webhook to trigger a workflow when an external event occurs. For a complete list of events that can be used to trigger workflows, see Events that trigger workflows.

## Jobs
A job is a set of steps that execute on the same runner. By default, a workflow with multiple jobs will run those jobs in parallel. You can also configure a workflow to run jobs sequentially. For example, a workflow can have two sequential jobs that build and test code, where the test job is dependent on the status of the build job. If the build job fails, the test job will not run.

## Steps
A step is an individual task that can run commands in a job. A step can be either an action or a shell command. Each step in a job executes on the same runner, allowing the actions in that job to share data with each other.

## Actions
Actions are standalone commands that are combined into steps to create a job. Actions are the smallest portable building block of a workflow. You can create your own actions, or use actions created by the GitHub community. To use an action in a workflow, you must include it as a step.


## Runners
A runner is a server that has the GitHub Actions runner application installed. You can use a runner hosted by GitHub, or you can host your own. A runner listens for available jobs, runs one job at a time, and reports the progress, logs, and results back to GitHub. GitHub-hosted runners are based on Ubuntu Linux, Microsoft Windows, and macOS, and each job in a workflow runs in a fresh virtual environment. For information on GitHub-hosted runners, see “About GitHub-hosted runners.” If you need a different operating system or require a specific hardware configuration, you can host your own runners. For information on self-hosted runners, see “Hosting your own runners.”

<p align="center">
  <img width="1000" height="500" src="https://miro.medium.com/max/1094/1*L-PwXviTPRCpa88UMSWQUg.gif">
</p>

## GitHub Actions Comparison with Jenkins:

<p align="center">
  <img width="1000" height="500" src="https://miro.medium.com/max/2000/1*9uTbCT9ikkKxi4JjQZ5jng.gif">
</p>


<p align="center">
  <img width="1000" height="500" src="https://miro.medium.com/max/1400/1*dbOKDV8sCsgdz6JFwvMBsg.gif">
</p>

## Key Differences:
```
Jenkins has two types of syntax for creating pipelines: Declarative Pipeline and Scripted Pipeline. GitHub Actions uses YAML to create workflows and configuration files. For more information, see “Workflow syntax for GitHub Actions.”

Jenkins deployments are typically self-hosted, with users maintaining the servers in their own data centers. GitHub Actions offers a hybrid cloud approach by hosting its own runners that you can use to run jobs, while also supporting self-hosted runners. For more information, see About self-hosted runners.

Jenkins splits its Declarative Pipelines into multiple sections. Similarly, GitHub Actions organizes its workflows into separate sections. The table below compares Jenkins sections with the GitHub Actions workflow.

Jenkins lets you send builds to a single build agent, or you can distribute them across multiple agents. You can also classify these agents according to various attributes, such as operating system types.

Similarly, GitHub Actions can send jobs to GitHub-hosted or self-hosted runners, and you can use labels to classify runners according to various attributes. The following table compares how the distributed build concept is implemented for both Jenkins and GitHub Actions.

```

# Integrating Terraform with GitHub Actions:

## Introduction to Terraform:
Terraform is an infrastructure as code (IaC) tool that allows you to build, change, and version infrastructure safely and efficiently. This includes low-level components such as compute instances, storage, and networking, as well as high-level components such as DNS entries, SaaS features, etc.

So how we can integrate terraform with github actions ? Find answer below.

Create a repository with any name here, i created two directories.

1. `.github/workflows` → In this folder we will be having github action .yml file.
2. `terraform_github_actions_example` → In this folder, we will write terraform files (.tf)


<p align="center">
  <img width="1000" height="300" src="https://miro.medium.com/max/1094/1*aw3H9yuXR5wALAt97XZOyQ.png">
</p>

Now you have to create the terraform `.tf` files in the other folder. So here in the `terraform_github_actions_example` i have placed `.tf` file. In one file only i have given provider, variables and resource section.


<p align="center">
  <img width="800" height="6000" src="https://miro.medium.com/max/1094/1*TxckDrnW01UGT8gPp96SGw.png">
</p>

Below is the github action .yml code. This code is placed inside `.github/workflows` directory. The name of the of the job is `terraform-github-actions`. This job will run on every push and pull-request whereas in the env section you have to pass the `AWS_SECRET_KEY` and `AWS_SECRET_ACCESS_KEY`. So, terraform can take this variables and its respective values. In the build section you have to specify the image name and commands in the run section.

<p align="center">
  <img width="1000" height="500" src="https://miro.medium.com/max/1094/1*qoUXNvKZ-8jLndk9gZdwNQ.png">
</p>

Now as soon as you commit your job will run automatically. Click on start commit and then write some comments and then commit. Then move to Actions section there you will find the job summary.

<p align="center">
  <img width="1000" height="400" src="https://miro.medium.com/max/1094/1*Uw4j8htZSUdu1mniK_DGwQ.png">
</p>

Now you will see job with name terraform-github-action in left side and you will see the job running on the right side.


<p align="center">
  <img width="1000" height="250" src="https://miro.medium.com/max/1094/1*Eqh2-IjF5KQu9Kgm2YcNeQ.png">
</p>

Drag down to each successful step and then you will find the output of the commands i.e (`terraform init`, `validate`, `plan`, `apply`)

<p align="center">
  <img width="1000" height="500" src="https://miro.medium.com/max/1094/1*35v7WHICexLe_QwMmBAnfA.png">
</p>

After running the job you will see that all the steps run perfectly and there was no error. So you will have a grey color tick mark as the each steps run successfully.

<p align="center">
  <img width="600" height="200" src="https://miro.medium.com/max/781/1*q03CSUEolWKFxgU9C8HBSw.png">
</p>

Now after that navigate to aws and then see the resources launched or not.

## Following Resources Launched in AWS:

security group created successfully
![hello](https://miro.medium.com/max/1094/1*t3g7sC6v692608QDhk7WFg.png)


Internet Gateway created successfully
![hello](https://miro.medium.com/max/1094/1*wwCAYnIUzsut8KzYB5VR4A.png)

VPC created successfully
![hello](https://miro.medium.com/max/1094/1*bczadHtYFpzfV9uenhFIrA.png)

Subnet created successfully
![hello](https://miro.medium.com/max/1094/1*qMqSTyOIOd9NF3kQlL-89w.png)

Routing Table created successfully
![hello](https://miro.medium.com/max/1094/1*LuWrz8dnlH3KOu4Lbrbsjg.png)

ec2_launched successfully
![hello](https://miro.medium.com/max/1094/1*r7lmz_gl_WxgjwTTIA9Ujw.png)

I hope you will find this `automation article` interesting 🤩🤩

