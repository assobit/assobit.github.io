---
layout: post
title: Bilancio Partecipativo e Data Certa del Bilancio AssoB.it su Blockchain
img: /img/averagePrice.png
bgimg: /img/post-bg.jpg
membro: Gabriele Domenichini, Stefano Capaccioli e Riccardo Casatta
ruolo: Membri fondatori AssoB.it
---

Il 5 marzo 2016 il Consiglio Direttivo ha pubblicato la bozza di relazione e di Rendiconto sulla parte pubblica del sito Assob.it che è costruito su GitHUB, con possibilità per chiunque di proporre miglioramenti il sistema software di controllo di versione distribuito.
<!-- more -->
Il Consiglio Direttivo ha poi approvato il Bilancio il data 14 marzo 2015, potendo tenere conto delle modifiche che gli associati potevano proporre.

Il Bilancio e l'annessa Relazione integrativa dell'Associazione sono stati
"congelati" sulla Blockchain.
Abbiamo usato il servizio "Notarize" di Eternity Wall per incidere in modo indelebile
nel pubblico registro mondiale un'"impronta digitale" del documento.


## I concetti
Qualsiasi documento informatico può produrre un identificativo univoco di sè
stesso tale per cui non esiste altro documento che produce lo stesso
identificativo e se sì effettuano modifiche di qualsiasi tipo al documento
l'identificativo riproducibile non potrà essere più lo stesso di prima. Questo
identificativo viene ad essere quindi la testimonianza che il documento non è stato
alterato nel tempo se ricavando nuovamente l'identificativo questo è
uguale a quello originario.

L'operazione per ricavare l'identificativo è detta hashing e l'identificativo
è detto Hash.

Se si inserisce l'Hash di un documento Nella Blockchain, e ci sono alcuni modi
per farlo, si ha la prova dell'esistenza dell'Hash prima di una determinata data.

Siccome quell'Hash può essere ricavato dallo stesso documento anni dopo con la
stessa operazione se e solo se il documento non è stato alterato, questo fatto
può essere usato come prova inconfutabile:

1. che il documento esisteva prima di una certa data
2. che il contenuto del documento non è stato alterato dal momento in cui il suo
Hash fu ricavato e inciso nella Blockchain.

## Il procedimento utilizzato

Abbiamo preso il Bilancio e la relazione Integrativa e ne abbiamo ricavato il
[file PDF][Bilancio PDF].
Abbiamo utilizzato il servizio "Notarize" di Eternity Wall per "scolpire"
l'hash del documento nella Blockchain.

Per non abusare dello spazio sulla Blockchain Il servizio Notarize utilizza
Un sistema di certificazione multipla, cioè certifica tutti i documenti che ne
fanno richiesta in una certa data in un unica transazione incidendo non l'hash
di un singolo documento sulla blockchain ma l'Hash di un [reticolo di Hash][merkle tree]
ricavato dai documenti da certificare.

La verifica diventa meno immediata ma
ugualmente affidabile in quanto è impossibile modificare uno qualsiasi dei
documenti certificati senza compormettere il reticolo e quindi l'hash radice
che si trova in forma definitiva sulla blockchain.

Perché la verifica dia
esito positivo è necessario che il documento produca lo stesso hash
dell'istante in cui è entrato nel reticolo e che questo hash assieme ad alcuni
altri del reticolo possano produrre l'"Hash radice" che troviamo inciso nella
transazione confermata all'interno della Blockchain.

## Come abbiamo certificato il bilncio con Notarize

Abbiamo mandato una mail al [servizio "Notarize"][notarize] di
[eternitywall.it][eternitywall] e abbiamo ricevuto dal servizio una mail di
risposta con un testo che riportava l'hash calcolato del file PDF che avevamo
inviato al servizio:

    b69e3c95e30d6deca14f513e8c0e46c075be8980aa0ad139321ba8214a4e4b99 : assobit-bilanncio-e-relazione-2015.pdf

e tre file in formato json che contenevano elementi del [Merkle tree][merkle tree].
Il file che ci interessava aveva il
seguente contenuto:


    {
        "status": "ok",
        "txHash": "58ccb4d55fa183a498145deb6db28d1f5044170ec7bc26333b72cd5cbef1166b",
        "merkle": {
            "root": "bc4587f7734e9d575a93e9daaf6d64c6af2ce07171742056674cd24c7a448973",
            "leaves": ["0f11e6a697ceb3ea664ce5ac29ba94d8579570a7389e07ec55c363104f405fd0", "b69e3c95e30d6deca14f513e8c0e46c075be8980aa0ad139321ba8214a4e4b99"]
      }
    }


Con queste componenti possiamo dimostrare a chiunque in futuro che il documento
esisteva prima del 22 di marzo del 2016 e che da allora il contenuto non è cambiato
infatti l'hash del documento non è altro che una delle "leaves" (foglie) del
[merkle tree][merkle tree] il cui Merkle root è stato scritto nella transazione
bitcoin con ID: [58ccb4d55fa183a498145deb6db28d1f5044170ec7bc26333b72cd5cbef1166b][tx]
Sottoforma di OP_RETURN.
Nei dettagli della transazione, analizzando l'output troviamo infatti:

OP_RETURN 455743**bc4587f7734e9d575a93e9daaf6d64c6af2ce07171742056674cd24c7a448973**

I primi sei bytes dell'OP_RETURN sono il "marchio di fabbrica del servizio" cioè
"EWC" in formato esadecimale (455743) mentre la restante parte della stringa è
costituita dal merkle root (bc4587f7734e9d575a93e9daaf6d64c6af2ce07171742056674cd24c7a448973]
 che è stato ottenuto anche dall'hash del nostro documento inviato al sevizio.

 E' impossibile alterare il file del nostro bilancio senza alterarne l'hash e
 senza compromettere l'intero merkle tree la cui root e stata "scolpita" nella
 Blockchain per sempre all'interno di [una transazione][tx] certificata dalla
 Blockchain il 22/3/2016.
Per verificare la consistenza del documento si possono seguire le [istruzioni
riportate sul sito][verification].

## Certificazione dei documenti dell'Associazione.

Il passo successivo consisterà nell'archiviazione del documento anche su
IPFS per garantire allo stesso una sede il più decntralizzata e distribuita
possibile.

Per il prossimo anno abbiamo intenzione di produrre e certificare il Bilancio e
l'annessa relazione in formato XBRL e di permetterne la consultazione attraverso
 l'utilizzo di CSS o di trasformazioni XSLT.





[tx]: https://blockexplorer.com/tx/58ccb4d55fa183a498145deb6db28d1f5044170ec7bc26333b72cd5cbef1166b
[merkle tree]: https://en.wikipedia.org/wiki/Merkle_tree
[eternitywall]: http://eternitywall.it
[notarize]: http://eternitywall.it/notarize
[Bilancio PDF]: https://drive.google.com/a/gdtre.net/folderview?id=0B9RhYggrYYllSE9RcFp6SVJ2VFU&usp=sharing&tid=0B9RhYggrYYllTFZhdjFGd2lIMVU
[verification]: http://blog.eternitywall.it/2016/02/16/how-to-verify-notarization/
