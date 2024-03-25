# Esercizio 5 (*)

## Obiettivo
Crea un deployment per pubblicare una pagina web statica, utilizzando Apache HTTP server.

## Svolgimento
Crea un deployment con un container httpd (puoi trovare maggiori informazioni sulla relativa 
immagine qui: https://hub.docker.com/_/httpd). Configura il container httpd affinche' monti 
il percorso `/usr/local/apache2/htdocs/` da un volume di tipo `emptyDir`.
Aggiungi nel deployment un secondo container (del tipo che preferisci) responsabile della generazione
della pagina html statica che dovra' essere pubblicata da httpd. La pagina deve contenere (almeno)
il testo `"Hello, ITIS Galileo Galilei!"`.
Crea inoltre un service di tipo NodePort per accedere la pagina web via browser.

*Bonus:* aggiungi un ingress in modo simile all'esercizio 4.
