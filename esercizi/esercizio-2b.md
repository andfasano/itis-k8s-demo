# Esercizio 2b

## Obiettivo
Creazione di un service per utilizzare il gioco 2048.

## Svolgimento
2. Crea un file `game2048-service.yaml` per creare un nuovo service:
```
apiVersion: v1
kind: Service
metadata:
  name: game2048-service
spec:
  type: NodePort
  ports:
    - port: 8080
      nodePort: 30545
      targetPort: 80
  selector:
    app: "2048"
```
3. Crea il service:
```
$ $ kubectl apply -f game2048-service.yaml
```
4. Verifica che il service sia stato creato:
```
$ kubectl get service
```
5. Ottieni l'IP del nodo worker `minikube-m02`:
```
$ kubectl get nodes -o wide
```
6. Collegati al gioco utilizzando l'IP del nodo e la porta specificata nel service utilizzando un browser. Buon divertimento!

7. Proviamo adesso a simulare un problema, fermando il nodo worker:
```
$ minikube node stop minikube-m02
```
8. Verifica che il nodo worker sia in stato `NotReady`
```
$ kubectl get nodes -o wide
```
8. Verifica che il gioco non sia piu' disponibile tramite browser
9. Prova a collegarti al gioco utilizzando l'IP dell'unico nodo attivo, verificando che sia disponibile.
10. Rimuovi il cluster:
```
$ minikube delete
```

