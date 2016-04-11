---
layout: post
title: Riassunto meeting IRC del 2016-03-17
bgimg: /img/post-bg.jpg
membro: Gabriele Domenichini
ruolo: Presidente AssoB.it
---
Ogni giovedì alle 19:00 UTC i core developers si trovano su IRC
(calale #bitcoin-dev su irc.freenode.net)
per discutere gli argomenti più importanti. Da mesi Stefan Gilis conosciuto come
[g1lius](github.com/G1lius ) scrive riassunti eccezionali. In suo onore ho
deciso di tradurne alcuni per avvicinare la tecnologia bitcoin di frontiera
ad un pubblico competente ma che teme di perdere qualcosa nel tradurre.
Questa settimana:

- Programmazione del primo soft fork BIP9 per i BIPs 68, 112, 113
- Caratteristiche della 0.12.1 oltre al BIP9
- Stato di Segregated Witness

<!-- more -->

- [Link ai logs di questa settimana](http://bitcoinstats.com/irc/bitcoin-core-dev/logs/2016/03/17#l1458241237.0)
- [Note sull'Incontro di meetbot](http://www.erisian.com.au/meetbot/bitcoin-core-dev/2016/bitcoin-core-dev.2016-03-17-19.00.html)


## Argomenti Principali

- Programmazione del primo soft fork BIP9 per i BIPs 68, 112, 113
- Caratteristiche della 0.12.1 oltre al BIP9
- Stato di Segregated Witness

## Programmazione del primo soft fork BIP9 per i BIPs 68, 112, 113

### Antefatto

VersionBits [BIP9][] permette di usare il campo versione dell'header del blocco  come una schiera di bits perché i miners possano segnalare la disponibilità verso fino a 29.
soft forks simultaneamente. Secondo il codice attuale proposto, un miner che non ha intenzione di segnalare la disponibilità verso nessun soft fork tra quelli proposti, creerà un 'blocchi versione 4' cioè blocchi con la stessa versione di quelli utilizzati per attivare e poi rafforzare il  soft fork CLTV [BIP65][].

### Commenti dell'incontro

Tutti sembrano contenti della PR  [#7575][](incorporata poco dopo l'incontro).
Nel momento in cui si decide la data di partenza e il numero del bit, dovrebbe essere annunciata la cosa sulla mailing list in modo che altre implementazioni possano implementarla a loro volta.
Btcdrak e Morcos avranno i backports per 0.12 & 0.11 pronti.
Il testo per il BIP [BIP9][] è aggiornato, sarebbe una buona idea aggiornare anche i BIPs [68][BIP68], [112][BIP112] e [113][BIP113] con le informazioni sul soft fork.


### conclusioni del meeting

- Merge [#7575][]
- Review [#7648][]
- Data per l'inizio della messa in campo basata sul [BIP9][] è l' 1 maggio, il numero del bit è 0.
- btcdrak aggiornerà la sezione relativa alla messa in campo dei testi BIP [68][BIP68], [112][BIP112] e [113][BIP113] con le nuove informazioni sul soft fork.

## Caratteristiche della 0.12.1 al di là del BIP9

### Commenti dell'incontro

Jonasschnelli sta lavorando sulle funzionalità di avviso della GUI (PR [#7579][]), la gente è propensa a rimandare la cosa alla 0.12.2 per concentrarsi sul soft fork nella 12.1Morcos vorrebbe aggiungere le PRs  [#7715][]("Rimedio nel calcolo dei saldi e dei coins disponibili") e [#7707][] ("supporto UI per le transazioni abbandonate") sua e di jonasschnelli che gestiscono le transazioni abbandonate per riuscire a spendere nuovamente gli outputs che hanno avuto commissioni troppo basse.

Wumpus fa notare che gli piace evitare di portare molte funzionalità durante un softfork. Al momento il sistema di allarme per controllare se sei su una catena sbagliata ha un sacco di falsi positivi. C'è un senso di urgenza nel o ripararlo o disabilitarlo perchè la situazione attuale porterà la gente a ignorare gli avvertimenti.
Un rimedio è stato apportato da dgenr8 (PR [#7568][])

### conclusioni del meeting

-  Esame [#7568][] ("Correzione all'attivazione del messaggio di avviso sulla Bad-cahin") & [#7715][]
- [#7707][] RPC-only (commit 42e945d79fd54ab11ad48978910b42d10c1c7cf8), Che è una linea di codice.

## Stato di segregated witness

### Antefatto

Vari sviluppatori stanno lavorando  a un soft fork per introdurre Segregated witness nella rete principale Bitcoin, con un testing iniziale portato avanti su una speciale testnet. Segregated witness permette che i dati delle firme delle transazioni siano memorizzati al di fuori dei dati utilizzati nel calcolo dell'hash necessario a produrre l'identificatore della transazione, rimuovendo tutte le forme conosciute di malleabilità della transazione da parte di terze parti, permettendo ai full node di compilare il set attuale delle UTXO senza scaricare tutte le firme, e preparando il terreno per le fraud proofs che possono permettere ai client leggeri (SPV) di aiutare a rinforzare le regole di consenso. Il soft fork segwit permette anche ai miners di sostituire una 1byte di spazio nel blocco con 4 byte di dati segwit, aumentando la capacità di transazione per il wallet che usano segwit.

### Commenti dell'incontro

Sipa sta lavorando al problema dell'aggiornamento post-fork nell'attuale codice segwit, dopo questo farà una nuova segnet che includa la logica bit di versione.
Il suo obiettivo è averla prima del rilascio della 0.13.


## Rilievo umoristico

{% highlight text %}
sipa: Sono contento che il BIP9 sembra completato
btcdrak:    sipa: festa a casa tua. Noi portiamo le birre.
jonasschnelli:    btcdrak finalmente si rivelerà al party.
btcdrak:    haha
sipa: jonasschnelli: ecco perché porti un mixer di bibite

{% endhighlight %}

## Participanti

| IRC nick      | Name/Nym                  |
|---------------|---------------------------|
| jtimon        | [Jorge Timon][]           |
| btcdrak       | [BtcDrak][]               |
| gmaxwell      | [Gregory Maxwell][]       |
| jonasschnelli | [Jonas Schnelli][]        |
| morcos        | [Alex Morcos][]           |
| sdaftuar      | [Suhas Daftuar][]         |
| sipa          | [Pieter Wuille][]         |
| wumpus        | [Wladimir van der Laan][] |

## Dichiarazione di non responsabilità

Questa sintesi è stata redatta senza il contributo di nessuno dei partecipanti nella discussione, ogni errore è attribuibile all'autore del riassunto e non ai partecipanti la discussione.

[#7575]: https://github.com/bitcoin/bitcoin/pull/7575
[#7648]: https://github.com/bitcoin/bitcoin/pull/7648
[#7579]: https://github.com/bitcoin/bitcoin/pull/7579
[#7715]: https://github.com/bitcoin/bitcoin/pull/7715
[#7707]: https://github.com/bitcoin/bitcoin/pull/7707
[#7568]: https://github.com/bitcoin/bitcoin/pull/7568

[BIP1]: https://github.com/bitcoin/bips/blob/master/bip-0001.mediawiki
[BIP9]: https://github.com/bitcoin/bips/blob/master/bip-0009.mediawiki
[BIP11]: https://github.com/bitcoin/bips/blob/master/bip-0011.mediawiki
[BIP13]: https://github.com/bitcoin/bips/blob/master/bip-0013.mediawiki
[BIP14]: https://github.com/bitcoin/bips/blob/master/bip-0014.mediawiki
[BIP16]: https://github.com/bitcoin/bips/blob/master/bip-0016.mediawiki
[BIP21]: https://github.com/bitcoin/bips/blob/master/bip-0021.mediawiki
[BIP22]: https://github.com/bitcoin/bips/blob/master/bip-0022.mediawiki
[BIP23]: https://github.com/bitcoin/bips/blob/master/bip-0023.mediawiki
[BIP30]: https://github.com/bitcoin/bips/blob/master/bip-0030.mediawiki
[BIP31]: https://github.com/bitcoin/bips/blob/master/bip-0031.mediawiki
[BIP34]: https://github.com/bitcoin/bips/blob/master/bip-0034.mediawiki
[BIP35]: https://github.com/bitcoin/bips/blob/master/bip-0035.mediawiki
[BIP37]: https://github.com/bitcoin/bips/blob/master/bip-0037.mediawiki
[BIP42]: https://github.com/bitcoin/bips/blob/master/bip-0042.mediawiki
[BIP61]: https://github.com/bitcoin/bips/blob/master/bip-0061.mediawiki
[BIP65]: https://github.com/bitcoin/bips/blob/master/bip-0065.mediawiki
[BIP66]: https://github.com/bitcoin/bips/blob/master/bip-0066.mediawiki
[BIP68]: https://github.com/bitcoin/bips/blob/master/bip-0068.mediawiki
[BIP70]: https://github.com/bitcoin/bips/blob/master/bip-0070.mediawiki
[BIP71]: https://github.com/bitcoin/bips/blob/master/bip-0071.mediawiki
[BIP72]: https://github.com/bitcoin/bips/blob/master/bip-0072.mediawiki
[BIP111]: https://github.com/bitcoin/bips/blob/master/bip-0111.mediawiki
[BIP112]: https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki
[BIP113]: https://github.com/bitcoin/bips/blob/master/bip-0113.mediawiki
[BIP125]: https://github.com/bitcoin/bips/blob/master/bip-0125.mediawiki
[BIP130]: https://github.com/bitcoin/bips/blob/master/bip-0130.mediawiki
[BIP133]: https://github.com/bitcoin/bips/blob/master/bip-0133.mediawiki
[BIP142]: https://github.com/bitcoin/bips/blob/master/bip-0142.mediawiki

[@bitcoincoreorg]: https://twitter.com/bitcoincoreorg
[#bitcoin-core-dev]: https://webchat.freenode.net?channels=%23bitcoin-core-dev&uio=MTY9dHJ1ZSYxMT0yMTU87
[issues]: https://github.com/bitcoin/bitcoin/issues
[pulls]: https://github.com/bitcoin/bitcoin/pulls
[bitcoin-discuss]: http://lists.linuxfoundation.org/mailman/listinfo/bitcoin-discuss
[bitcoin-dev]: http://lists.linuxfoundation.org/mailman/listinfo/bitcoin-dev
[bitcoin-core-dev]: http://lists.linuxfoundation.org/mailman/listinfo/bitcoin-core-dev
[Slack]: https://bitcoincore.slack.com/
[slack-invite]: https://slack.bitcoincore.org/
[software life cycle]: /en/lifecycle

[laanwj-key]: https://github.com/bitcoin/bitcoin/blob/master/contrib/gitian-downloader/laanwj-key.pgp
[jonasschnelli-key]: https://github.com/bitcoin/bitcoin/blob/master/contrib/gitian-downloader/jonasschnelli-key.pgp
[sipa-key]: https://github.com/bitcoin/bitcoin/blob/master/contrib/gitian-downloader/sipa-key.pgp

[recent-contributors]: https://github.com/bitcoin/bitcoin/graphs/contributors?from=2015-01-01&to=2016-03-21&type=c

[website-issues]: https://github.com/bitcoin-core/bitcoincore.org/issues
