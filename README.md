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

Projeto de preparação do servidor Wildfly em ambiente Kubernetes.

- Instalação do Docker

- Instalando Kubernetes

Para preparar o servidor Wildfly no ambiente Kubernetes, temos que ter alguns manifestos do Kubernetes que seriam Deployments, Services e Ingress.

- Implantações:

Na configuração Deployments, as réplicas especificam o número desejado de pods replicados com o rótulo igual à diretiva matchLabels que está na chave do formulário, valor. Se houver vários rótulos, eles serão AND, o que significa que podemos ter tantos rótulos de pod, mas eles devem corresponder a pelo menos todos os pares de chave e valor matchLabels.

Esses pares de rótulos de valores-chave facilitam a filtragem de recursos com base no rótulo. Por exemplo, se adicionarmos label tier: back-end aos serviços de implantação de back-end, podemos obter a lista de implantação com

- Serviço

Temos pods em execução no cluster Kubernetes que precisam ser conectados de alguma forma. Esse é o trabalho do Serviço.

O serviço abstrai os endereços IP do pod para um nome de serviço estático para que solicitações externas possam ser enviadas por proxy para vários pods. Temos diferentes tipos de serviços: NodePort, ClusterIP, LoadBalancer que discutiremos em outro post.

As solicitações de proxy para o pod desejado são baseadas no seletor de especificação de serviço que deve corresponder aos rótulos de metadados no pod.

- Entrada

O serviço só pode ser usado dentro do cluster. Por exemplo, dentro do cluster podemos acessar o nginx com o comando curl http://my-service onde my-service é o nome do serviço com seletor para o pod nginx.

Agora, precisamos configurar a forma de acesso aos serviços fora do cluster via endereço IP ou alguma URL. A entrada vem aqui também para terminação SSL para balanceamento de carga.

Um Ingress é uma coleção de regras que permitem que conexões de entrada alcancem serviços de cluster.

A especificação de entrada deve fornecer o nome do serviço como backend ( my-service no caso acima) e a porta ( servicePort ) que é exposta pelo serviço junto com a rota de URL (/api, /login) ou host com base no nome (api .example.com, login.example .com)

- com os manifestos escritos e revisados, os comandos para execução dos pods serão apresentados a seguir.

Comandos:

- kubectl create -f /k8s/deployments/

- kubectl create -f /k8s/ingress/

- kubectl create -f /k8s/services/

para expor o IP do nó em que o pod está contido:

-  minikube service serve --url

*Esses comandos executam os arquivos no cluster criando suas entidades.

referências:

- https://hub.docker.com/r/bitnami/wildfly

- https://kubernetes.io/pt-br/docs/home/


