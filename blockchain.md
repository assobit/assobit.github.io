# Cos’è la blockchain e perché è la componente fondamentale del Bitcoin
Ia blockchain (in italiano la “catena dei blocchi”) è il registro contabile che contiene tutti i bitcoin esistenti e la storia di questi fin dalla loro creazione. Per capire perchè il registro contabile è l’essenza dell’esistenza del Bitcoin proviamo a immaginare di costruire del denaro digitale dall’inizio.

Uno dei requisiti che vorremmo che il nostro denaro digitale possedesse sarebbe la sua unicità e scarsità ma è noto che qualsiasi oggetto digitale ha la proprietà di poter essere duplicato innumerevoli volte ad un costo trascurabile e questo permetterebbe a chiunque fosse in possesso di un pò del nostro “denaro” di duplicare le sue sostanze a piacere e pagare con “la stessa moneta” una pluralità di persone.
Questo piccolo ostacolo sul nostro cammino di gloria, noto da molti anni, è conosciuto come il *problema della doppia spesa* e consiste nel fatto che posso pagare Tizio, inviandogli una copia dell’oggetto digitale in pagamento e pagare Caio con un’altra copia dello stesso oggetto per altri beni o servizi senza che nessuno dei due ne sia necessariamente al corrente o possa fare alcunchè.

Per questa ragione, da tempo, tutto il denaro digitale esistente (compreso quello che usiamo tutti i giorni)  necessita di uno o più registri che certificano che un determinato ammontare di denaro digitale esista una solo posto e possa essere creato o aumentato solo con determinate regole stabilite dai manutentori di questi. Questi registri garantiscono che gli utenti del denaro digitale non possano effettuare scritture doppie e, per esempio, rattribuirsi ammontari da loro già spesi.
Grande fiducia viene data dagli utenti ai manutentori di questi sistemi e di questi registri i quali sono infatti normalmente organismi pesantemente regolati dai governi.
Pensiamo al nostro denaro nel conto corrente bancario che rappresenta oggi e, sempre di più in futuro, la maggior parte del denaro che abbiamo a disposizione. Questo denaro esiste solo in quanto scritto nel registro contabile digitale mantenuto dal nostro istituto di credito. Quando mandiamo denaro con un bonifico, ciò che avviene in grande sostanza è un confronto tra due registri contabili e una riconciliazione per cui ad un calo del saldo dell’uno a seguito del trasferimento corrisponde un aumento del saldo dell’altro per l’arrivo del denaro.

La Blockchain è il registro contabile unico del mondo Bitcoin, è dove tutti i Bitcoin vengono creati e dove è riportata la storia di ciascuno di essi e la sua posizione attuale. Non esistono riconciliazioni nel registro unico perchè questo ha una sola versione di tutte le transazioni che avvengono nel “mondo Bitcoin”.

## Bhè ma allora che bisogno c’era di un altro registro contabile per il denaro digitale?
La Blockchain è il primo registro contabile che non richiede fiducia verso il manutentore dello stesso perchè la correttezza dell’operato e delle scritture è verificabile e in grande misura verificato dagli utenti del sistema.
Dalla sua genesi il Bitcoin è nato come una comunità di utenti con l’unico scopo comune della correttezza del funzionamento contabile del sistema e tale comunità è nata e cresciuta senza il patrocinio, la garanzia e la tutela di nessun governo, o di nessuna impresa pubblica o privata.
Il sistema è stato concepito per la partecipazione di chiunque segua le rigide regole di correttezza contabile che sono costantemente verificate da tutti gli altri utenti.  

La Blockchain risponde unicamente a due regole fondamentali nel sua attività:
* La correttezza delle scritture contabili, che recita: in ogni transazione l’ammontare di bitcoin sbloccato deve essere uguale o superiore all’ammontare di bitcoin che si vincola con le nuove condizioni
* Esiste una sola sequenza delle transazioni ed un unica storia di tutti i bitcoin
Esaminiamo questi concetti più a fondo

