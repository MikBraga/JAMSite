---
title: "Architettura del blog"
date: 2021-11-24T23:41:53+01:00
# weight: 1
# aliases: ["/first"]
tags: ["blog"]
author: "Michele Braga"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "Come ho costruito questo blog spendendo veramente poco grazie all'architetura Jamstack e servizi cloud in versione gratuita."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "https://res.cloudinary.com/mikbraga/image/upload/v1637886614/blog/architettura-blog/jamstack-burger_y1bwk6.jpg" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
editPost:
    URL: "https://github.com/<path_to_repo>/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

Ora che ho uno spazio online è giunto il momento di scrivere e pubblicare qualcosa. Per il momento il blog è davvero basico e incompleto – ci sono delle cose che ancora non funzionano – ma con il tempo confido di riuscire a mettere tutti i tasselli al proprio posto. Ho diverse idee in cantiere e argomenti che non hanno trovato spazio altrove, ma ci vorrà del tempo. Nel frattempo ho pensato di raccogliere qualche informazione su come ho realizzato questo progetto.
Il blog sfrutta la tecnologia Jamstack, un insieme di servizi cloud nella loro versione gratuita e Google Domains per la registrazione del dominio. L'idea l'ho presa da un [post](https://riccardo.im/articoli/nuovo-sito-riccardo-palombo/) di Riccardo Palombo e da un suo [video](https://youtu.be/O_IViNjCApU) dedicato al tema.

## Cos'è Jamstack
Jamstack è una architettura progettata per creare siti web veloci, sicuri e scalabili. Alla base di tutto ci sono due concetti chiave: il *pre-rendering* e il *decoupling*.
Cercando di semplificare al massimo, con *pre-rendering* si intende che la pagina web è statica, è già pronta perché creata in anticipo durante il processo di build del sito; non c'è quindi alcun lavoro da parte del server per generare la pagina richiesta. Questo riduce e ottimizza i tempi di caricamento. I siti statici possono essere serviti in modo diretto da una CDN (*Content Delivery Network*), eliminando il costo di una infrastruttura necessaria a generare le pagine web in tempo reale come avviene con siti basati su database in stile Wordpress. Esistono diversi strumenti per generare siti web in questo modo: io ho scelto **Hugo**.
Il termine *decoupling* indica invece la separazione netta tra i diversi servizi che come gli ingredienti di un grande sandwich compongono il sito finale. Questa strategia permette di aggiungere, riumovere, aggiornare o sostituire elementi e funzioni del sito in modo efficiente. Grazie al markup, è possibile utilizzare JavaScript e API di vario tipo per comunicare con piattaforme esterne e integrare servizi all'interno delle pagine web di tipo statico. I siti costruiti con tecnologia Jamstack possono utilizzare questi servizi durante la fase di generazione (build) oppure dal vivo e in modo diretto attraverso JavaScript.

{{<figure src="https://res.cloudinary.com/mikbraga/image/upload/v1637848493/blog/architettura-blog/architettura-blog_pgicbd.jpg" title="Questa è l'architettura Jamstack con cui ho costruito questo blog.">}}

## Piattaforma di sviluppo
Da qualche tempo il mio dispositivo di lavoro principale è un iPad Pro 12.9 (2021) a cui affianco un MacBook Pro 15" del 2018; tuttavia per sviluppare il blog ho scelto di approntare una macchina virtuale Microsoft Windows 10. La decisione è frutto di molteplici fattori: non era possibile installare l'ambiente di sviluppo in iPadOS; non volevo fare esperimenti sul MacBook Pro di produzione; volevo poter anche lavorare dall'iPad Pro e, qualora ne avessi avuto bisogno, volevo che l'ambiente di sviluppo fosse accessibile da remoto.
La scelta finale è stata frutto di un altro esperimento messo in cantiere durante la costruzione della mia postazione di lavoro domestica: un piccolo HomeLab del quale magari vi racconterò qualcosa in futuro.

{{<figure src="https://res.cloudinary.com/mikbraga/image/upload/v1637885229/blog/architettura-blog/homelab-ESXi-1_rulxbh.jpg" title=" ">}}

Per il momento vi dico che utilizzo un sistema Intel NUC – NUC10i7FNH – sul quale ho installato l'hypervisor VMware ESXi. Utilizzo questa piattaforma per diversi tipi di esperimenti e per ospitare la macchina virtuale Windows 10 per lo sviluppo del blog.
Le singole pagine di questo blog sono file markdown. C'è una sezione riservata ai metadata e a contenere alcuni flag e parametri relativi al singolo post, una sezione con il corpo del post e i vari shortcode che uso per inserire elementi come le immagini o rimandare a servizi esterni. Tutti i sorgenti del blog sono poi caricati in una repository GitHub così da essere accessibili al servizio cloud Netlify; questo come spiego più avanti si occupa di generare della fase di pre-rendering e di distribuzione su CDN. Dimenticato, le immagini – tranne alcune – sono fornite on demand attraverso il servizio cloud Cloudinary.

{{<figure src="https://res.cloudinary.com/mikbraga/image/upload/v1637885235/blog/architettura-blog/homelab-ESXi-3_skqhdh.jpg" title=" ">}}

## Microsoft Visual Studio Code
Per lavorare sul codice del blog ho dovuto scegliere un buon editor, uno strumento in grado di aiutarmi con la sintassi dei diversi linguaggi di markup. Ho scelto Microsoft Visual Studio perché mi ci sono trovato subito piuttosto bene e perché è disponibile anche per macOS e  Linux. Qualora decidessi di cambiare ambiente di sviluppo non dovrei adattarmi a un nuovo strumento, ma semplicemente installare Visual Studio Code sulla nuova piattaforma. Per di più Visual Studio Code è completamente gratuito e l'installazione di base è praticamente pronta all'uso (ho fatto giusto un paio di aggiustamenti alle preferenze). Peccato non esista una versione per iPadOS.

{{<figure src="https://res.cloudinary.com/mikbraga/image/upload/v1637888774/blog/architettura-blog/visual-studio-code-ipadpro_lctq7i.jpg" title="Visual Studio Code in macchina virtuale su iPad Pro tramite desktop remoto.">}}

## Editor di testo
Non ho ancora preso una decisione definitiva circa l'editor di testo che intendo utilizzare per scrivere i contenuti del sito; sicuramente non Visual Studio Code: va bene per il codice ma non per la scrittura. Per di più è scartato in partenza visto che non esiste una versione per iPadOS.
I word processor come Microsoft Word li ho abbandonati da tanto tempo in favore di ambienti di scrittura in markdown molto più leggeri e versatili. Dopo aver usato Ulysses per molti anni, poco prima dell'estate sono migrato su IA Writer. È un'app che mi piace, ma sto pensando di provare a usare [Obsidian](https://obsidian.md) anche per la scrittura. Questo post lo sto scrivendo proprio in Obsidian – la cosa mi sta dando parecchie soddisfazioni – perché l'obiettivo finale – probabilmente uno di quelli irraggiungibili – è di concentrare i miei lavori in uno unico contenitore con la possibilità di costruire connessioni tra i diversi elementi al suo interno.
Su questo fronte non ho ancora le idee chiare. Molto dipende dall'interazione delle diverse app, dalle funzioni di gestione del testo e via discorrendo. Uno degli esprimenti che farò presto servirà a capire il livello di interazione tra le app di scrittura in markdown e l'app Working Copy che permette di gestire in modo sorprendente GitHub da iPadOS. Se non fosse ancora chiaro l'obiettivo è di poter scrivere e pubblicare dall'iPad Pro 12.9 per essere completamente svincolato nel tempo e da una postazione fisica.

## Hugo
Come ho già accennato ho scelto [Hugo](https://gohugo.io) come motore per generare le pagine html del blog. L'installazione di Hugo richiede solo qualche minuto: io ho scaricato l'archivio zip dell'ultima versione disponibile e seguito le indicazioni per impostare in modo corretto il path nelle impostazioni di sistema. Una volta installato Hugo basta conoscere pochi comandi da usare nella Power Shell di Windows per creare la prima struttura del sito web o del blog. Fatto questo ho scelto, scaricato e installato un tema – [PaperMod](https://github.com/adityatelange/hugo-PaperMod) – al quale apportare modifiche di stile per dare un carattere personale al blog.
Una volta generato il sito web potete utilizzare Hugo per attivare un servizio di server web locale che genera le pagine html del blog e le serve in tempo reale su una porta localhost. Ogni modifica ai contenuti o al codice del sito diventa visibile subito dopo che è stata salvata. Questo permette di avere un riscontro istantaneo durante lo sviluppo del sito.

## Cloudinary
Per la gestione delle immagini presenti nel blog ho deciso di provare Cloudinary. Si tratta di un servizio cloud – uso solo l'account gratuito – concepito per archiviare e organizzare contenuti multimediali serviti attraverso un link. Questo accorgimento permette di sfruttare le grandi potenzialità di un servizio specializzato nella distribuzione di contenuti multimediali e di alleggerire al tempo stesso l'impronta del blog nella repository di GitHub visto che le immagini, almeno la maggior parte, sono esterne al blog e caricate al volo insieme al resto del contenuto della pagina web.

{{<figure src="https://res.cloudinary.com/mikbraga/image/upload/v1637889080/blog/architettura-blog/cloudinary-ipadpro_rjxupb.jpg">}}

## GitHub
Per mettere online il blog con l'architettura Jamstack ho dovuto creare una repository remota con i sorgenti necessari a generare le pagine html del blog stesso. Ho scelto GitHub, ma è possibile utilizzare altre piattaforme. Questo passaggio è l'anello di congiunzione tra l'ambiente di sviluppo locale e la piattaforma che integra i servizi di generazione e pubblicazione del blog, Netlify.

## Netlify
Netlify è una piattaforma integrata che offre hosting e servizi per siti web i cui file sorgenti sono conservati in strutture Git, generati in versione statica attraverso motori tipo Hugo e quindi serviti al pubblico attraverso una struttura CDN. Netlify ha aggiunto nel tempo funzioni CMS (*Content Management System*) e altre funzioni che esulano da questo progetto. Le funzioni che mi interessano per il blog sono il supporto alla generazione di pagine statiche attraverso un motore Hugo integrato e la distribuzione del blog attraverso una rete CDN.
Una volta stabilito il collegamento tra la repository GitHub e l'account Netlify il gioco è quasi fatto. Netlify e l'architettura Jamstack sono una scelta ideale per operare secondo il modello CI/CD (*Continuos Integration / Continuos Deployment*), ovvero con pagine statiche rigenerate ogni qual volta viene rilevato un cambiamento nella repository GitHub collegata. Ciò significa che una volta aggiornata la repository GitHub con le nuove modifiche (contenuti, aggiornamenti del codice, ecc) tutto il resto avviene in automatico. Gli aggiornamenti possono anche essere di tipo atomico così da ridurre tempi e costi di elaborazione e tempi di distribuzione attraverso la CDN.

L'ultimo tassello in questo puzzle di servizi riguarda la gestione del dominio. Netlify fornisce un indirizzo univoco per ogni sito, ma è poco sfruttabile. È però possibile agganciare l'indirizzo Netlify a un dominio registrato.

## Google Domains
Per il dominio ho scelto Google Domains perché costa poca e perché in questo campo i servizi offerti da Google funzionano bene e sono piuttosto semplici da usare e configurare. Con pochi euro si può avere il dominio senza che il costo salga dopo il primo anno di registrazione (una cosa che mi è successa spesso con altri servizi).
Seguendo le istruzioni di Netlify sono bastati pochi minuti per configurare i parametri DNS e avere reindirizzare le chiamate al dominio registrato per il blog sull'indirizzo generato da Netlify.

## Costi
In questa analisi dei costi ho escluso il mio hardware perché in effetti basterebbe molto meno. Anche un Raspberry Pi 4 con una distrubuzione Linux.


