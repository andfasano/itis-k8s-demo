# Esercizio 2a

## Obiettivo
Creazione e gestione di un deployment del gioco 2048.

## Svolgimento
1. Crea un cluster con 2 nodi:
```
$ minikube start -n 2
```
2. Attendi di avere due nodi in stato `Ready` utilizzando il seguente comando:
```
$ kubectl get nodes -o wide
```
2. Crea un file `game2048-deployment.yaml` per eseguire il deployment del gioco 2048:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: "game2048-deployment"
spec:
  selector:
    matchLabels:
      app: "2048"
  replicas: 2
  template:
    metadata:
      labels:
        app: "2048"
    spec:
      containers:
        - image: alexwhen/docker-2048
          imagePullPolicy: Always
          name: "2048"
```
3. Crea il deployment:
```
$ $ kubectl apply -f game2048-deployment.yaml
```
4. Verifica che il deployment sia stato creato e sia `Ready`:
```
$ kubectl get deployments
```
5. Controlla che il replicaset sia stato creato:
```
$ kubectl get rs
```
6. Controlla i pod del deployment, ed osserva su quali nodi siano stati distribuiti:
```
$ kubectl get pods -o wide
```
7. Prova a cancellare uno dei pod:
```
$ kubectl delete pod <nome-pod>
```
8. Verifica che un nuovo pod sia stato creato dopo la cancellazione:
```
$ kubectl get pods -o wide
```
9. Controlla la sequenza di eventi
```
$ kubectl get events --sort-by='.metadata.creationTimestamp'
```
10. Prova ad aumentare a 5 il numero di repliche:
```
$ kubectl scale deployment game2048-deployment --replicas=5
```
11. Verifica che vi siano effettivamente 5 pod disponibili, ed osserva su quali nodi siano presenti:
```
$ kubectl get pods -o wide
```
12. Riporta a 2 il numero di repliche:
```
$ kubectl scale deployment game2048-deployment --replicas=2
```
13. Passa all'esercizio 2b