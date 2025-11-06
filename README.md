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