## Ma se è così importante, come si fa se si rompe o si perde?
La Blockchain è in realtà duplicata in migliaia di copie e chiunque può ed è caldamente invitato ad averne una all’interno del proprio PC per garantire la solidità e la correttezza del sistema. Le copie sono tenute sincronizzate attraverso aggiunte successive di “pagine” o meglio blocchi di nuove transazioni che vengono certificati dal sistema e distribuiti per essere aggiunte alla propria copia della blockchain. Ogni nuovo blocco è logicamente legato al precedente dalla sequenza del numero del blocco e da un meccanismo matematico che garantisce l’integrità del blocco e di tutti i precedenti a cui questo si attacca.
Questa struttura a blocchi successivi di dati legati tra di loro ha suggerito il nome di catena dei blocchi (Blockchain in inglese) con cui il registro del Bitcoin è conosciuto

## Se nessuno comanda e controlla il sistema cosa impedisce che mi arrivino diversi blocchi di transazioni con lo stesso numero e magari con transazioni diverse dentro?
Il meccanismo che permette a tutti i computer che tengono una copia della blockchain di trovare un accordo su quale è l’esatto contenuto di questa per tutti è il cuore della genialità e dell’originalità della blockchain ed è un processo imperfetto ad approssimazione successiva.

Esistono nella rete Bitcoin computers con il compito di costruire i blocchi con le transazioni che in ogni istante vengono trasmesse nella rete. per costruire il blocco devono raccogliere un gruppo arbitrario di transazioni e cercare di risolvere una specie di quiz la cui difficoltà è regolata in modo che si possa trovare una soluzione ogni dieci minuti.
Se uno di questi computer trova una soluzione ampiamente prima degli altri trasmette a tutti i computer il blocco di transazioni  e la soluzione del quiz e il nuovo blocco viene attaccato alla propria copia della blockchain senza ambiguità.
Se due dei computer designati alla scrittura dei blocchi trovano e propagano in maniera quasi simultanea due pagine simili e una soluzione corretta del quiz, può capitare che parte della rete attacchi una delle due pagine al proprio registro e l’altra parte della rete l’altra pagina semplicemente perché ha visto prima quella. In questi casi si formano due versioni del registro contabile ma il software che custodisce la vostra copia del registro è scritto per preferire sempre la copia del registro con il numero di pagine più alto (con la più alta quantità di quiz risolti). Se il blocco successivo verrà trovato da un computer che aveva sposato la versione alternativa del registro rispetto a quella da voi in buona fede adottata, quando il nuovo blocco verrà distribuito, il vostro PC recepirà immediatamente la blockchain più lunga e il sistema si sarà automaticamente riordinato.

## Cos’é una transazione Bitcoin?
La blockchain contiene l’elenco di tutte le transazioni Bitcoin suddivise in blocchi. E’ importante capire in cosa consiste una transazione.
Ogni ammontare di bitcoin è vincolato sul registro da una serie di condizioni informatiche e di codici che è necessario fornire al sistema per sbloccare quel particolare ammontare di bitcoin cioè per spenderli. Queste condizioni possono richiedere dati che solo un utente ha (il “possessore dei bitcoin in questione) oppure condizioni oggettive come la data e un’ora su cui il sistema concorda essere quella attuale.
Siamo abituati alla metafora del mandare a Tizio o a Caio i soldi in tutto il mondo ma la metafora corretta sarebbe quella di poter aprire lo scrigno in cui i bitcoin sono contenuti e poter scrivere sulla Blockchain in quali scatole (sotto quali condizioni informatiche) questi ammontari devono essere nuovamente rinchiusi. Ogni scatola ha le sue regole di sblocco e, se scelgo di vincolare i bitcoin che ho sbloccato in uno scrigno in cui le condizioni informatiche di sblocco sono in mano solo a Tizio ottengo l’effetto di avergli consegnato la disponbilità di quell’ammontare in modo irreversibile. E’ come se effettivamente glieli avessi “mandati”. Il paradosso è che a fronte della possibilità di mandare il denaro dappertutto, questo in realtà non si muoverà mai dall’unico posto dove può esistere: la Blockchain.

