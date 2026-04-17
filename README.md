# unipds-infra-cloud

## structures

### Deployment
Um Deployment é responsável

### Replicaset

### Pod

### services
#### secret
#### mapconfig

## Healthy

### liveness

### readiness

## Horizontal Pod Autoscaler - HPA
Ajusta automaticamente o número de réplicas em um Deployment, Statefulset ou Replicaset
baseado no uso de CPU/memória ou em méticas customizadas

```bash
$ kubectl get hpa
```
Em uma das colunas aparecerá o uso de CPU, algo como:
```bash
cpu: <unknown>/50%
```

Será necessário criar um servidor de métricas para que o HPA consiga capturar as métricas

### Metric Server
Baixe o arquivo yaml aqui: [https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.8.1/components.yaml](https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.8.1/components.yaml)

Edite-o, adicionando, nos argumentos do container, um trecho para aceitar requisições inseguras (quando for ambiente de desenvolvimento)

```Dockerfile
- --kubelet-insecure-tls
```

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.8.1/components.yaml
```

Após um tempo, já será possível ter métricas do HPA

```bash
$ kubectl get hpa
```
Em uma das colunas aparecerá o uso de CPU, algo como:
```bash
cpu: 10%/50%
```

> Observação: esses valores são apenas para teste e verificar o scale up em funcionamento