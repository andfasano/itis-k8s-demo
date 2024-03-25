# Esercizio 7 (*)

## Obiettivo
Stesso obiettivo dell'esercizio 5, ma in questo caso e' richiesto che il web server ed il 
generatore di pagine siano collocati su due pod diversi, con la condivisione dei dati
attraverso un persistent volume. 

## Svolgimento
Crea un deployment separato per il web server, ed uno per il generatore della pagina statica,
con relativo service per accedere ad Apache via browser.
Entrambi i pod dovranno montare lo stesso persistent volume per la condivisione dei dati.
Crea quindi un PV di tipo `local`, consultando la documentazione ufficiale di Kubernetes
sui volumi a questo indirizzo: https://kubernetes.io/docs/concepts/storage/volumes/.
Crea un claim associato al PV da utilizzare in entrambi i pod.

[!NOTE] 
I PV di tipo `local` richiedono che il folder di destinazione sia gia' presente sull'host.
Poiche' stiamo utilizzando minikube con 1 nodo, puoi specificare il path `/home/docker`.
Puoi utilizzare il comando `minikube ssh` per accedere temporaneamente all'host e verificare
che il file condiviso sia stato generato correttamente.