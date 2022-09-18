```Kubectl``` is a command-line tool for communicating with the Kubernates cluster


The following is the command of kubectl.


***


###get###


```Kubectl get $(resource)``` shows information about Kubernetes resources


Below are the options for kubectl


```-o $(command)```

* wide : show more info
* json : show format json

```
kubectl get [(-o|--output=)json|yaml|name|go-template|go-template-file|

template|templatefile|jsonpath|jsonpath-as-json|jsonpath-file|

custom-columns|custom-columns-file|wide] (TYPE[.VERSION][.GROUP] [NAME | 

-l label] | TYPE[.VERSION][.GROUP]/NAME ...) [flags]
```

###run###
```kubectl run```

