# Esercizio 4

## Obiettivo
Utilizzo di un ingress per accedere ad un service interno al cluster.

## Svolgimento
1. Crea un cluster:
```
$ minikube start
```
2. Per utilizzare un ingress in minikube, e' necessario abilitare un addon:
```
$ minikube addons enable ingress
```
3. Verifica che l'ingress ngnix sia attivo:
```
$ kubectl get pods -n ingress-nginx
```
4. Crea il file `helloworld-deployment.yaml` con il seguente contenuto,
e crea il deployment:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world-deployment
spec:
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
        - name: hello-world
          image: gcr.io/google-samples/hello-app:1.0
          ports:
            - containerPort: 8080
```
5. Crea il file `helloworld-service.yaml` con il seguente contenuto,
e crea il service:
```
apiVersion: v1
kind: Service
metadata:
  name: hello-world-service
spec:
  ports:
    - name: http
      port: 80
      targetPort: 8080
      protocol: TCP
  type: ClusterIP
  selector:
    app: hello-world
```
6. Crea il file `helloworld-ingress.yaml` con il seguente contenuto,
e crea l'ingress:
```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: helloworld-ingress
spec:
  rules:
    - host: helloworld.local
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: hello-world-service
                port:
                  number: 80
```
8. Verifica che l'ingress sia stato creato correttamente:
```
$ kubectl get ingress
```
Annota l'ip riportato nella colonna `ADDRESS`
9. Modifica il file `/etc/hosts/` aggiungendo una nuova riga in fondo al file,
sostituendo `<IP>` con il valore precedentemente annotato:
```
<IP> helloworld.local
```
> [!WARNING] 
> Presta attenzione quando editi il file `/etc/hosts`!
> Non cancellare il contenuto esistente!
10. Verifica che sia possibile accedere al servizio tramite browser
11. Prova a modificare direttamente l'ingress, modificando il field `port.number` da `80` a `9999`:
```
$ kubectl edit ingress helloworld-ingress
```
12. Verifica che il service non sia piu' raggiungibile tramite browser
13. Edita nuovamente l'ingress, riportando la porta corretta, e verifica l'accesso tramite browser.
14. Modifica il file `/etc/hosts/` rimuovendo *solo* la riga precedentemente aggiunta.
10. Rimuovi il cluster:
```
$ minikube delete
```
