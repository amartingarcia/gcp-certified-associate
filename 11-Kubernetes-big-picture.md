# Kubernetes Big Picture
## Big Picture
![k8s big picture](img/k8s_big_picture.png)

## The Kubernetes API
![k8s api](img/k8s_api.png)

* __Alpha__: Hairy! User beware! (eg _v1alpha1_)
* __Beta__: Taking shape. Becoming stable. (eg. _v2beta1_)
* __GA__: Ready for production (eg. _v1_, _v2_)

## Kubernetes Objects
* POD:
  * Contains one or more containers
  * Atomic unit of scheduling
  * Object on the cluster
  * Defined in the __v1__ API group
* Deployment:
  * Object on the cluster
  * Defined in the __apps/v1__ API group
  * Scaling
  * Rolling updates

![k8s multiple objects](img/k8s_multiple_objects.png)