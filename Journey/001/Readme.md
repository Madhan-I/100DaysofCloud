**Add a cover photo like:**
![placeholder image](https://via.placeholder.com/1200x600)

# Build a Website using Google Kubernetes Engine on Google Cloud

## We are going to see on how to create a website on google cloud using Google Kubernetes Engine and also to complete the Challenge lab in Qwiklabs.

This topic covers basic steps on how to create a monolithic web app into microservices, Deploying and exposing microservices deployed on GKE 

## Prerequisite
I would recommend people to go through Hands-on-Lab on building a Website on Google Cloud to get familiar, so that you will confidence on completing the challenge lab without scrolling down.


Basic knowledge on GCP would be handy.

## Use Case

- 🖼️ (Show-Me) Create an graphic or diagram that illustrate the use-case of how this knowledge could be applied to real-world project
- Your task is to take the company's existing monolithic e-commerce website and break it into a series of logically separated microservices. The existing monolith code is sitting in a GitHub repo, and you will be expected to containerize this app and then refactor it.
- You will be tasked with pulling down the source code, building a container from it (one of the farmers left you a Dockerfile), and then pushing it out to GKE

## Cloud Research

- ✍️ Document your trial and errors. Share what you tried to learn and understand about the cloud topic or while completing micro-project.
- 🖼️ Show as many screenshot as possible so others can experience in your cloud research.

## Try yourself

✍️ Add a mini tutorial to encourage the reader to get started learning something new about the cloud.

### Step 1 — Download the monolith code and build your container

Log in to your new project, open up Cloud Shell.

First things first, you'll need to clone your team's git repo. There's a setup.sh script in the root directory of the project that you'll need to run to get your monolith container built up.

After running the setup.sh script, there will be a few different projects that can be built and pushed.

Push the monolith build (conveniently located in the monolith directory) up to the Google Container Registry. There's a Dockerfile located in the ~/monotlith-to-microservices/monolith folder which you can use to build the application container.

You will have to run Cloud Build (in that monolith folder) to build it, then push it up to GCR.

Name your artifact as follows:
![alt text]

Hint:

Make sure that you submit a build named "fancytest" with a version of "1.0.0".

![Screenshot](https://via.placeholder.com/500x300)

### Step 1 — Summary of Step

![Screenshot](https://via.placeholder.com/500x300)

### Step 3 — Summary of Step

![Screenshot](https://via.placeholder.com/500x300)

## ☁️ Cloud Outcome

✍️ (Result) Describe your personal outcome, and lessons learned.

## Next Steps

✍️ Describe what you think you think you want to do next.

## Social Proof

✍️ Show that you shared your process on Twitter or LinkedIn

[link](link)