La Blockchain esiste sostanzialmente per certificare che un determinato ammontare di bitcoin possa essere sbloccato e che lo stesso ammontare di Bitcoin abbia delle destinazioni precise e non si possa “creare moneta” all’interno della *transazione*.

L’unicità e l’autorità del registro fanno sì che non ci sia ambiguità nell’ammontare dei bitcoin in circolazione e nella loro allocazione a determinate regole di sblocco.
La transazione è un documento informatico diviso in due in cui:
* nella prima parte si forniscono le istruzioni al sistema di quali scrigni aprire e si forniscono le condizioni per aprirli
* nella seconda parte in cui si individuano le nuove regole che occorreranno per sbloccare l’ammontare intero in una successiva transazione oppure diversi insiemi di regole per sbloccare frazioni dell’ammontare originario.

## Cosa impedisce che vengano emesse due transazioni valide che sbloccano lo stesso importo ma in cui si forniscano delle condizioni differenti di successivo vincolo dei fondi?

Niente in realtà impedisce di comunicare al sistema di voler spendere dei propri ammontari bitcoin in modi tra loro diversi. Le transazioni verranno comunicate al sistema che le riterrà valide tutte e due ma verrà scritta sulla Blockchain una sola di queste transazioni che diverrà immediatamente l’unica valida. Dopo che la transazione è stata scritta sulla Blockchain quell’importo non risulterà più vincolato dalle condizioni originarie e qualsiasi tentativo di svincolare lo stesso importo con le condizioni precedenti verrà rifiutato dalla rete (non è possibile spendere due volte lo stesso denaro).

La Blockchain è il registro notarile insindacabile che certifica ciò che è vero per la rete in termine di sequenza e temporalità delle operazioni. Questo fornisce un sottoprodotto del sistema Bitcoin che sembra andare al di là della semplice gestione di una nuova valuta virtuale e di cui parleremo qui sotto.
Riassumiamo le caratteristiche fondamentali e distintive della Blockchain e le immense potenzialità che ne derivano e su cui istituzioni e governi di tutto il modo guardano con interesse.

* La Blockchain è il solo registro di tutto ciò che è valido per il mondo Bitcoin
La sua esistenza e il suo funzionamento è governato unicamente dalle leggi matematiche e da un comportamento scritto nel software, accettato e certificato da tutti gli utenti
* Ciò che è scritto sulla Blockchain non è reversibile e la sequenza temporale delle sue scritture non è modificabile senza il pregiudizio di tutto il sistema
* Le condizioni di sblocco e successivo vincolo degli ammontari sono programmabili via software e la gamma di condizioni utilizzabili nelle transazioni si amplia mano a mano che il sistema viene migliorato.
* Ogni singolo Bitcoin o frazione di esso è rintracciabile sulla Blockchain assieme a tutte le condizioni di svincolo a cui è stato sottoposto in passato e a quelle che lo vincolano adesso

Queste caratteristiche hanno permesso di immaginare molti possibili sviluppi di questa tecnologia vediamole nel dettaglio:

