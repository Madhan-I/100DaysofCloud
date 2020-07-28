![pic 1](https://user-images.githubusercontent.com/55656091/88679033-abc74f00-d10c-11ea-802c-5c2319144e04.JPG)


# Build a Website using Google Kubernetes Engine on Google Cloud

## We are going to create a website on google cloud using Google Kubernetes Engine along with steps to complete the Challenge lab in Qwiklabs.

This topic covers below list of tasks, 

- Building and refactoring a monolithic web app into microservices
- Deploying microservices in GKE
- Exposing the Services deployed on GKE

## Prerequisite
I would recommend to go through Hands-on-Lab on building a Website on Google Cloud, so that you will familiarize yourself on completing the challenge lab without scrolling down.

Basic knowledge on GCP would be handy.

## Use Case

- Your task is to take the company's existing monolithic e-commerce website and break it into a series of logically separated microservices. The existing monolith code is sitting in a GitHub repo, and you will be expected to containerize this app and then refactor it.
- You will be tasked with pulling down the source code, building a container from it (one of the farmers left you a Dockerfile), and then pushing it out to GKE

## Try yourself

✍️ We will be completing with below steps, Hope it's useful.

### Step 1 — Download the monolith code and build your container

Log in to your new project, open up Cloud Shell.

First you need to clone the team's git repo. There's a setup.sh script in the root directory of the project that you'll need to run to get your monolith container built up.

COMMAND:

![s1](https://user-images.githubusercontent.com/55656091/88682807-bc79c400-d110-11ea-805b-972a6fa08a2e.JPG)

Next, Run the setup.sh to install the NodeJS dependencies for the monolith code

COMMAND:

![s2](https://user-images.githubusercontent.com/55656091/88682844-c7ccef80-d110-11ea-862a-e6382adb16ae.JPG)

Before building the Docker container, you can preview the monolith application on port 8080 by running the following commands to start the web server:

COMMAND:

![s3](https://user-images.githubusercontent.com/55656091/88682923-dd421980-d110-11ea-8675-cb16b3011de0.JPG)

Next Push the monolith build up to the Google Container Registry. There's a Dockerfile located in the ~/monotlith-to-microservices/monolith folder which can be used to build the application container.

Name your artifact as follows:

![S5](https://user-images.githubusercontent.com/55656091/88684300-54c47880-d112-11ea-8ceb-cd3c38c68408.JPG)

COMMAND:

![s4](https://user-images.githubusercontent.com/55656091/88683255-37db7580-d111-11ea-8470-0a2a67ccc00b.JPG)

### Step 2 — Create a kubernetes cluster and deploy the application

Now that you have created the image and it is in container registry, it's time to create a cluster to deploy it to.

Create the resources in us-central1-a zone, before that you'll need to create a GKE cluster named as "fancy-cluster". Start with a 3 node cluster to begin with.

Create your cluster as follows:

![S6](https://user-images.githubusercontent.com/55656091/88684388-6efe5680-d112-11ea-92f7-8a4c123e8733.JPG)

COMMAND:

![s8](https://user-images.githubusercontent.com/55656091/88685775-f00a1d80-d113-11ea-9d97-a9caba21d52b.JPG)

Now that you've built up an image, and have a cluster up and running, it's time to deploy your application.

Create and expose your deployment as follows:

![S7](https://user-images.githubusercontent.com/55656091/88684582-a79e3000-d112-11ea-804a-5c2076ee099b.JPG)

Make note of the IP address that is assigned in the expose deployment. You should now be able to visit this IP address from your browser!

You should see the following:

![s9](https://user-images.githubusercontent.com/55656091/88685971-2e074180-d114-11ea-9510-ad4b3dfdd4df.JPG)

After the cluster is ready, you need to deploy the application. Make sure that you name the deployment to be “fancytest”, expose the service on port 80 and map it to port 8080.

COMMAND:

![t1](https://user-images.githubusercontent.com/55656091/88686223-80486280-d114-11ea-874f-675ecf2533d5.JPG)

### Step 3 — Create a containerized version of your Microservices

There are 3 services that need to be broken out into their own containers. 
Since you are moving all of the services into containers, you need to track the following information for each service:

 - The root folder of the service (where you will build the container)
 - The repository you will upload the container to
 - The name & version of the container artifact

Below is the set of services which need to be containerized. Navigate to the source roots mentioned below, and upload the artifacts which are created to the Google Container Registry with the metadata indicated.

![T2](https://user-images.githubusercontent.com/55656091/88688225-b850a500-d116-11ea-9c9f-1553f44f4e54.JPG)

To complete the above steps, use below command to Submit a build named "orders" with a version of "1.0.0"

COMMMAND:

![T3](https://user-images.githubusercontent.com/55656091/88688562-18dfe200-d117-11ea-9f45-0586cace468f.JPG)

Similarly, repeat the step for build named "products" with a version of "1.0.0"

COMMMAND:

![T4](https://user-images.githubusercontent.com/55656091/88688565-19787880-d117-11ea-8129-abf2f59d3bdb.JPG)

### Step 4 — Deploy the new microservices

Deploy these new containers following the same process that you followed for the "fancytest" monolith. 

Create and expose your deployments as follows:

![t5](https://user-images.githubusercontent.com/55656091/88689893-aff96980-d118-11ea-9a63-5a7be7e59eb1.JPG)

NOTE: Please make note of the IP address of both Orders and Products services once they have been exposed, you will need them in future steps.

Name the deployment to be “orders” and “products”, and expose the services on port 80.

Commands to deploy the Orders Microservice:

![T9](https://user-images.githubusercontent.com/55656091/88691159-1c289d00-d11a-11ea-9d30-904fd09dc13d.JPG)

Commands to deploy the Products Microservice:

![T91](https://user-images.githubusercontent.com/55656091/88691162-1cc13380-d11a-11ea-8d19-52ba893c1b36.JPG)

COMMAND to Check IP Address for Orders and Products:   

kubectl get all


You can verify whether the deployments are successful and the services have been exposed by going to the following URLs in your browser:

http://ORDERS_EXTERNAL_IP/api/orders

http://PRODUCTS_EXTERNAL_IP/api/products

You will see each service return a JSON string if the deployments were successful.

### Step 5 — Configure the Frontend microservice

Now that you have extracted both the Orders and Products microservice, you need to configure the Frontend service to point to them, and get it deployed.

Use the nano editor to replace the local URL with the IP address of the new Products microservices:

![T93](https://user-images.githubusercontent.com/55656091/88691521-96f1b800-d11a-11ea-8d0b-00540bead221.JPG)

When the editor opens, your file should look like this:

![t7](https://user-images.githubusercontent.com/55656091/88690505-5e9daa00-d119-11ea-8420-4b2c2de34cd2.JPG)

Replace the URL's to new format while replacing it with Orders and Product microservice IP addresses so it matches below:

![t8](https://user-images.githubusercontent.com/55656091/88690507-5f364080-d119-11ea-8e43-5906c34db62f.JPG)

Press __CTRL+O__, press __ENTER__, then __CTRL+X__ to save the file in the nano editor and rebuild the frontend app before containerizing it.

![T95](https://user-images.githubusercontent.com/55656091/88691828-f9e34f00-d11a-11ea-9717-0cc565cef003.JPG)

### Step 6 — Create a containerized version of the Frontend microservice

With the Orders and Products microservices now containerized and deployed, and the Frontend service configured to point to them, the final step is to containerize and deploy the Frontend.

Use Cloud Build to package up the contents of the Frontend service and push it up to the Google Container Registry.

Submit a build named "frontend" with a version of "1.0.0".

![t96](https://user-images.githubusercontent.com/55656091/88695796-04541780-d120-11ea-9092-4d1ffb062fa4.JPG)

COMMAND:

![T98](https://user-images.githubusercontent.com/55656091/88696051-5e54dd00-d120-11ea-9327-2e5874286657.JPG)

### Step 7 — Deploy the Frontend microservice

Deploy this container following the same process that you followed for the "Orders" and "Products" microservices.

Create and expose your deployment as follows:

![t97](https://user-images.githubusercontent.com/55656091/88695801-05854480-d120-11ea-8f0f-226567c7f5c0.JPG)

COMMAND:

![T99](https://user-images.githubusercontent.com/55656091/88696059-5eed7380-d120-11ea-9688-d225e4e107e6.JPG)

You can verify that the deployment was successful and that the microservices have been properly exposed by hitting the following the IP address of the frontend service in your browser: You will see the Fancy Store homepage, with links to the Products and Orders pages powered by your new microservices.


## ☁️ Cloud Outcome

✍️ With this challenge, I got familiarized on using microservices on GKE to create a website 

## Next Steps

✍️ Well, next I will be heading on with preparation on clearing AZ-900  

## Social Proof

✍️ 

https://www.linkedin.com/in/madhan-i-58241670/

https://twitter.com/Madhan2712
