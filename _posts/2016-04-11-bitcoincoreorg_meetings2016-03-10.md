---
layout: post
title: Riassunto meeting IRC del 2016-03-10
bgimg: /img/post-bg.jpg
membro: Gabriele Domenichini
ruolo: Presidente AssoB.it
---

layout: post
---
Ogni giovedì alle 19:00 UTC i core developers si trovano su IRC
(calale #bitcoin-dev su irc.freenode.net)
per discutere gli argomenti più importanti. Da mesi Stefan Gilis conosciuto come
[g1lius](github.com/G1lius ) scrive riassunti eccezionali. In suo onore ho
deciso di tradurne alcuni per avvicinare la tecnologia bitcoin di frontiera
ad un pubblico competente ma che teme di perdere qualcosa nel tradurre.
Questa settimana:

- Coordinamento di Segregated witness (segwit)
- Politiche su ciò che è considerato standard
- Tipi di indirizzo segwit
- Scaricamento iniziale dei blocchi (IBD) con UTXOs pregenerate firmate
- Porting a ritroso in Bitcoin Core 0.11
- Versione di default del blocco nel versionBits


<!-- more -->


- [Link ai logs di questa settimana](http://bitcoinstats.com/irc/bitcoin-core-dev/logs/2016/03/10#l1457636399.0)
- [Note di meetbot sull'Incontro](http://www.erisian.com.au/meetbot/bitcoin-core-dev/2016/bitcoin-core-dev.2016-03-10-18.59.html)

---

## Coordinamento di Segregated witness (segwit)

Vari sviluppatori stanno lavorando  a un soft fork per introdurre
Segregated witness nella rete principale Bitcoin, con un testing iniziale
portato avanti su una speciale testnet. Segregated witness permette
 che i dati delle firme delle transazioni siano memorizzati al di fuori dei dati utilizzati nel calcolo dell'hash necessario a
produrre l'identificatore della transazione, rimuovendo tutte le forme conosciute di malleabilità della transazione da parte di terze parti
, permettendo ai full node di compilare il set attuale delle UTXO
senza scaricare tutte le firme, e preparando il terreno per le fraud proofs
che possono permettere ai client leggeri (SPV) di aiutare a rinforzare
 le regole di consenso. Il soft fork segwit permette anche ai miners di
sostituire una 1 byte di spazio nel blocco con 4 byte di dati segwit, aumentando
 la capacità di transazione per il wallet che usano segwit.*

Pieter Wuille comincia, " il mio piano era quello di applicare i cambiamenti relativi a segwit di seguito a quelli relativi al BIP9
[versionbits], aggiungere la logica del  [BIP9] a ritroso e continuare dopo un
aggiornamento post-fork, e proseguire con una nuova segnet [segwit testnet]."

La conversazione da qui riguarda sia le politiche di standardizzazione che i nuovi
tipi di indirizzi Bitcoin:

 ### Politiche su ciò che è considerato standard

*[Nota dell'autore: BIP9 usa la parola "active" per significare "enforced per tutti
i blocchi di nuova creazione". I vecchi soft forks usavano "active" con un diverso
significato. Ma per consistenza il testo sotto usa il significato BIP9 in tutti i
casi.]*

Suhas Daftuar domanda una discussione sulle politiche di ciò che è considerato standard, le
politiche opzionali che i nodi seguono per default per decidere quali
 tipi di transazioni distribuire o immettere nel processo di mining. Il soft fork segwit creerà un nuovo tipo di
transazione nello stesso modo in cui il BIP16 creò il tipo di transazione P2SH
, e proprio come in quel caso chiunque avesse speso un
output P2SH prima che il soft fork P2SH si attivasse (e la gente lo fece) avrebbe potuto
avere i bitcoin in quegli output sottratti così ancora si verificherà
che chiunque spenda un output segwit prima che il soft fork segwit
si attivi potrebbe avere i bitcoin in quell'outpiut sottratti se la transazione
che li spende è inviata fuori da un blocco oppure se il blocco che la contiene
 è forkato al di fuori della catena migliore.

"Credevo che avessimo deciso di avvisare gli autori dei wallets di aspettare un pò di tempo dopo
che segwit si attivi prima di usarla", Dice Dauftuar con l'approvazione di
Alex Morcos, descrivendo così una politica che lascia la decisione in capo all'autore
 del wallet e ai suoi utenti. Pieter Wuille descrive alternative che
utilizzerebbero le regole di ciò che è considerato stndard, "una possibilità è quella di non permettere
la logica di distribuzione o di messa in mempool per transazioni segwit fino a dopo 2 [intervalli di riassestamento]
 dopo l'attivazione." Cioè circa un mese dopo l'attivazione."Un'altra
possibilità è di essere prudenti e non abilitare la funzionalità nei
wallets fino a dopo un rilascio post-segwit." Wuille non accoglie nè
respinge queste alternative; le descrive come opzioni.

Gregory Maxwell non commenta sul fatto che una politica su ciò che è considerato stndard debba
essere usata, ma per il wallet di bitcoin core suggerisce, "io
raccomanderei che ci sia uno switch all'utilizzo di segwit come default alla
release successiva dopo che il soft fork si è attivato. Raccomando
l'uso della release [successiva] [perché] in questo caso non è richiesto un comportamento automatico.
Inoltre---è un grosso cambiamento comportamentale usarlo, ad es: dovresti
emettere nuovi tipi di indirizzo in risposta. Avere questo cambiamento
[nell'interfaccia utente] attivato da un comportamento della rete invisibile-all'utente non è
una gran cosa.

**Azioni decise:** La discussione sembra girare attorno al lasciare
la decisione agli sviluppatori dei wallets piuttosto che alla creazione
di una politica di ciò che è considerato standard, ma nessuna decisione concreta è stata raggiuntae e Eric Lombrozo suggerisce di
affrontare altri argomenti, "questo è un qualcosa che può essere
deciso una volta che segwit è stato messo in campo e sta sta aspettando
 l'attivazione".

### Tipi di indirizzo segwit

*Antefatto: L'annuncio iniziale di segwit prevedeva due strade
per i wallet abilitati segwit per richiedere pagamenti, una strada usa la
ben collaudato stile di indirizzo P2SH; l'altra avrebbe procurato un nuovo tipo
che sarebbe stato pienamente ottimizzato per l'utilizzo con segwit. [BIP142][] la proposta per
Quel nuovo stile di indirizzo, ma il supporto per lui è stato abbandonato dal piano per
per l'iniziale messa in campo di segwit a causa di preoccupazioni sia dentro
che fuori dal progetto.*

Wuille comioncia la discussione, "Vorrei che avessimo uno stile di indirizzo per segwit
come parte dello standard." "Morcos approva, "penso che dovremmo farlo,
altrimenti tutti incorporeranno [segwit] dentro al P2SH che è abbastanza
 stupido."

Lombroso spiega perché non è parte dello standard iniziale, "Non abbiamo
spinto [BIP142]  per delle preoccupazioni che riguarda no temibili 'nuovi
indirizzi'. Internamente [nel progetto] alcuni odiano il base58;
esternamente alcuni sono ancora fermi all'idiozia 'segwit
è troppo difficile'. Penso non sia una battaglia che valga la pena di essere combattuta in questo momento".
BtcDrak indica un'approvazione per quest'ultima frase.

Maxwell spiega perché obietta lo stile di indirizzo del BIP142:"[il]
continuato uso del base58 è orribile." Meno seriamente (come indicato da un
emoticon) continua, "rifiuterò di discutere la codifica
degli indirizzi con chiunque non mi abbia letto un indirizzo al telefono."

Matt Corallo aggiunge:"non spetta a noi determinare gli indirizzi
 per segwit -- questo è un qualcosa in cui i **wallets** dovrebbero essere coinvolti --
gente che ha effettivamente qualche competenza UX, che non esiste qui."
(Enfasi nell'originale.) Maxwell approva, "Sì assolutamente ma questo è anche
perché realizzare un nuovo tipo di indirizzo nello stesso momento [in cui rilasciamo segwit]
 non è una buona idea, sarebbe nel mezzo di quel tipo di
collaborazione."

Wuille rimane poco convinto, "la penso al contrario." Maxwell
rimarca che c'è un'altra ragione per posporre la creazione di un nuovo
style di indirizzo per il momento, "[Wuille] solleva perplessità sul fatto che se
se qualcosa non viene fatto prima , saremo bloccati nella sicurezza [degli attuali indirizzi] da 80-bit
per sempre; gli ho ricordato [...] che abbiamo un
miglioramento del checksig in arrivo per ridurre le dimensioni della transazione del 30% che
costituirebbe un bel momento per fare un anche un nuovo tipo di indirizzo." il miglioramento di `OP_CHECKSIG`
a cui allude è il permettere l'uso dell' [algoritmo per la firma digitale Schnorr][shnorr]
, che è già supportato
nella libreria di firma e verifica di Bitcoin Core, [libsecp256k1][].

**Azioni decise:** nessuna. [Nota dell'autore: come Corallo e Maxwell
suggeriscono, sarebbe bene che gli sviluppatori di wallet leggendo questo
cominciassero a discutere che cosa piacerebbe a loro vedere in un nuovo stile di indirizzo e
come (e quando) pensano che dovrebbe essere messo in campo]*

## Scaricamento iniziale dei blocchi (IBD) con UTXOs pregenerate firmate

*Antefatto: ogni full node Bitcoin Core scarica e processa ogni
blocco sulla catena migliore per creare un database dello stato attuale degli
Output di Transazione Non Spesi (UTXOs). Questa è la lista dei bitcoin spendibili
e le condizioni alle quali possono essere spesi (come ad esempio a quale
 chiave pubblica la firma che spende deve corrispondere). al processare tutti quei
blocchi è dovuto il fatto che Bitcoin Core impiega due o più ore per diventare
pienamente pronto la prima volta che lo avvii.  Jonas Schnelli propone di fornire
agli utenti una copia pregenerata del set delle UTXO ad una certa
recente altezza del blocco, con la firma di membri della comunità molto rispettati
, per permettere di evitare di scaricare e processare
tutti i blocchi tranne quelli più recenti.*

Jonas Schnelli comincia,"cosa ne pensate del mio approccio di
[effettuare lo scarico iniziale dei blocchi (IBD)] con un set di UTXO pregenerati
firmati?"

La risposta è totalmente negativa:

- Luke Dashjr: "Suona come una perdita di tempo nel migliore dei casi ad essere franchi.
  preferirei molto vedere [Bitcoin Core partire in] modalità SPV fino a quando l'IBD
  non termina."

- Morcos: "Penso che sia una cattiva idea. Gli sviluppatori Core (o chiunque per quel
  motivo) non dovrebbero certificare lo stato del registro in nessun momento."

- Wladimir van der Laan: "E' rischioso. porta della fiducia nel sistema.
  Di chi ti fideresti per la firma di una cosa del genere?"

- Wuille: "Questo non riduce il servizio dei blocchi; cambia il modello
  di fiducia invece."

**Azioni decise:** Schnelli accetta le risposte con riconoscenza, fornendo una
emoticon positiva e dice,"okay... allora lasciate che non lo metta in campo."

## Porting a ritroso in Bitcoin Core 0.11

"Antefatto: Il documento sul [ciclo di vita del software] di Bitcoin Core dice, "Noi
di mantenere le versioni principali fino al loro 'Fine Manutenzione'. Noi in genere
manteniamo release principale attuale e quella precedente. Quindi se la
versione attuale è la 0.12, allora 0.11 è considerata mantenuta anche lei. Una volta che la 0.13 è
rilasciata, allora la 0.11 sarebbe considerata a 'fine manutenzione'."*

Morcos comincia,"abbiamo bisogno di fare un porting a ritroso del codice di tutti questi soft forks
[BIPs[9][BIP9], [68][BIP68], [112][BIP112], [113][BIP113]] alla 0.11; è
 corretto?"

Maxwell, van der Laan, e Wuille approvano, "Penso che il porting a ritroso alla 0.11
è del tutto necessario; è solo una versione di distanza", dice Var der Laan.

Dashjr vuole vedere il porting a ritroso alla 0.10 se non fosse troppo difficile:
"0.11 è necessario; 0.10 sarebbe ideale; ma affronterò la 0.10 dopo
penso."

Moorcos risponde, "0.10? avrei sperato che voi ragazzi avreste voluto evitare
la 0.11. Sono preoccupato della bontà dei test di questi importanti [soft fork con porting a ritroso]."
BtcDrak sembra condividere, "rinuncerei alla 0.11".

**Azioni decise:** Morcos and BtcDrak discutono su come dividersi il lavoro e
tutti sembrano approvare il porting a ritroso di tutti i BIPs alla serie 0.11 di Bitcoin Core
Wuille conclude,"Penso che possiamo affrontare i [BIPs]
9/68/112/113 presto". Morcos, van der Laan, and BtcDrak tutti concordano con
BtcDrak che dice "68/112/113 sono conclusi per quanto mi riguarda; Morcos vuole aggiungere
ulteriori test RPC, il che è opportuno."


## Versione di default del blocco nel versionBits

*Antefatto :VersionBits [BIP9][] permette di usare il campo della versione dell'header del blocco
come una schiera di bits perché i miners possano segnalare la disponibilità verso fino a 29.
soft forks simultanei. Secondo il codice e la proposta attuale, un
miner che non segnala la disponibilità per nessun soft fork creerà
dei 'blocchi versione 4', cioè blocchi con la stessa versione che venne utilizzata
per attivare e rafforzare il soft fork  [BIP65][] CLTV."

Daftuar dice, "In questo momento [[pull request] #7575][#7575] torneremo ai
blocchi versione 4 dopo che il primo soft fork si attiva, se nessun altro soft
fork è in coda; assumo che non sia voluto?"

Wuille risponde che invece è proprio voluto, "Questo [comportamento] sembra
corretto ai miei occhi; la vecchia versione [4] è utilizzata per indicare 'nessun versionbits'."

Morcos non è sicuro che sia il modo giusto di farlo, "tutti i soft-forks precedenti
richiedevano che i miners aggiornassero. Quello che mi piacerebbe fare è, con questo primo
soft fork, richiediamo che [l'header del blocco] sia maggiore di 4. Poi
possiamo sollevare avvertimenti per qualsiasi cosa non sia [un campo di bit in cui i primi non siano] 001
a meno che non sia maggiore o uguale a 4, che sappiamo che è invalido."

Il bitfield con i primo bits a 001000è proposto come una buona scelta con
Maxwell che dice, "mi piace 001000 nel fatto che incoraggia i tools di visualizzazione
ad esaminare il bitfield invece di mostrare semplicemente un intero."
In effetti i primi tre bits impostati a 001 corrisponderebbero a
Un numero di versione di 536,870,912 nel sistema precedente, che sembrerebbe
 molto strano in un block chain explorer che lo mostrasse in quel modo.

**Azioni decise:** nessuno lo ha detto esplicitamente ma sembra probabile che
la versione di default del bitfield avrà i primi bits impostati a 001000.

## Sull'obbligatorietà di una nuova versione di default del versionbits

Dopo che le precedenti discussioni sembravano aver concluso che l'impostazione
di default dei primi bits del campo versionbits doveva essere 001000, Pieter Wuille vuole
sapere se fare la versione di default uguale a 5 o più grande
dovrebbe essere "[una regola] del consensus oppure no? Io preferisco non introdurre nuove
logiche di consenso, specialmente quando l'unica ragione per questa è un migliore
garanzia per gli avvertimenti."

Morcos risponde, "Suppongo che non debba essere un regola del consenso, ma
penso che sia più chiaro che non ci dovrebbero essere problemi se fosse
una regola del consenso perché questo è il modo in cui [gli aumenti di versione dei precedenti soft- forks]
funzionavano. Se non è una regola del consenso tu non puoi essere **sicuro** che i vecchi
nodi saranno avvertiti che le regole sono cambiate [ma] forse questo
non dovrebbe preoccuparci." (enfasi nell'originale)

Wuille chiede, "siamo preoccupati che [i miners] possano ignorare un meccanismo
di warning?" I soft forks sono diversi dagli hard forks nel fatto che la maggioranza
dell'hash rate può cominciare a rafforzare un soft fork in qualsiasi momento senza
creare una divisione permanente della rete. Sia il versionbits che il metodo precedente
di amministrare i soft forks permettono ai miners di usare il loro hash rate per segnalare
la loro disponibilità al rafforzamento ad altri miners in modo che possano
tutti rafforzarlo nello stesso momento, ma non c'è niente che impedisca
direttamente i miners di accordarsi su un soft fork privatamente. Questo implica
che un meccanismo di avvertimento per il soft fork dipenda dalla collaborazione tra i miners e
cercare di progettarlo per prevenire qualche forma trascuratezza potrebbe essere uno
sforzo inutile.

Morcos sembra propenso a non farne una regola del consenso, tuttavia dice,
"mi sembra solo strano: sento che stiamo passando da un sistema vecchio
ad uno nuovo, e la transizione dovrebbe essere conforme al vecchio
sistema --- ma dal momento che rendiamo 001000 il default, penso che le mie siano solo delle
preoccupazioni teoriche."

**Azioni decise:** nessuna.

## Conclusioni

Il meeting si conclude al tempo prestabilito con la discussione
che prosegue su come gli avvertimenti dovrebbero essere cambiati per
i soft-forks gestiti tramite versionbits.

## Rilievo umoristico

{% highlight text %}
- Wladimir van der Laan: E' rischioso. porta della fiducia nel sistema.
Di chi ti fideresti per la firma di una cosa del genere?"
sipa:   Bob.
wumpus: sì, senza dubbio Bob
Luke-Jr: XD
CodeShark: :p
{% endhighlight %}

## Participanti

| IRC nick      | Name/Nym                  |
|---------------|---------------------------|
| BlueMatt      | [Matt Corallo][]          |
| btcdrak       | [BtcDrak][]               |
| CodeShark     | [Eric Lombrozo][]         |
| evoskuil      | [Eric Voskuil][]          |
| gmaxwell      | [Gregory Maxwell][]       |
| jonasschnelli | [Jonas Schnelli][]        |
| Luke-Jr       | [Luke Dashjr][]           |
| morcos        | [Alex Morcos][]           |
| sdaftuar      | [Suhas Daftuar][]         |
| sipa          | [Pieter Wuille][]         |
| warren        | [Warren Togami][]         |
| wumpus        | [Wladimir van der Laan][] |

## Dichiarazione di non responsabilità

Le citazioni prese dalla discussione conservano il loro uso delle maiuscole, punteggiatura,
e la sillabazione modificata per produrre delle frasi consistenti. Le parole e i frammenti tra parentesi quadre
così come gli antefatti e le esposizioni escplicative,
sono state aggiunte dall'autore di questa sintesi e potrebbero aver
accidentalmente cambiato il significato di alcune frasi; se pensate che qualsiasi
frase sia stata presa fuori contesto, per favore contattateci e l'errore
sarà corretto.

Questa sintesi è stata redatta senza l'ausilio di nessuno dei partecipanti nella
discussione, per cui ogni errore sono sotto la responsabilità dell'autore del riassunto e
non dei partecipanti alla discussione.



[schnorr]: https://en.wikipedia.org/wiki/Schnorr_signature
[libsecp256k1]: https://github.com/bitcoin/secp256k1

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
