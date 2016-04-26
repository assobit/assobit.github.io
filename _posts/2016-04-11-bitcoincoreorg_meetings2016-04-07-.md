---
layout: post
title: Riassunto meeting IRC del 2016-04-07
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

- Come procedere col wallet bitcoin
- Gestione della RPC/UI per RBF

<!-- more -->

- [Link ai logs di questa settimana](http://bitcoinstats.com/irc/bitcoin-core-dev/logs/2016/04/07#l1460055658.0)
- [Note sull'Incontro di meetbot](http://www.erisian.com.au/meetbot/bitcoin-core-dev/2016/bitcoin-core-dev.2016-04-07-19.00.html)


## Argomenti Principali

- Come procedere col wallet bitcoin
- Gestione della RPC/UI per RBF

## Argomenti brevi

- 0.12.1 Release candidate 1 è stata etichettata (al momento della redazione 0.12.1 RC2 era stata etichettata)
- Aggiornamento per il controllo della violazione della mediana del tempo passato: gmaxwell ha generato un numero di violazioni delle quali nessuna è entrata nel processo di mining. Ci sta ancora lavorando sopra perché ritiene di doverle spedire in modo più forzato.
- 20-22 Maggio ci sarà una convention di Hacking di Bitcoin core in Zurigo (Svizzera) [http://coredev.tech](http://coredev.tech) gli sviluppatori Core che sono interessati dovrebbero riferire a jonasschnelli prima del 15 Aprile.
- Jtimon vorrebbe qualche feedback su un esperimento nella PR [#7829][] che cerca di aiutare la gente nuova a familiarizzare con git, il processo di revisione, etc. e ad ottenere il loro primo merge

## Come procedere col wallet bitcoin

### Antefatto

Nel corso degli anni il wallet di Bitcoin Core ha subito pochi cambiamenti. Molte funzionalità sono richieste e necessarie per la sostenibilità di lungo termine del wallet.
L'obiettivo di lungo periodo è che il wallet diventi indipendente da Core.

### Commenti al meeting

Jonasschnelli propone di estendere la PR [#7830][] che clona l'attuale wallet dentro a un secondo wallet attualmente sperimentale che poi può essere abilitato con l'opzione --enable-lightwallet. In questo modo non ci sono requisiti di compatibilità all'indietro e ci sono meno vincoli di cui tenere conto. Il nuovo wallet rimuove gli [accounts](https://en.bitcoin.it/wiki/Help:Accounts_explained), rimpiazza il BerckleyDB con logDB, aggiunge  [BIP32][] e SPV.

Jonasschnelli fa una stima molto azzardata delle tempistiche: "Il nuovo wallet senza gli account e senza BDB potrebbe essere nella 0.13, l'API stabile nella 0.15, ... non-beta nella 0.16".

Un sacco di unità di test per le funzionalità non-wallet si basano sulla presenza di un wallet. In una più lunga prospettiva questi test dovrebbero essere meno dipendenti dal wallet.

Il nuovo wallet dovrebbe avere anche un'interfaccia completamente nuova.

### conclusioni del meeting

- Features should mostly end up in the new wallet, the old wallet should still receive bugfixes.
- Jonasschnelli will write a proposal to more clearly document the plan of what he'll be working on and how people can best support him.

## Gestione della RPC/UI per RBF

### Antefatto

Il [BIP125][] replace-by-fee (RBF) facoltativa è una nuova funzione che permette ai wallets di dichiarare le transazioni come rimpiazzabili quando sono ancora nella mempool. Questo permette ai wallet di dare una spinta alle commissioni, di aggiungere destinatari, etc. C'è una grande FAQ a questo proposito su [reddit](https://www.reddit.com/r/Bitcoin/comments/3urm8o/optin_rbf_is_misunderstood_ask_questions_about_it/).
Al momento il wallet Bitcoin Core non offre alcuna funzione per avantaggiarsi di tale miglioramento.

### Commenti dell'incontro

Petertodd: "Penso che ciò di cui avete bisogno qui da un punto di vista RPC è pensare in termini di quale indirizzo l'utente voleva pagare e se altre transazioni (confermate) lo hanno già fatto con successo - il che non è proprio il modo in cui il wallet funziona al momento"

Mentre aggiungere outputs sarebbe utile, un primo step consistere nel supporto della spinta con le commissioni.
Petertodd ha scritto un tool per dare una spinta alle commissioni di una transazione [in python](https://github.com/petertodd/replace-by-fee-tools/blob/master/bump-fee.py).

A Gmaxwell piacerebbe vedere un approccio diverso, vale a dire un approccio basato su una "fee adattativa" nel quale si precreano le spinte con scadenze e si mettono in coda. Benché migliore, la gente preferirebbe cominciare con una spinta di comissioni semplice e singola, perchè la versione con le scadenze riutilizzerebbe quel codice. Dovremo essere cauti con le spinte automatiche delle fees perché gli utilizzatori hanno bisogno di esserne consapevoli e aspettarsi tale comportamento.

L'abbassamento del "resto" ha qualche implicazione dal punto di vista della privacy, comunque la privacy diventerà più costosa e incerta se la si cerca in modo accurato. Gmaxwell afferma: "la cosa principale da fare prima di tutto ottenere è una stima accurata, anche se in questo momento il resto è così facilmente identificabile che stai chiudendo la stalla quando i muli sono scappati. :)"
Gmaxwell notes: "the main thing to do is to get the estimate right in the first place, though right now change is so thoroughly identifiable you're closing the barn door after the horse has left. :)"

La spinta alle commissioni potrebbe essere aggiunta al wallet attuale, soluzioni più avanzate come la spinta automatica possono essere realizzate sul nuovo wallet.

### conclusioni del meeting

- Lavorare sulla spinta alle commissioni

## Rilievo umoristico

{% highlight text %}
19:14:37 * gmaxwell bangs gavel  
19:14:43 <sipa> chi è Gavel?  

19:24:40 <petertodd> Sono stato a Zurigo per una settimana ed era così bello che una tazza di caffè costasse 10$

19:31:26 <jonasschnelli> petertodd: bumpfee ... sì. Forse troveremo un nome che sia più flessibile per il futuro?  
19:32:10 <petertodd> jonasschnelli: RispesaAstrattaConChiccoDiFabbricaCambiato?
19:32:51 <sipa> jonasschnelli: dovremo chiamarlo BeeFump
{% endhighlight %}

## Participanti

| IRC nick      | Name/Nym                  |
|---------------|---------------------------|
| MarcoFalke    | [Marco Falke][]           |
| btcdrak       | [BtcDrak][]               |
| gmaxwell      | [Gregory Maxwell][]       |
| jonasschnelli | [Jonas Schnelli][]        |
| petertodd     | [Peter Todd][]            |
| Morcos        | [Alex Morcos][]           |
| sipa          | [Pieter Wuille][]         |
| wumpus        | [Wladimir van der Laan][] |
| kanzure       | [Bryan Bishop][]          |
| sdaftuar      | [Suhas Daftuar][]         |
| jtimon        | [Jorge Timon][]           |
| phantomcircuit| [Patrick Strateman][]     |      
| paveljanik    | [Pavel Janik][]           |

## Esenzione di responsabilità

Questa sintesi è stata redatta senza il contributo di nessuno dei partecipanti nella discussione, ogni errore è attribuibile all'autore del riassunto e non ai partecipanti la discussione.

[#7830]: https://github.com/bitcoin/bitcoin/pull/7830
[#7829]: https://github.com/bitcoin/bitcoin/pull/7829
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
[Gregory Maxwell]: https://github.com/gmaxwell
[Luke Dashjr]: https://github.com/luke-jr
[Peter Todd]: https://github.com/petertodd
[Suhas Daftuar]: https://github.com/sdaftuar
[Pieter Wuille]: https://github.com/sipa
[Eric Lombrozo]: https://github.com/codeshark
[BtcDrak]: https://github.com/btcdrak
[Cory Fields]: https://github.com/theuni
[Alex Morcos]: https://github.com/morcos
[Pavel Janik]: https://github.com/paveljanik
[Matt Corallo]: https://github.com/TheBlueMatt
[Eric Voskuil]: https://github.com/evoskuil
[Jonas Schnelli]: https://github.com/jonasschnelli
[Warren Togami]: https://github.com/wtogami
[Wladimir van der Laan]: https://github.com/laanwj
[Jorge Timon]: https://github.com/jtimon
[Marco Falke]: https://github.com/MarcoFalke
[Tom Harding]: https://github.com/dgenr8
[Patrick Strateman]: https://github.com/pstratem
[Pavel Janik]: https://github.com/paveljanik
[Bryan Bishop]: https://github.com/kanzure
