workshop 1 kubernetes architecture

![workshop1](./workshop1.png)

switch kubectl context to docker desktop

```kubectl config use-context docker-desktop```

check kubectl current context

```kubectl config current-context```

list of kubectl contexts

```kubectl config get-contexts```

create workshop1 namespace

```kubectl apply -f ./workshop1/hello-springboot-namespace.yaml```

You will see 'workshop1' on lists after execute following command

```kubectl get ns```

Deploy hello-spring-boot application

```kubectl apply -f ./workshop1/hello-springboot-deployment.yaml```

Watch deployment, `-n` is used to specify namespace, specify the name is *workshop1*

```kubectl get deployment -n workshop1 --watch```

hello-spring-boot application should be in running status.

```kubectl get pods -n workshop1 --watch```

Access hello-spring-boot application through browser by *port-forward* method

```kubectl port-forward pod/{REPLACE YOUR POD NAME} 8888:10000 -n workshop1```

An example

```kubectl port-forward --address 0.0.0.0 pod/spring-boot-deployment-59f5d7f8c8-fcl85 8888:10000 -n workshop1```

Access http://127.0.0.1:8888/workshop1/home through browser, you should see **Hello, spring-boot-example!** message.

Create a service on hello-spring-boot application

```kubectl apply -f ./workshop1/hello-spring-boot-service.yaml```

Describe spring-boot-service to view more information, etc IP, Type, Endpoints...

```kubectl describe service spring-boot-service -n workshop1```

Access hello-spring-boot application through spring-boot-service

```kubectl port-forward service/spring-boot-service 9888:9091 -n workshop1```

Access http://127.0.0.1:9888/workshop1/home through browser, you should see **Hello, spring-boot-example!** message.