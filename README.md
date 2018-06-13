Hiatus
======

Hiatus is a proposal of a tool that is capable of replacing and creating Kubernetes files (deployments, services) from reading metadata input such as json.


Parsing
-------

I have been thinking something like a simple sed to parse the streaming input and replace internal variables

``` ssh
sed "
s/<latest-ver>/$(git rev-parse HEAD)/g; 
s/<application-name>/my-api-example/g;
s/<project-id>/my-project-id/g;
s/<registry>/gcr.io/g" Kubernetes/deployment.yaml | kubectl apply -f -
```

Input
-----

Input files could cover as JSON or some other metadata with the following input: 


``` json
{
    registry: gcr.io,
    project-id: my-project-id,
    application-name: my-api-example,
    port: 30001,
    targetPort: 30001,
    imagePullPolicy: Always,
    type: Deployment | Service 
}
```

Incoming ideas are also welcome :)