## La Blockchain è il solo registro di tutto ciò che è valido per il mondo Bitcoin
I mercati finanziari di tutto il mondo hanno attualmente a che fare con pesanti processi di riconciliazione tra diversi registri contabili.
Il NASDAQ e tutti i mercati finanziari statunitensi di azioni hanno bisogno di tre giorni lavorativi (tempo noto noto come T+3) per certificare il “passaggio di mano” di un qualsiasi titolo in una compravendita. Altri tipi di mercati come i Syndacated Loans necessitano settimane. Questo sostanzialmente perchè i vari registri contabili della banca del compratore, del venditore, del broker, della piattaforma del mercato devono essere riconciliati per riflettere il nuovo stato del sistema. Queste riguardano sia il trasferimento del titolo nella nuova custodia titoli, sia il passaggio del denaro che costituisce il pagamento.
La tecnologia Blockchain ha suggerito al mondo finanziario la possibilità di spostare tutte le transazioni finanziarie su un unico registro per rendere condiviso il nuovo stato del sistema istantaneamente. Addirittura si ritiene possibile lo scambio della proprietà del titolo e del denaro in un unica transazione detta di tipo “atomico” in quanto composta di multiple modifiche dello stato del sistema considerate come una unica.
Il Nasdaq ha già effettuato con successo la prima transazione su una Blockchain sperimentale.

## La sua esistenza e il suo funzionamento è governato unicamente dalle leggi matematiche e da un comportamento scritto nel software, accettato e certificato da tutti gli utenti
La natura indipendente e decentralizzata della Blockchain la rende suscettibile di un utilizzo internazionale che superi barriere linguistiche, geografiche e regolatorie. Nonostante i rischi di una simile apertura, la tentazione di convergenza verso l’utilizzo di un qualcosa pensato in modo universale dalla sua fondazione, stimola anche i governi più curiosi e dinamici preoccupati di diventare i fanalini di coda di una nuova ondata di globalizzazione.

## Ciò che è scritto sulla Blockchain non è reversibile e la sequenza temporale delle sue scritture non è modificabile senza il pregiudizio di tutto il sistema
L’esistenza di un “registro notarile” la cui sequenza delle scritture non è alterabile senza compromettere un’economia da miliardi di dollari, ha stimolato l’idea di poter “scolpire” sulla Blockchain all’interno delle transazioni la prova dell’esistenza di un determinato oggetto digitale ad una certa data. L’esempio più banale può essere dato dalla possibilità di scolpire un proprio brano musicale o un proprio brevetto sulla Blockchain ad una certa data. Tale esistenza non potrebbe essere in futuro contestata da nessuna perizia tecnica di nessun tribunale al mondo.
Pur non esistendo ancora nessuna evidenza giuridica dell’opponibilità di una prova del genere, è ormai universalmente riconosciuto che la Blockchain potrebbe diventare un immenso registro notarile universale per la “data certa” di qualsiasi oggetto digitale.

## Le condizioni di sblocco e successivo vincolo degli ammontari sono programmabili via software e la gamma di condizioni utilizzabili nelle transazioni si amplia mano a mano che il sistema viene migliorato.
Se qualsiasi ammontare bitcoin può essere vincolato con condizioni a scelta, è possibile trasformare contratti assicurativi, di distribuzione dei proventi legati alla vendita di beni sottoposti a diritti (come i libri o la musica), in condizioni elaborabili in modo non presidiato dal software. Condizioni all’avverarsi delle quali sbloccano dei fondi e li distribuiscono in maniera automatica e non sindacabile per andare a rivincolarli in modo totalmente predeterminato.
E’ possibile già oggi fare sì che un determinato progetto possa essere finanziato sulla Blockchain alla sola condizione che la raccolta “crowdfunding” raggiunga un determinato importo entro un determinato tempo. Se ciò non avviene, l’importo viene restituito ai finanziatori, altrimenti viene allocato al progetto con condizioni spendibili da parte del promotore dello stesso.
Questo e molti altri tipi di contratto sono già oggi automatizzabili sulla Blockchain e sono detti Smart Contracts in quanto dotati di una loro intelligenza intrinseca che ne permette l’autonoma esecuzione al verificarsi di condizioni predeterminate e accettate.
Ogni singolo Bitcoin o frazione di esso è rintracciabile sulla Blockchain assieme a tutte le condizioni di svincolo a cui è stato sottoposto in passato e a quelle che lo vincolano adesso
Questa caratteristica rende possibili alcuni metodi per associare ad un frammento di bitcoin presente sulla Blockchain un altro oggetto identificabile  informaticamente come un certificato azionario, un lotto di terreno oppure perchè no un importo in una valuta che un qualche ente può impegnarsi a rimborsare a fronte della presentazione di quella particolare frazione di Bitcoin dal valore intrinseco trascurabile.

