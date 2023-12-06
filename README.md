# kustomize-example
Small example how to use kustomize to configure and reuse k8s manifests.  
It' especially useful for working with ArgoCD and builtin with the kubectl binary.  

## Directories
In the **base**-directory the original manifest files are placed.  
In this case, there is just a simple deployment.  
There is also a kustomization file, that just references everything in this directory.  

In the **overlays**-dir all the different configurations are stored. Using the strategicMergePatch allows to update the fields, but not remove or add, for this the JSONPatch would be needed.  
The **development** dir contains the configuration for the dev environment, and the **prod** dir for the production env.  

The kustomization files in these dirs reference to the base directory and the patches to apply.  

## kustomize commands
The different manifests can be build using this command in the respective folder:
```
kubectl kustomize
```
Which will result in a yaml manifest file.  

Piping its output to kubectl we can just apply it to the cluster.
```
k kustomize | k apply -f -
```