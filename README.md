# Helm-practice

## Solution:

- The mainly objective with this activity is getting familiarized with Kubernetes helm.
- In this case we are going to expose to our localhost a single python application.

## Step followed:

### Step #1: Creating base structure

The command used in this step was.

````
helm create hello-world-python
````
That indicate we are going to create a helm chart called ``hello-world-python`` that follows this structure:

````
hello-world-python/
├── Chart.yaml
├── values.yaml
├── charts/
├── templates/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   ├── hpa.yaml
│   ├── httproute.yaml
│   ├── serviceaccount.yaml
│   ├── _helpers.tpl
│   └── tests/
│       └── test-connection.yaml
└── .helmignore
````

## Step #2: Customizing with our values

In order to deploy the required application was required to modify some values of the file.

````yaml
image:
  repository: icesiops/hello-world-python
  # This sets the pull policy for images.
  pullPolicy: IfNotPresent
  # Overrides the image tag whose default is the chart appVersion.
  tag: "0.0.1"
````

- In this case we had to use the image ``hello-world-python`` who was saved in the ``icesi-ops`` dockerhub repository.
- We specified our application tag according to the information provided in dockerhub.

````yaml
service:
  # This sets the service type more information can be found here: https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types
  type: ClusterIP
  # This sets the ports more information can be found here: https://kubernetes.io/docs/concepts/services-networking/service/#field-spec-ports
  port: 5000
````
- We specified the type of service as Cluster-IP.
- We defined the application port (5000) according to the source code given.

## Step #3: Deploying our chart

Once the values are configured correctly. The next step is deploying our chart.

````
helm install hello-world-python <pathtochart>
````
<p align="center">
  <img width="1380" height="288" alt="image" src="https://github.com/user-attachments/assets/32d7bb3c-260d-471e-a5b5-57aab01c7504" />
</p>

We can also get the pods, services and deployment asociated with ``hello-world-python``.

````
kubectl get svc,po,deploy
````

<p align="center">
  <img width="1130" height="308" alt="image" src="https://github.com/user-attachments/assets/4a7e0bca-c660-4bad-b260-68b5b8761095" />
</p>  


## Step #4: Accesing to our application.

Finally we can access to our python application using the ip and given in the step #3.

<p align="center">
  <img width="1214" height="90" alt="image" src="https://github.com/user-attachments/assets/f1d3dd59-419c-4c5f-a74f-e624989bb534" />
</p> 

<p align="center">
  <img width="799" height="172" alt="image" src="https://github.com/user-attachments/assets/ed9f1781-aa9f-412c-9af9-d204512700d9" />
</p> 