Il fatto che questi oggetti siano “agganciati” a bitcoin che possono entrare in transazioni ma che sono in qualche modo “colorati” o identificati come associati a un titolo di proprietà apre possibilità molto ampie nella gestione della proprietà e del trasferimento della stessa di beni che vanno al di là del solo bitcoin.
Abbiamo già citato gli esperimenti del NASDAQ che hanno cominciato ad associare a frazioni di valuta digitale certificati azionari per poterne gestire la proprietà ed il trasferimento della stessa.

Il governo dell’Honduras ha avviato un progetto per associare a parti trascurabili di bitcoin i lotti del terreno dello stato per garantire verso i cittadini e verso il mondo la correttezza delle proprie scritture catastali. In futuro chi possiede le condizioni di sblocco di frazioni di bitcoin associate ad un qualsiasi titolo di proprietà un ente abbia deciso di associare a tale frazione, possiederà anche la proprietà e la disponibilità del bene di fronte a tale ente.

## Vabbè ho capito. Perchè non vedo applicazioni sulla Blockchain oggi?

Le possibilità aperte dalla tecnologia Blockchain sono molto promettenti ma avendo a che fare con valori e certificazioni con conseguenze legali, i programmi vanno testati a fondo e senza dubbio passerà un pò di tempo prima di vedere messi in pratica questi concetti.
Nel frattempo il mondo Bitcoin si sta confrontando con due sfide principali riguardanti la Blockchain e il sistema nel suo complesso:
* La decentralizzazione
* La scalabilità
La natura decentralizzata della Blockchain in cui tutti e nessuno è responsabile del mantenimento del ledger è un assoluta novità nel campo della scienza sociale.
Le economie discala stanno favorendo l’aggregazione di grandi e piccoli nuclei di potere che minacciano l’”anarchia” del progetto originario ma è compito di tutti mantenere integro il disegno iniziale di una rete “di tutti e per tutti” perchè così vuole la stragrande maggioranza degli utenti e questo è quello che differenzia il Bitcoin da tutto ciò che esiste oggi.

La scalabilità è la capacità di assorbire un numero di transazioni più alte di quello attuale.
La rete VISA può supportare oggi punte di 43000 transazioni al secondo mentre la rete Bitcoin solo 4. Il divario sembra incolmabile e sopratutto ci sono ragioni strutturali che impediscono al Bitcoin di scalare oltre un certo limite. La ragione principale sono i tempi del Consensus che tutta la rete dei computer partecipante deve raggiungere sull’attuale stato del ledger ufficiale.
I processi del Consensus sono lenti in quasi tutte le discipline e come caso pratico si pensi che la conta dei voti della più grande democrazia oggi esistente, l’India, richiede settimane.
Il paragone sembra discutibile ma rende l’idea sul fatto che mettere d’accordo 5’500 computer in giro per il mondo richiede tempo, specie se questi vogliono controllare di persona la correttezza delle scritture. Paragonare questo con un sistema fatto da calcolatori che svolgono calcoli paralleli senza doversi preoccupare dell’affidabilità di ciò che gli viene trasmesso (come nel caso della VISA) è quanto meno improprio.
La soluzione che si sta percorrendo consiste nel concentrare in una transazione Bitcoin molte transazioni che avvengono fuori dalla Blockchain e che usano questa solo come traghetto tra un sistema fuori dal registro ad un altro oppure come giudice di ultima istanza per le diatribe gravi o per periodici riallineamenti.
Qualunque sia il futuro della Blockchain sarà interessante seguirne lo sviluppo anche per le nuove idee che dallo sviluppo stesso stanno germinando.
