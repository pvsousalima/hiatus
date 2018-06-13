Hiatus
======
Some people of my team do not like to write k8 files because they tend to think it is too verbose and not worth thinking of.

JSON version based are also not straightforward and do have some crazy compatibility with k8s.

So I bring Hiatus.

Hiatus is a proposal of a tool that is capable of replacing and creating Kubernetes files (deployments, services) from reading metadata input such as json.

Parsing
-------

I have been thinking something like a simple sed to parse the streaming input and replace internal variables.

``` ssh
sed "
s/<latest-ver>/$(git rev-parse HEAD)/g; 
s/<application-name>/my-api-example/g;
s/<project-id>/my-project-id/g;
s/<registry>/gcr.io/g" Kubernetes/deployment.yaml | kubectl apply -f -
```

However I think that some templating would do better, as the tool would be also capable of creating a whole deployment file from multiple templates.

Input
-----

Input files could cover as JSON or some other metadata with the following input: 


```
{
    registry: gcr.io,
    projectid: my-project-id,
    applicationname: my-api-example,
    port: 30001,
    targetPort: 30001,
    imagePullPolicy: Always,
    type: Deployment | Service 
}
```

Incoming ideas are also welcome :)