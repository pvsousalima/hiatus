Hiatus
======
Some people of my team do not like to write k8 files because they tend to think it is too verbose and not easy to thinking of.

Think that *not only* SRE perform their long YAML writing job (if thats the case) but developers and some enthusiasts also like to perform quick tests and deploy stuff.

JSON version based are also not straightforward and do have some crazy compatibility with k8s.

So I thought of Hiatus.

Hiatus is a proposal of a tool that is capable of replacing and creating Kubernetes files (deployments, services) from reading metadata input such as json. Also I do think that most CLIs-based would have to deal with too many options and parse a lot of stuff.

Parsing
-------

I have been thinking something like a simple sed to parse the streaming input and replace internal variables.

``` ssh
sed "
s/<deployment-ver>/$(git rev-parse HEAD)/g;
s/<application-name>/my-api-example/g;
s/<project-id>/my-project-id/g;
s/<registry>/myregistry/g" Kubernetes/deployment.yaml | kubectl apply -f -
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
}
```

And the file type can be inferred from the extension. (Could be either .deployment.json or .service.json)

Incoming ideas are also welcome :)
