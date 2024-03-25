# Esercizio 6 (*)

## Obiettivo
Crea un deployment per pubblicare una pagina web dinamica, utilizzando Apache HTTP server.

## Svolgimento
In modo simile all'esercizio 5, crea un deployment con un container, configurato affinche'
monti una directory da un volume condiviso.
Per il secondo container invece devi creare una applicazione in Java che continuamente, ogni 5
secondi, scriva la data e l'ora corrente (piu' un messaggio a piacere) nel volume condiviso,
in modo tale che sia pubblicato dal web server.
L'applicazione deve essere compilata e distribuita all'interno di un'immagine.
Per caricare l'immagine in minikube utilizza il seguente comando:
```
$ minikube image build -t my_java_app .
```
> [!NOTE]
> Ricordati di configurare `imagePullPolicy: IfNotPresent` per il container scrittore, in modo
> che possa recuperare l'immagine correttamente.

*Bonus:* aggiungi un ingress in modo simile all'esercizio 4.
