# Esercizio 1

## Obiettivo
Creazione e gestione di un singolo pod.

## Sovlgimento
1. Crea un cluster con minikube:
```
$ minikube start
```
2. Crea un file `apache-pod.yaml` per definire un pod con un container basato su Apache HTTP server. 
   Utilizza il seguente template:
```
apiVersion: v1
kind: Pod
metadata:
  name: apache-pod
spec:
  containers:
  - name: apache-container
    image: httpd:latest
    ports:
    - containerPort: 80
```
3. Crea il pod:
```
$ kubectl apply -f apache-pod.yaml
```
4. Verifica lo stato del pod con il seguente comando, ed attendi che sia `Running`:
```
$ kubectl get pods
```
5. Accedi al container del pod per verificare che sia in esecuzione correttamente:
```
$ kubectl exec -ti apache-pod -- /bin/bash
```
6. Esci dal container e rimuovi il pod:
```
$ kubectl delete pod apache-pod
```
7. Rimuovi il cluster:
```
$ minikube delete
```