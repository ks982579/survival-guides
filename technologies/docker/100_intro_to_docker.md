> "Docker & Kubernetes: The Practical Guide \[2023 Edition\]" by Academind, Maximilian Schwarzmuller

# Intro to Docker

## Chapter 1: Getting Started

### Lesson 1: Welcome to the course

Docker and Kubernetes make managing and deploying, as well as developing, complex applications much easier. We will dive into what docker is and what are containers, which is the backbone of this technology. We will also discuss how to setup containers and which docker commands to run, and what the commands do. We will learn how docker can be setup locally and used with simple and complex projects, and how docker can be used in deployment. 

Then, we can look at Kubernetes, understand what it is and how it is connected with docker / works in tandem with docker. That means understand the same concepts, development and deployment of simple to complex projects, and understanding the advantages Kubernetes can offer. 

### Lesson 2: What is Docker?

If you ever need technical resources check out [docs.docker.com](https://docs.docker.com/). These will be my notes as I learn docker but always refer to the official documentation if anything is unclear. I will aim for the information to be accurate, but it might not be complete in that it won't cover every concept like the documentation will. 

**What is docker?** Docker is a **container** technology, a tool used for creating and managing containers. So then, what is a container? In software development, a container is a _standardized_ unit of software; a package of code and dependencies to run that code. If it's still unclear, think running some python code, what do you need? You will need the source code to run, dependencies the code uses, the python runtime, and an operating system... it's the whole bag of chips. 

Why would we want to use containers? Seems like a lot of work. However, the same container always yields the same exact application and execution behaviour, regardless where it is being executed. If you only have python 3.6 on your laptop, but the application requires at least 3.9, the application can run in a container independently from the outdated version on your local machine. Once more, you wouldn't have to `pip install` any dependencies either, or you shouldn't have to, and so there shouldn't be package conflicts either. 

You can think of it like picnic basket, it holds the food and silverware. You can share it with a friend, and no matter where you go or who has it, everyone has the same meal and all they need in the basket to eat it. 

Containers aren't actually a docker specific thing. Support for containers is built into modern operating systems. Docker is a tool used to simplify the creation and management of containers. 

### Lesson 3: Why Docker and Containers?