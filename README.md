# k8s_wildfly - Project under test

Project to prepare Wildfly Server in Kubernetes Environment.

- Docker installation

- Installing Kubernetes

To prepare the Wildfly Server in Kubernetes environment, we have to have some Kubernetes manifests that would be Deployments, Services and Ingress.

- Deployments:

In the Deployments configuration, replicas specifies the desired number of replicated pods with the label equal to the matchLabels directive which is in the form key, value. If there are multiple labels, they are AND, which means we can have as many pod labels, but they must match at least all matchLabels key and value pairs.

These key-value label pairs make it easy to filter resources based on the label. For example, if we add label tier: backend to the backend deployment services, we can get the deployment list with

- Service

We have pods running on the Kubernetes cluster that need to be connected somehow. That's the job of the Service.

The service abstracts the pod's IP addresses to a static service name so that external requests can be proxied to multiple pods. We have different types of services: NodePort, ClusterIP, LoadBalancer which we will discuss in another post.

Proxying requests to the desired pod is based on the service specification selector that must match the metadata labels on the pod.

- Ingress

The service can only be used within the cluster. For eg inside the cluster we can access nginx with the curl command http://my-service where my-service is the name of the service with selector for the nginx pod.

Now, we need to configure the way to access services outside the cluster via IP address or some URL. The entry comes here also for SSL termination for load balancing.

An Ingress is a collection of rules that allow incoming connections to reach cluster services.

The input spec must provide the service name as backend ( my-service in the above case) and the port ( servicePort) that is exposed by the service along with the URL route (/api, /login) or host based on name (api.example.com, login.example .com)

- with the manifests written and revised, the commands to execute the pods will be presented below.

Commands:

- kubectl create -f /k8s/deployments/

- kubectl create -f /k8s/ingress/

- kubectl create -f /k8s/services/

to expose the IP of the node the pod is contained in:

- minikube service serve --url

*These commands run the files on the cluster creating their entities.

references:

- https://hub.docker.com/r/bitnami/wildfly

- https://kubernetes.io/pt-br/docs/home/

------------------------------------------------------------------------------------------------------------------------------------------------------

# k8s_wildfly - Projeto em teste

Projeto de prepara????o do servidor Wildfly em ambiente Kubernetes.

- Instala????o do Docker

- Instalando Kubernetes

Para preparar o servidor Wildfly no ambiente Kubernetes, temos que ter alguns manifestos do Kubernetes que seriam Deployments, Services e Ingress.

- Deployments:

Na configura????o Deployments, as r??plicas especificam o n??mero desejado de pods replicados com o r??tulo igual ?? diretiva matchLabels que est?? na chave do formul??rio, valor. Se houver v??rios r??tulos, eles ser??o AND, o que significa que podemos ter tantos r??tulos de pod, mas eles devem corresponder a pelo menos todos os pares de chave e valor matchLabels.

Esses pares de r??tulos de valores-chave facilitam a filtragem de recursos com base no r??tulo. Por exemplo, se adicionarmos label tier: back-end aos servi??os de implanta????o de back-end, podemos obter a lista de implanta????o com

- Service

Temos pods em execu????o no cluster Kubernetes que precisam ser conectados de alguma forma. Esse ?? o trabalho do Servi??o.

O servi??o abstrai os endere??os IP do pod para um nome de servi??o est??tico para que solicita????es externas possam ser enviadas por proxy para v??rios pods. Temos diferentes tipos de servi??os: NodePort, ClusterIP, LoadBalancer que discutiremos em outro post.

As solicita????es de proxy para o pod desejado s??o baseadas no seletor de especifica????o de servi??o que deve corresponder aos r??tulos de metadados no pod.

- Ingress

O servi??o s?? pode ser usado dentro do cluster. Por exemplo, dentro do cluster podemos acessar o nginx com o comando curl http://my-service onde my-service ?? o nome do servi??o com seletor para o pod nginx.

Agora, precisamos configurar a forma de acesso aos servi??os fora do cluster via endere??o IP ou alguma URL. A entrada vem aqui tamb??m para termina????o SSL para balanceamento de carga.

Um Ingress ?? uma cole????o de regras que permitem que conex??es de entrada alcancem servi??os de cluster.

A especifica????o de entrada deve fornecer o nome do servi??o como backend ( my-service no caso acima) e a porta ( servicePort ) que ?? exposta pelo servi??o junto com a rota de URL (/api, /login) ou host com base no nome (api .example.com, login.example .com)

- com os manifestos escritos e revisados, os comandos para execu????o dos pods ser??o apresentados a seguir.

Comandos:

- kubectl create -f /k8s/deployments/

- kubectl create -f /k8s/ingress/

- kubectl create -f /k8s/services/

para expor o IP do n?? em que o pod est?? contido:

-  minikube service serve --url

*Esses comandos executam os arquivos no cluster criando suas entidades.

refer??ncias:

- https://hub.docker.com/r/bitnami/wildfly

- https://kubernetes.io/pt-br/docs/home/


