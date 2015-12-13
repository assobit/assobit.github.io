# Sito dell'associazione Assob.it

Il sistema Git, github, [github pages](https://pages.github.com/) costituiscono un insieme di strumenti molto utili per la manutenzione collaborativa di un sito Web e la nostra associazione deve basarsi necessariamente sulla collaborazione.

## Per cominciare (non esperti)

* Bisogna iscriversi a Github
* Seguire le istruzioni sulle [[FAQ | https://github.com/gabridome/gabridome.github.io/wiki/FAQ ]] per fare le operazioni comuni usando solo github.com

Le pull requests (modifiche proposte) sono attualmente valutate da me ma sono discusse pubblicamente. Spero prestissimo di avere collaboratori (più sono meglio sto).

### To have
Un sistema per dare al non esperto immediata visibilità delle sue modifiche. Se uno dei nostri legali fa modifiche a una parte di testo vorrà vedere come viene e sarebbe bello dargli la possibilità di apprezzare un 'anteprima delle modifiche. Attualmente github non visualizza anteprime di un tuo repository se non tramite github pages ed è possibile solo un sito github pages per account utente (da esplorare la possibilità di fare pagine di progetto con gh-pages).

## Per cominciare (esperti di git)
* Bisogna iscriversi a Github
* Fare un [fork](https://help.github.com/articles/about-forks/) di questo repository creando una copia sul proprio account github
* Clonare il repo in locale
* [Configurare il repository di origine come "upstream"] con il comanto git remote (il nostro fork su github è già configurato come "origin")
* [mantenerlo sincronizzato con quello di origine](https://help.github.com/articles/syncing-a-fork/)
In sintesi si tratta di recuperare spesso tutte le branch dal repository di origine (upstream) fare il merge, fare il commit e il push **sul proprio repository su github**

* Aprire una branch per ogni gruppo di modifiche uniformi (è più ordinato)
* quando una modifica è pronta per essere sottoposta ai "committers" si apre una pull request sul proprio repository forkato di github. Questo non è altro che un invito ai committers a "tirare dentro" al repository ufficiali le modifiche su cui abbiamo lavorato.

## Errori e Problemi

Contattate la mailing list dell'associazione o lasciate una nota sul repo oppure (meglio) forkate, modificate e aprite una pull request
