# k8s_wildfly



# k8s_wildfly

Projeto para preparar o Servidor Wildfly em Ambiente do Kubernetes.

- Instalação do Docker

- Instalação do Kubernetes

Para preparar o Servidor Wildfly em ambiente Kubernetes, temos que ter alguns manifestos do Kubernetes que seria o Deployments,Services e Ingress.

- Deployments:

Na configuração de Deployments, replicas especifica o número desejado de pods replicados com o rótulo igual à matchLabels diretiva que está no formato chave, valor. Se houver vários rótulos, eles são AND, o que significa que podemos ter tantos rótulos de pod, mas que devem corresponder pelo menos a todos os matchLabelspares de chave e valor.

Esses pares de rótulos de valor-chave facilitam a filtragem dos recursos com base no rótulo. Por exemplo, se adicionarmos rótulo tier: backendaos serviços de implantação de back-end, podemos obter a lista de implantação com

- Service

Temos pods rodando no cluster Kubernetes que precisa estar conectado de alguma forma. Esse é o trabalho do Serviço.

O serviço abstrai os endereços IP do pod para um nome de serviço estático para que as solicitações externas possam ser enviadas por proxy para vários pods. Temos diferentes tipos de serviços: NodePort, ClusterIP, LoadBalancer que discutiremos em outro post.

O proxy de solicitações para o pod desejado é baseado na selectorespecificação do serviço que deve corresponder aos rótulos de metadados no pod.

- Ingress

O serviço pode ser usado apenas dentro do cluster. Para, ex. dentro do cluster podemos acessar o nginx com o comando curl http://my-serviceonde my-serviceestá o nome do serviço com seletor para o pod do nginx.

Agora, precisamos configurar a maneira de acessar os serviços fora do cluster via endereço IP ou alguma URL. A entrada vem aqui também para terminação SSL para balanceamento de carga.

Um Ingress é uma coleção de regras que permitem que conexões de entrada alcancem os serviços de cluster.

A especificação de entrada deve fornecer o nome do serviço como back-end ( my-serviceno caso acima) e a porta ( servicePort)que é exposta pelo serviço junto com a rota de URL (/api, /login) ou host baseado em nome (api.example.com, login.example .com)

- com os manifestos escritos e revisados, os comandos realizar a execução dos pods vão ser apresentados a seguir.

Comandos:

kubectl create -f /k8s/deployments/

kubectl create -f /k8s/ingress/

kubectl create -f /k8s/services/

*Esses comandos executam os arquivos no cluster criando suas entidades.

