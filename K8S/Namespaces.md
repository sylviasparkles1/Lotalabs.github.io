<h1>Namespaces</h1>
* Namespaces are a way to organize clusters into virtual sub-clusters — they can be helpful when different teams or projects share a Kubernetes cluster. Any number of namespaces are supported within a cluster, each logically separated from others but with the ability to communicate with each other.
* When the cluster is initially set up, default namespaces are created to group pods, microservices or resources into one namespace. The second namespace set is Kube-system and then the Kube-public.
* kube-system—a default space for Kubernetes system objects, such as kube-dns and kube-proxy, and add-ons providing cluster-level features, such as web UI dashboards, ingresses, and cluster-level logging. This is like a back up of the default namespace in case it is lost or accidentally deleted.
* kube-public—a default space for resources available to all users without authentication.
<h2>Namespace Isolation</h2>
* If the environment is small and not expanding, you can keep using the same namespaces, but in cases of enterprise or production you can decide to create your own namespaces. For instance- If the same cluster is used in both Dev and Prod environment, but at the same time you want isolate the resources between them, you can create a different namespace for each of them so in that way while working in the same Dev environment, you do not accidentally modify the resources in Production.
<h2>Namepace-Resource Limits</h2>

