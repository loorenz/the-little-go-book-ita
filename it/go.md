# Su Questo Libro

## Licenza

"The Little Go Book" è rilasciato sotto la licenza Attribution-NonCommercial-ShareAlike 4.0 International. Non dovresti aver pagato per leggere questo libro.

Sei libero di copiare, distribuire, modificare e mostrare il libro. Tuttavia, ti chiedo solo di attribuire sempre questo libro a me, Karl Seguin, e non usarlo per scopi commerciali.

Puoi vedere il testo completo della licenza qui:

<https://creativecommons.org/licenses/by-nc-sa/4.0/>

## Ultima Versione

Puoi trovare l'ultima versione di questo libro qui:
<https://github.com/karlseguin/the-little-go-book>

# Introduzione

Ho sempre avuto un rapporto di odio-amore con l'idea di imparare un nuovo linguaggio. Da una parte, infatti, i linguaggi sono fondamentali per il nostro lavoro: le più piccole modifiche possono avere un impatto notevolissimo. Esatto, quel momento *aha* che ha un effetto particolare su di noi e va a ridefinire le aspettative che abbiamo nei confronti di quel linguaggio. Dall'altra parte, però, il design di un linguaggio è qualcosa di "incrementale". Impari nuove parole chiave, tipi, per poi passare al coding style e via, verso le librerie, community, paradigmi. Andando a "pesare" tutto questo l'idea potrebbe non far impazzire.

Beh, la verità è che *dobbiamo* andare avanti. A voler essere più precisi, dovremmo sempre essere tutto sommato contenti di imparare qualcosa di nuovo: d'altronde, i linguaggi sono il fondamento di quello che facciamo. Piano piano, un passo alla volta, possiamo fare nostre tutte quelle nozioni che nel tempo hanno un impatto sempre più ampio: leggibilità, performance, testabilità, gestione delle dipendenze, documentazione, profiling e così via.

Certo una domanda resta: **perché proprio Go?**. Per quanto mi riguarda, le ragioni fondamentali sono due. In primis, perché è un linguaggio relativamente semplice con una altrettanto relativamente semplice standard library. La "sostanza" alla base di Go è proprio questa: semplificare la complessità vista in molti linguaggi negli ultimi anni. Anche l'altra ragione non è da sottovalutare però: Go sarà un ottimo strumento per completare l'arsenale di un qualsiasi sviluppatore.

Go è stato costruito come linguaggio di sistema (parliamo di sistemi operativi, driver per device e così via) e di conseguenza può essere facilmente "orientato" a tutti gli sviluppatori C e C++. Tuttavia, stando a quello che il team di Go dice, la fetta più grande dell'utenza di Go non è quella dei system developer. Al contrario: sono gli application developer! Come mai? Sembra che tanti, tra coloro che costruiscono siti, servizi web, applicazioni desktop e non solo, si manifesti una necessità sempre più crescente di un certo numero di sistemi che facciano da "cuscinetto" tra il software di alto livello (applicazione) e quello di basso livello (sistema).

Può essere un sistema di messaging, caching, analisi dei dati intensiva, tool da linea di comando. I sistemi crescono in termini di complessità e di conseguenza aumenta la ricerca di software che "aiuti" l'infrastruttura. Certo, si tratta sempre di cose che possiamo implementare con Python o Ruby ma avere a disposizione un sistema di tipi più rigido e maggiori performance certo non è da sottovalutare. Detto questo, nulla ti vieta di usare Go per costruire siti web. Ci sono molti che lo fanno ma è anche vero che l'espressività di altri linguaggi può essere più adatta allo scopo.

Ad ogni modo, ci sono anche altre aree in cui Go eccelle. Ad esempio, non esiste il concetto di dipendenza nel momento in cui viene eseguito un programma scritto in Go. Non bisogna preoccuparsi di quale JVM è installata, tantomeno quale versione. Anche per questo motivo Go sta diventando sempre più popolare tra tutti quelli che ne fanno uso per costruire tool da linea di comando.

Insomma, Go è indubbiamente un ottimo uso del tuo tempo. Anche perché non dovrai spendere chissà tempo per impararlo ad usare: in poco tempo infatti potrai già implementare un sacco di applicazioni utili e renderti conto da solo del suo potenziale.

## Una Nota dall'Autore

Prima di scrivere questo libro ho esitato molto. Per varie ragioni. Innanzitutto, la documentazione ufficiale di Go, in particolare [Effective Go](https://golang.org/doc/effective_go.html), è un'ottima risorsa.

Inoltre, devo ammettere di essermi trovato un po' "a disagio" nello scrivere un libro su un linguaggio. Quando ho scritto "The Little MongoDB Book" ho dato per scontate alcune delle nozioni fondamentali da conoscere. Stessa cosa per "The Little Redis Book".

Qui il discorso è diverso: sapevo che non avrei potuto fare le stesse assunzioni. Insomma, come fare per capire quanto tempo spendere per parlare delle interfacce in Go sapendo che per alcuni l'argomento è nuovo, ma per altri basta un *Go ha le interfacce*?

Arrivo alla mia richiesta: se qualche passaggio dovesse sembrarti più oscuro del previsto, fammelo presente! Vedilo un po' come il prezzo di questo libro, dai.

# I Primi Passi

Se vuoi iniziare a "giocare" un po' con Go potresti dare un'occhiata al [Go Playground](https://play.golang.org/), tool che ti permette di eseguire codice online senza dover installare nulla sulla tua macchina. Tra l'altro, il Go Playground viene spesso usato quando si chiede aiuto nei forum come [questo qui](https://groups.google.com/forum/#!forum/golang-nuts), o in posti come StackOverflow.

Installare Go, comunque, è piuttosto semplice. Puoi farlo partendo dai sorgenti ovviamente, anche se è molto più comodo usare i binari pre-compilati. Basta dare uno sguardo alla [pagina dei download](https://golang.org/dl/) sul sito ufficiale e trovare quello per la tua piattaforma.

Ora, se escludiamo alcuni esempi basilari, Go è stato progettato per "lavorare" nel momento in cui il tuo codice si trova in quello che viene definito "workspace". In poche parole, parliamo di una cartella al cui interno trovi altre cartelle `bin`, `pkg` ed `src`. Occhio, perché potresti essere tentato di impostare un progetto seguendo il tuo gusto personale. Non farlo: non è questo il caso.

Tendenzialmente, io metto tutto il mio codice in `~/code`. Di conseguenza, `~/code/blog` conterrà il mio blog. Per Go, il mio workspace è `~/code/go` ed il mio blog in Go si troverà in `~/code/go/src/blog`.

Per capirci: crea una cartella `go` con una sottocartella `src` al suo interno dove pensi metterai il tuo codice.

Vediamo ora come installare Go su OSX / Linux e Windows.

## OSX / Linux

Scarica il file `tar.gz` per la tua piattaforma. Per OSX probabilmente ti intereserà `go#.#.#.darwin-amd64-osx10.8.tar.gz`, dove `#.#.#` è l'ultima versione di Go.

Estrai tutto in `/usr/local` tramite `tar -C /usr/local -xzf go#.#.#.darwin-amd64-osx10.8.tar.gz`.

Sistema quindi due variabili di sistema:

  1. `GOPATH` che punterà al tuo workspace. Nel mio caso, ad esempio, è `$HOME/code/go`.
  2. Aggiungi quindi il path dei binari di Go alla variabile `PATH`;

Puoi fare tutto questo da shell, con due `echo`.

    echo 'export GOPATH=$HOME/code/go' >> $HOME/.profile
    echo 'export PATH=$PATH:/usr/local/go/bin' >> $HOME/.profile

Per "attivare" queste variabili riavvia la shell, o esegui `source $HOME/.profile`.

Esegui il comando `go version`. Se vedi dell'output simile a `go version go1.3.3 darwin/amd64`, è fatta!

## Windows

Scarica l'ultima versione in formato zip. Se sei su un sistema x64 vorrai usare `go#.#.#.windows-amd64.zip`, dove `#.#.#` è l'ultima versione di Go.

Estrai il tutto in una cartella a tua scelta. `c:\Go` è una buona scelta.

Anche in questo caso dovrai lavorare su due variabili di sistema.

  1. `GOPATH` che punterà al tuo workspace. Nel mio caso, ad esempio, è `c:\users\goku\work\go`.
  2. Aggiungi `c:\Go\bin` alla variabile `PATH`.

Puoi gestire le variabili d'ambiente tramite `Variabili d'Ambiente` nel tab `Avanzate` del pannello di controllo `Sistema`. In alcune versioni di Windows questa nomenclatura potrebbe cambiare leggermente.

Una volta fatto tutto, apri un prompt e digita `go version`. Se è andato tutto bene dovresti vedere un output simile a `go version go1.3.3 windows/amd64`.

# Capitolo 1 - Le Basi

Go è un linguaggio compilato e basato su tipizzazione statica, che presenta una sintassi che ricorda il C. Gestisce autonomamente, inoltre, la garbage collection. Bello tutto, ma che significa?

## Compilazione

La compilazione è quel processo di "traduzione" del codice sorgente in un linguaggio di basso livello (come assembly, nel caso di Go), o magari altri linguaggi intermedi (come avviene per Java e C#).

A volte può rivelarsi poco piacevole lavorare con un linguaggio compilato: la procedura può essere lenta e iterare velocemente significa spendere comunque minuti oppure ore ad aspettare la compilazione. Per fortuna, la velocità di compilazione è uno degli obiettivi più importanti del design di Go.

C'è da dire che i programmi scritti in linguaggi poi compilati tendono ad essere eseguiti più velocemente e non hanno bisogno di dipendenze (questa cosa vale almeno per C, C++, Go).

## Static Typing

Per "static typing" o "tipizzazione statica" si intende un concetto molto semplice: ogni variabile deve avere un tipo ben specifico (int, string, bool e così via). Questa specifica avviene in due modi: dichiarando esplicitamente il tipo della variabile o, a volte, lasciando questo compito al compilatore. Vedremo a breve alcuni esempi.

C'è molto da dire sullo static typing: sono convinto però che sia ancora più comprensibile guardando il codice. Se sei abituato a lavorare con linguaggi dalla tipizzazione dinamica, all'inizio troverai il tutto un po' poco agevole. Non hai torto ma, come ho già detto, ci sono dei vantaggi. Specialmente quando il linguaggio è compilato.

## Sintassi C-Like

Dire che un linguaggio ha una sintassi C-Like (in italiano "simile al C") significa che se hai già lavorato con C, C++, Java, JavaScript o C#, molto probabilmente troverai Go familiare. Almeno per quanto riguarda la sintassi: `&&` è effettivamente un AND booleano, `==` viene invece usato per le uguaglianze, le `{` parentesi `}` vengono usate per creare degli scope e così via.

I linguaggi C-Like inoltre presentano, in genere, il punto e virgola a fine linea e le parentesi per delimitare le condizioni. In questo caso, Go non ne fa uso, anche se le parentesi possono essere comunque usate per gestire le precedenze nei controlli. Ecco un esempio:

```go
if name == "Leto" {
  print("the spice must flow")
}
```

Questo è un caso semplice, le parentesi non servono. Qui, invece...

```go
if (name == "Goku" && power > 9000) || (name == "gohan" && power < 4000)  {
  print("super Saiyan")
}
```

... le parentesi sono effettivamente molto utili perché ci permettono di gestire l'ordine dei controlli.

Sia chiaro: Go è molto più vicino al C che al Java. Non solo in termini di sintassi ma proprio in termini di scopo.

## Garbage Collection

Alcune variabili, una volta create, hanno un ciclo di vita facilmente individuabile. Una variabile locale in una funzione, ad esempio, cessa di esistere nel momento in cui la funzione è stata eseguita. In altri casi, tuttavia, questo ciclo non è così ovvio... almeno per il compilatore. Pensiamo ad una variabile il cui valore viene ritornato da una funzione, o ad una reference ad un'altra variabile. In situazioni del genere può essere indubbiamente più difficile definire a priori un ciclo di vita. Senza la garbage collection, il compito di "eliminare" la variabile ad un certo punto spetta allo sviluppatore.

Come? In C, ad esempio, devi letteralmente chiamare una funzione `free(str);` su quella variabile.

I linguaggi con garbage collection però, come Ruby, Python, Javascript, C# ed ovviamente Go) sono capaci di tenere traccia di tutto e liberare la memoria appena possibile. Certo, la garbage collection aggiunge overhead ai nostri software. Tuttavia, il "prezzo" da pagare è l'assenza di tanti bug noiosi e magari difficili da trovare.

## Il Nostro Primo Programma Go

Ok, basta parlare, è arrivato il momento di eseguire scrivere, compilare ed eseguire il nostro primo programma! Apriamo il nostro editor di testo preferito e riportiamo questo codice:

```go
package main

func main() {
  println("it's over 9000!")
}
```

Salviamo il file come `main.go`. Per ora salvalo dove vuoi: al momento non c'è bisogno di lavorare dentro il workspace Go.

Apri quindi una shell/prompt nella directory in cui hai salvato il file. Nel mio caso, `cd ~/code`.

Esegui quindi il programma con:

```
go run main.go
```

Se tutto è andato a dovere, dovresti leggere *it's over 9000!*.

Ok, adesso fermi tutti: che significa tutto questo? Abbiamo compilato il nostro codice oppure no? Facciamo un po' di chiarezza. Innanzitutto, `go run` è un comando molto utile che innanzitutto compila il nostro codice *e* poi lo esegue. Usa una cartella temporanea per effettuare tutte le operazioni, dopodiché esegue il nostro codice ed infine pulisce tutto.

Aggiungendo l'opzione `--work` al comando run puoi vedere quale cartella verrà usata.

```
go run --work main.go
```

Per compilare esplicitamente il codice, invece, dovrai usare `go build`:

```
go build main.go
```

L'esecuzione di questo comando genererà un eseguibile `main`, pronto ad essere usato. Non scordare, se sei su Linux/OSX, di aggiungere il prefisso `./` all'eseguibile (`./main`).

L'idea alla base di tutto quello che vedi è semplice: in fase di sviluppo, usare al volo `go run` è molto utile. Al momento del deploy, però, dovrai usare `go build` e poi eseguire il compilato.

### Main

Immagino che il codice del nostro primo programma sia abbastanza comprensibile: tutto quello che abbiamo fatto è stato creare una funzione e stampare una stringa con la funzione `printLn`. Come puoi facilmente immaginare, `go run` ha eseguito esattamente quella funzione perché, in Go, il punto di ingresso di un'applicazione è la funzione `main` in un package `main`. Semplice!

Parleremo più avanti dei package: per ora, scriveremo il nostro codice sempre in un package `main` per concentrarci sulle basi del linguaggio.

Se vuoi fare una prova, sentiti libero di modificare il codice e cambiare il nome del package. L'istruzione `go run` ti restituirà un errore. D'altronde, stai rimuovendo il punto di ingresso della tua applicazione!

## Import

Come avviene per molti linguaggi, anche Go ha svariate funzioni già pronte: `printLn` è una di queste. C'è da dire, però, che non andremo molto lontano senza usare la standard library di Go e, a volte, librerie di terze parti.

In Go, la keyword `import` viene usata per dichiarare quali package verranno usati dal codice presente in un certo file.

Facciamo qualche modifica al nostro programma.

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  if len(os.Args) != 2 {
    os.Exit(1)
  }
  fmt.Println("It's over", os.Args[1])
}
```

Proviamolo ad eseguire, stavolta così:

```
go run main.go 9000
```

Adesso, il nostro programma usa due package della standard library: `fmt` ed `os`. Abbiamo introdotto anche un'altra funzione built-in, `len`, che si occupa di ritornare, in questo caso, il numero di elementi in un array.

Avrai inoltre notato la notazione `fmt.Println` per chiamare la funzione `Println`: è differente rispetto a ciò che puoi vedere in altri linguaggi. Ne parleremo, tuttavia, in un secondo momento.

Una cosa molto interessante da sapere è che Go è molto rigido per quello che riguarda l'import di package. Se un package non viene usato ma ne è specificato l'import, la compilazione non andrà mai a buon fine. Non ci credi? Prova ad eseguire questo codice:

```go
package main

import (
  "fmt"
  "os"
)

func main() {
}
```

Otterrai due errori riguardanti `fmt` ed `os`, appunto. Noioso? Si, vero. Nel tempo però imparerai ad apprezzarlo: importare qualcosa che non ti serve infatti aumenterebbe il tempo di compilazione.

Detto questo, apro una piccola parentesi per farti notare una cosa davvero interessante. Come puoi vedere tu stesso, la documentazione della standard library fa il suo lavoro egregiamente. Guarda qui, ad esempio: <https://golang.org/pkg/fmt/#Println>. Si tratta della reference relativa alla funzione `Println` che abbiamo usato.

Ecco la cosa interessante: sei in viaggio, non hai accesso ad internet ma hai bisogno della documentazione. Come fare? Semplice:

```
godoc -http=:6060
```

Questo comando metterà su al volo un server contenente la stessa identica documentazione. Non dovrai fare altro che puntare il tuo browser verso `http://localhost:6060`.

## Le Variabili

Sarebbe davvero molto simpatico, per me, poter guardare al volo le variabili e cavarmela con un *ok, puoi dichiarare ed assegnare un valore ad una variabile con un semplice x = 4*. Spiacente, in Go le cose non vanno così... sono leggermente più complesse, ma non troppo.

Vediamo subito qualche sempio.

Partiamo dal modo più esplicito (e verboso) di gestire la dichiarazione di una variabile e la sua assegnazione.

```go
package main

import (
  "fmt"
)

func main() {
  var power int
  power = 9000
  fmt.Printf("It's over %d\n", power)
}
```

Qui dichiariamo una variabile `power` di tipo `int`. Di default, Go assegna alle variabili `int` il valore `0`. Subito dopo diamo un valore a questa variabile: `9000`. Possiamo rendere la cosa più sintetica... così:

```go
var power int = 9000
```

Inizia ad essere più scorrevole, vero? Bene. Abbiamo comunque a disposizione un altro operatore: il `:=`.

```go
power := 9000
```

Cos'ha di speciale? Può "indovinare" il tipo, partendo dal valore che gli viene assegnato. Può essere anche usato con una funzione alla sua destra.

```go
func main() {
  power := getPower()
}

func getPower() int {
  return 9001
}
```

Ricorda: l'operatore `:=` viene usato per dichiarare *e* assegnare un valore ad una variabile. Se lo usi due volte nello stesso scope otterrai un errore. Come in questo caso:

```go
func main() {
  power := 9000
  fmt.Printf("It's over %d\n", power)

  // COMPILER ERROR:
  // no new variables on left side of :=
  power := 9001
  fmt.Printf("It's also over %d\n", power)
}
```

Il compilatore restituirà un errore  del tipo *no new variables on left side of :=*. Tutto quello che bisogna fare è ricordarsi che, nello stesso scope, dopo aver usato la prima volta `:=`, dovremo poi usare sempre il classico `=`.

Se sei attento, avrai fatto caso che il messaggio di errore riguarda più variabili (recita infatti "variables"). Questo succede perché in Go puoi effettuare questa operazione di assegnamento per più variabili in una volta sola.

```go
func main() {
  name, power := "Goku", 9000
  fmt.Printf("%s's power is over %d\n", name, power)
}
```

Finchè almeno una delle variabili è "nuova", puoi usare `:=` senza problemi. Questo esempio è perfettamente valido:

```go
func main() {
  power := 1000
  fmt.Printf("default power is %d\n", power)

  name, power := "Goku", 9000
  fmt.Printf("%s's power is over %d\n", name, power)
}
```

Un po' come succede per gli import, inoltre, Go non ti permette di compilare il tuo programma se hai variabili non usate. Questo esempio:

```go
func main() {
  name, power := "Goku", 1000
  fmt.Printf("default power is %d\n", power)
}
```

non verrà compilato perché `name` è stata dichiarata ma non usata. Anche in questo caso, all'inizio sarà un po' frustrante... ma nel lungo periodo ti aiuterà a tenere il codice pulito e leggibile.

C'è tanto da sapere riguardo le variabili ed il loro assegnamento. Per ora, ricordiamoci queste semplici regole:

* se usiamo `var NAME TYPE` le dichiariamo e assegnamo loro il valore di default;
* se usiamo `NAME := VALUE` le dichiariamo e assegnamo loro il valore VALUE. Il tipo verrà "capito" automaticamente;

## Le Funzioni

Ok, questo è un ottimo momento per dire che le funzioni possono ritornare più di un valore. Diamo uno sguardo a questi esempi. Sono tre funzioni: una non ha valore di ritorno, la seconda uno solo, la terza ne ha ben due.

```go
func log(message string) {
}

func add(a int, b int) int {
}

func power(name string) (int, bool) {
}
```

Ecco un esempio d'uso della terza:

```go
value, exists := power("goku")
if exists == false {
  // handle this error case
}
```

A volte, potresti aver bisogno soltanto di uno dei valori ritornati. In questi casi, assegna l'altro valore a `_` per ignorarlo.

```go
_, exists := power("goku")
if exists == false {
  // qui gestiamo un eventuale errore...
}
```

Si tratta, più che altro, di una convenzione. Il `_`, il blank identifier, permette di essere usato tutte le volte che vuoi, senza dover preoccuparsi del tipo del valore ritornato.

Infine, una piccola "scorciatoia". Se in una funzione i parametri sono tutti dello stesso tipo, puoi anche specificare questo tipo una volta sola. Così:

```go
func add(a, b int) int {

}
```

Adesso tutto questo, forse, ti dice poco. In futuro però troverai molto utile avere funzioni che ritornano più valori. Troverai altrettanto utile poter scartare un certo valore ritornato con `_`. Per ora, comunque, è tutto.

## Prima di Proseguire

Molto probabilmente, in questo momento stai pensando di vedere tanti piccoli "pezzettini" di questo linguaggio. Pezzettini che non ancora compongono un'immagine ben definita. Nessun problema: è normale, soprattutto adesso.

Se vieni da un linguaggio dinamico, alcune cose ti sembreranno noise. Controintuitive. Se vieni da linguaggi a tipizzazione statica, invece, dovresti trovarti a tuo agio. Un po' alla volta, però, sono sicuro apprezzerai in ogni caso la pulizia verso la quale sarai portato.

# Capitolo 2 - Strutture

Go non è un linguaggio orientato agli oggetti come C++, Java, Ruby o C#. Non ha oggetti, niente ereditarietà, nessun concetto associabile alla programmazione orientata agli oggetti che conosciamo, come polimorfismo od overloading.

In Go esistono le strutture, alle quali possiamo associare dei metodi. C'è anche una semplice (ma efficace) forma di composizione di queste strutture. Il risultato? Codice più semplice, anche se a volte sentirai la mancanza di ciò che viene offerto dallo sviluppo orientato agli oggetti. (Varrebbe la pena ricordare che nell'antica battaglia del *composition over inheritance* Go è uno dei primi linguaggi che ha preso una posizione ben precisa).

Insomma, Go è abbastanza lontano dall'OOP. Tuttavia, ci sono alcune similitudini da notare nella definizione di una struttura e di una classe. Facciamo subito un esempio: ecco una struttura. La chiameremo `Sayian`.

```go
type Saiyan struct {
  Name string
  Power int
}
```

Non è poi così illeggibile, vero?

## Dichiarazioni ed Inizializzazioni

Nel capitolo precedente, parlando delle variabili, abbiamo dato uno sguardo ai principali tipi già presenti in Go, come interi e stringhe. Ora che la nostra "conversazione" a riguardo si sta ampliando, vale la pena spiegare il concetto di puntatore (pointer) nelle prossime righe.

Dunque: abbiamo definito la nostra struttura. Diamo adesso un valore ad una variabile di questo tipo.

```go
goku := Saiyan{
  Name: "Goku",
  Power: 9000,
}
```

*Nota:* la virgola `,` nella struttura è necessaria anche dopo l'ultimo elemento della struttura. Senza, infatti, il compilatore restituirà un errore.

Non devi necessariamente valorizzare tutti i campi della struttura. Ad esempio, un'istruzione del genere è perfettamente valida:

```go
goku := Saiyan{}

// oppure...

goku := Saiyan{Name: "Goku"}
goku.Power = 9000
```

Proprio come accade per le variabili, infatti, anche i campi di una struttura hanno dei valori di default.

Se ti è comodo, puoi evitare di specificare il nome del campo da valorizzare e usare come "ordine" lo stesso in cui hai dichiarato i vari campi nella struttura. Ecco un esempio:

```go
goku := Saiyan{"Goku", 9000}

// che è uguale a...

goku := Saiyan{
  Name: "Goku",
  Power: 9000,
}
```

Insomma, come vedi ci sono molti modi di fare assegnare alla variabile `goku` uno specifico valore. Detto questo, veniamo ai puntatori.

Non sempre, appunto, avrai bisogno di accedere al valore di una variabile. In alcuni casi avrai bisogno di un puntatore a quella variabile, a quel valore. Puoi vedere un puntatore come un indirizzo specifico di memoria. Il "posto" dove trovare quel valore. Un po' come "essere a casa" e "avere l'indirizzo di casa", per capirci.

La domanda sorge spontanea: perché mai dovremmo aver bisogno di un puntatore?

Semplice: in Go, normalmente, gli argomenti di una funzione vengono passati come copie. Che significa? Facciamo una prova per capire meglio. Guarda questo codice:

```go
func main() {
  goku := Saiyan{"Goku", 9000}
  Super(goku)
  fmt.Println(goku.Power)
}

func Super(s Saiyan) {
  s.Power += 10000
}
```

Sai dirmi quale sarà il suo output? 19000? Sbagliato. La funzione `Super`, certo, aggiunge 10000 al valore di `Power`... ma l'argomento passato alla funzione è comunque una copia del "goku originale" che si trova in `main`. Nello scope di `main`, quindi, `Power` rimane 9000.

Per far funzionare il tutto avremo bisogno di usare un puntatore. Così:

```go
func main() {
  goku := &Saiyan{"Goku", 9000}
  Super(goku)
  fmt.Println(goku.Power)
}

func Super(s *Saiyan) {
  s.Power += 10000
}
```

Guarda bene: abbiamo fatto due piccole ma importantissime modifiche. Innanzitutto, abbiamo usato l'operatore `&` che serve ad ottenere l'indirizzo della variabile con cui viene usato. Viene infatti chiamato l'operatore "address of". Come conseguenza, quindi, abbiamo modificato il tipo di parametro che `Super` si aspetta. Non più un `Saiyan` dunque, bensì un `*Saiyan` (o *puntatore a Saiyan*). C'è quindi una relazione tra `Saiyan` e `*Saiyan`, anche se rimangono due tipi separati e distinti.

Proviamo ad eseguire ora il programma: il risultato stavolta sarà 19000!

Giusto come conferma ulteriore, modifica come segue il codice ed esegui nuovamente il programma.

```go
func main() {
  goku := &Saiyan{"Goku", 9000}
  Super(goku)
  fmt.Println(goku.Power)
}

func Super(s *Saiyan) {
  s = &Saiyan{"Gohan", 1000}
}
```

Stavolta il risultato sarà 9000. Perché? Guarda bene: hai aggiunto `&` in `Super`. Stai lavorando di nuovo con una copia.

Un'altra cosa su cui vale la pena riflettere è il "peso": copiare un puntatore è molto meglio rispetto al copiare una struttura complessa e passarla come parametro... non trovi? Su una macchina a 64-bit, un puntatore è grande ben 64 bit. Se ci trovassimo ad usare strutture molto grandi, creare delle copie sarebbe decisamente problematico. Il vero punto di forza consiste proprio nella condivisione di questo valore.

Se alcune cose non ti sono chiarissime, rileggi più di una volta questa parte. In ogni caso non temere: continueremo ad affrontare la questione puntatore/valore più avanti.

## Associare Metodi alle Strutture

Possiamo "associare" un metodo ad una struttura così:

```go
type Saiyan struct {
  Name string
  Power int
}

func (s *Saiyan) Super() {
  s.Power += 10000
}
```

Con il codice qui sopra stiamo affermando che `*Saiyan` è il ricevente (receiver) del metodo `Super`. Che possiamo chiamare così:

```go
goku := &Saiyan{"Goku", 9001}
goku.Super()
fmt.Println(goku.Power) // will print 19001
```

## Costruttori

Le strutture *non* hanno costruttori. Puoi però creare delle funzioni che ritornano un'istanza del tipo di cui hai bisogno (un po' come avviene con le factory, per capirci).

```go
func NewSaiyan(name string, power int) *Saiyan {
  return &Saiyan{
    Name: name,
    Power: power,
  }
}
```

Sia chiaro: non è necessario far ritornare un puntatore ad una funzione del genere. Anche questa funzione qui di seguito, infatti, è perfettamente valida.

```go
func NewSaiyan(name string, power int) Saiyan {
  return Saiyan{
    Name: name,
    Power: power,
  }
}
```

## Funzione "New"

Nonostante la mancanza di un costruttore, Go ha una funzione `new` che permette di allocare la memoria necessaria per un certo tipo di variabile. Il risultato di `new(X)` sarà lo stesso di `&X{}`.

```go
goku := new(Saiyan)

// è uguale a...

goku := &Saiyan{}
```

Sta a te decidere quale usare, tuttavia sappi che molti  trovano più comoda la seconda nel momento in cui ci sono anche dei campi da inizializzare, visto che il risultato è più leggibile.

```go
goku := new(Saiyan)
goku.name = "goku"
goku.power = 9001

// contro...

goku := &Saiyan {
  name: "goku",
  power: 9000,
}
```

Ad ogni modo, a prescindere da quale sia l'approccio scelto, ricorda che scegliere il "factory" pattern visto poco sopra è molto utile: puoi separare il resto del tuo codice da tutti i dettagli relativi all'allocazione.

## Campi di una Struttura

Nell'esempio visto finora, `Saiyan` ha due campi: `Name` e `Power`, rispettivamente di tipo `string` ed `int`. I campi di una struttura possono essere di qualsiasi tipo (incluse altre strutture).

Ecco un esempio perfettamente valido di `Saiyan` (con una piccola aggiunta):

```go
type Saiyan struct {
  Name string
  Power int
  Father *Saiyan
}
```

... che potremmo inizializzare così:

```go
gohan := &Saiyan{
  Name: "Gohan",
  Power: 1000,
  Father: &Saiyan {
    Name: "Goku",
    Power: 9001,
    Father: nil,
  },
}
```

## Composizione

Come già menzionato prima, Go supporta la composizione, che consiste nell'includere una struttura dentro l'altra. In alcuni linguaggi si parla di *mixin* o *trait*. Ecco un esempio in un altro linguaggio (Java):

```java
public class Person {
  private String name;

  public String getName() {
    return this.name;
  }
}

public class Saiyan {
  // Saiyan is said to have a person
  private Person person;

  // we forward the call to person
  public String getName() {
    return this.person.getName();
  }
  ...
}
```

Ecco una dichiarazione simile, stavolta in Go.

```go
type Person struct {
  Name string
}

func (p *Person) Introduce() {
  fmt.Printf("Hi, I'm %s\n", p.Name)
}

type Saiyan struct {
  *Person
  Power int
}

// and to use it:
goku := &Saiyan{
  Person: &Person{"Goku"},
  Power: 9001,
}
goku.Introduce()
```

La struttura `Saiyan` conta al suo interno un campo di tipo `*Person`. Non avendo dato esplicitamente un nome al campo di tipo `*Person`, possiamo accedere ai suoi membri direttamente dal tipo "composto".

Il compilatore ha gestito in modo autonomo la cosa. Guarda qui:

```go
goku := &Saiyan{
  Person: &Person{"Goku"},
}
fmt.Println(goku.Name)
fmt.Println(goku.Person.Name)
```

Le ultime due istruzioni sono entrambe valide, e stamperanno lo stesso valore.

### Overloading

Nonostante l'overaloading non sia qualcosa di "specifico" delle strutture, vale la pena comunque darci un'occhiata. Di base, Go *non* supporta l'overloading. Di conseguenza, vedrai (e scriverai) spesso funzioni come `Load`, `LoadById`, `LoadByName` e così via.

Ora, dato che la composizione implicita è un (comodo) trucco del compilatore, possiamo anche "sovrascrivere" una funzione per un tipo composto. Abbinando il codice qui sotto a quello visto nell'esempio precedente...

```go
func (s *Saiyan) Introduce() {
  fmt.Printf("Hi, I'm %s. Ya!\n", s.Name)
}
```

... avremo due diverse versioni di `Introduce`. Quella della struttura `Person` sarà disponibile comunque tramite `s.Person.Introduce()`.

## Puntatori Vs. Valori

Quando scriverai il codice dei tuoi programmi in Go, spesso ti ritroverai a chiederti: *devo usare un puntatore oppure direttamente un valore?* Beh, un valore non è una cattiva scelta in casi come:

* assegnamento di una variabile in locale;
* campo in una struttura;
* valore di ritorno di una funzione;
* parametro di una funzione;
* ricevente di un metodo;

Per il resto... nel dubbio, usa un puntatore.

Ad ogni modo, ricorda che passare un valore (e non un puntatore) ad una funzione è un ottimo modo per preservare l'immutabilità. Può essere il comportamento di cui hai bisogno, altre volte invece no. Tienilo a mente.

Considera poi, comunque, i costi di creazione di una copia di una tale struttura. In altri casi però potresti avere strutture semplici, come questa:

```go
type Point struct {
  X int
  Y int
}
```

In casi come questi, il costo di copia della struttura è rilevante quasi quanto l'accesso diretto, senza troppo overhead.

Insomma: valuta caso per caso. La pratica rende perfetti.

## Prima di Proseguire

Questo capitolo ti ha dato una prima infarinatura sulle strutture, come crearne un'istanza e come rendere queste strutture "ricevitori" di una funzione. Abbiamo inoltre aggiunto i puntatori al nostro bagaglio.

Nei prossimi capitoli aggiungeremo altra carne al fuoco: nuove strutture e approfondimenti sui meccanismi di questo linguaggio.

# Chapter 3 - Maps, Arrays and Slices

So far we've seen a number of simple types and structures. It's now time to look at arrays, slices and maps.

## Arrays

If you come from Python, Ruby, Perl, JavaScript or PHP (and more), you're probably used to programming with *dynamic arrays*. These are arrays that resize themselves as data is added to them. In Go, like many other languages, arrays are fixed. Declaring an array requires that we specify the size, and once the size is specified, it cannot grow:

```go
var scores [10]int
scores[0] = 339
```

The above array can hold up to 10 scores using indexes `scores[0]` through `scores[9]`. Attempts to access an out of range index in the array will result in a compiler or runtime error.

We can initialize the array with values:

```go
scores := [4]int{9001, 9333, 212, 33}
```

We can use `len` to get the length of the array. `range` can be used to iterate over it:

```go
for index, value := range scores {

}
```

Arrays are efficient but rigid. We often don't know the number of elements we'll be dealing with upfront. For this, we turn to slices.

## Slices

In Go, you rarely, if ever, use arrays directly. Instead, you use slices. A slice is a lightweight structure that wraps and represents a portion of an array. There are a few ways to create a slice, and we'll go over when to use which later on. The first is a slight variation on how we created an array:

```go
scores := []int{1,4,293,4,9}
```

Unlike the array declaration, our slice isn't declared with a length within the square brackets. To understand how the two are different, let's see another way to create a slice, using `make`:

```go
scores := make([]int, 10)
```

We use `make` instead of `new` because there's more to creating a slice than just allocating the memory (which is what `new` does). Specifically, we have to allocate the memory for the underlying array and also initialize the slice.  In the above, we initialize a slice with a length of 10 and a capacity of 10. The length is the size of the slice, the capacity is the size of the underlying array. Using `make` we can specify the two separately:

```go
scores := make([]int, 0, 10)
```

This creates a slice with a length of 0 but with a capacity of 10. (If you're paying attention, you'll note that `make` and `len` *are* overloaded. Go is a language that, to the frustration of some, makes use of features which aren't exposed for developers to use.)

To better understand the interplay between length and capacity, let's look at some examples:

```go
func main() {
  scores := make([]int, 0, 10)
  scores[7] = 9033
  fmt.Println(scores)
}
```

Our first example crashes. Why? Because our slice has a length of 0. Yes, the underlying array has 10 elements, but we need to explicitly expand our slice in order to access those elements. One way to expand a slice is via `append`:

```go
func main() {
  scores := make([]int, 0, 10)
  scores = append(scores, 5)
  fmt.Println(scores) // prints [5]
}
```

But that changes the intent of our original code. Appending to a slice of length 0 will set the first element. For whatever reason, our crashing code wanted to set the element at index 7. To do this, we can re-slice our slice:

```go
func main() {
  scores := make([]int, 0, 10)
  scores = scores[0:8]
  scores[7] = 9033
  fmt.Println(scores)
}
```

How large can we resize a slice? Up to its capacity which, in this case, is 10. You might be thinking *this doesn't actually solve the fixed-length issue of arrays.* It turns out that `append` is pretty special. If the underlying array is full, it will create a new larger array and copy the values over (this is exactly how dynamic arrays work in PHP, Python, Ruby, JavaScript, ...). This is why, in the example above that used `append`, we had to re-assign the value returned by `append` to our `scores` variable: `append` might have created a new value if the original had no more space.

If I told you that Go grew arrays with a 2x algorithm, can you guess what the following will output?

```go
func main() {
  scores := make([]int, 0, 5)
  c := cap(scores)
  fmt.Println(c)

  for i := 0; i < 25; i++ {
    scores = append(scores, i)

    // if our capacity has changed,
    // Go had to grow our array to accommodate the new data
    if cap(scores) != c {
      c = cap(scores)
      fmt.Println(c)
    }
  }
}
```

The initial capacity of `scores` is 5. In order to hold 20 values, it'll have to be expanded 3 times with a capacity of 10, 20 and finally 40.

As a final example, consider:

```go
func main() {
  scores := make([]int, 5)
  scores = append(scores, 9332)
  fmt.Println(scores)
}
```

Here, the output is going to be `[0, 0, 0, 0, 0, 9332]`. Maybe you thought it would be `[9332, 0, 0, 0, 0]`? To a human, that might seem logical. To a compiler, you're telling it to append a value to a slice that already holds 5 values.

Ultimately, there are four common ways to initialize a slice:

```go
names := []string{"leto", "jessica", "paul"}
checks := make([]bool, 10)
var names []string
scores := make([]int, 0, 20)
```

When do you use which? The first one shouldn't need much of an explanation. You use this when you know the values that you want in the array ahead of time.

The second one is useful when you'll be writing into specific indexes of a slice. For example:

```go
func extractPowers(saiyans []*Saiyans) []int {
  powers := make([]int, len(saiyans))
  for index, saiyan := range saiyans {
    powers[index] = saiyan.Power
  }
  return powers
}
```

The third version is a nil slice and is used in conjunction with `append`, when the number of elements is unknown.

The last version lets us specify an initial capacity; useful if we have a general idea of how many elements we'll need.

Even when you know the size, `append` can be used. It's largely a matter of preference:

```go
func extractPowers(saiyans []*Saiyans) []int {
  powers := make([]int, 0, len(saiyans))
  for _, saiyan := range saiyans {
    powers = append(powers, saiyan.Power)
  }
  return powers
}
```

Slices as wrappers to arrays is a powerful concept. Many languages have the concept of slicing an array. Both JavaScript and Ruby arrays have a `slice` method. You can also get a slice in Ruby by using `[START..END]` or in Python via `[START:END]`. However, in these languages, a slice is actually a new array with the values of the original copied over. If we take Ruby, what's the output of the following?

```go
scores = [1,2,3,4,5]
slice = scores[2..4]
slice[0] = 999
puts scores
```

The answer is `[1, 2, 3, 4, 5]`. That's because `slice` is a completely new array with copies of values. Now, consider the Go equivalent:

```go
scores := []int{1,2,3,4,5}
slice := scores[2:4]
slice[0] = 999
fmt.Println(scores)
```

The output is `[1, 2, 999, 4, 5]`.

This changes how you code. For example, a number of functions take a position parameter. In JavaScript, if we want to find the first space in a string (yes, slices work on strings too!) after the first five characters, we'd write:

```go
haystack = "the spice must flow";
console.log(haystack.indexOf(" ", 5));
```

In Go, we leverage slices:

```go
strings.Index(haystack[5:], " ")
```

We can see from the above example, that `[X:]` is shorthand for *from X to the end* while `[:X]` is shorthand for *from the start to X*. Unlike other languages, Go doesn't support negative values. If we want all of the values of a slice except the last, we do:

```go
scores := []int{1, 2, 3, 4, 5}
scores = scores[:len(scores)-1]
```

The above is the start of an efficient way to remove a value from an unsorted slice:

```go
func main() {
  scores := []int{1, 2, 3, 4, 5}
  scores = removeAtIndex(scores, 2)
  fmt.Println(scores)
}

func removeAtIndex(source []int, index int) []int {
  lastIndex := len(source) - 1
  //swap the last value and the value we want to remove
  source[index], source[lastIndex] = source[lastIndex], source[index]
  return source[:lastIndex]
}
```

Finally, now that we know about slices, we can look at another commonly used built-in function: `copy`. `copy` is one of those functions that highlights how slices change the way we code. Normally, a method that copies values from one array to another has 5 parameters: `source`, `sourceStart`, `count`, `destination` and `destinationStart`. With slices, we only need two:

```go
import (
  "fmt"
  "math/rand"
  "sort"
)

func main() {
  scores := make([]int, 100)
  for i := 0; i < 100; i++ {
    scores[i] = int(rand.Int31n(1000))
  }
  sort.Ints(scores)

  worst := make([]int, 5)
  copy(worst, scores[:5])
  fmt.Println(worst)
}
```

Take some time and play with the above code. Try variations. See what happens if you change copy to something like `copy(worst[2:4], scores[:5])`, or what if you try to copy more or less than `5` values into `worst`?

## Maps

Maps in Go are what other languages call hashtables or dictionaries. They work as you expect: you define a key and value, and can get, set and delete values from it.

Maps, like slices, are created with the `make` function. Let's look at an example:

```go
func main() {
  lookup := make(map[string]int)
  lookup["goku"] = 9001
  power, exists := lookup["vegeta"]

  // prints 0, false
  // 0 is the default value for an integer
  fmt.Println(power, exists)
}
```

To get the number of keys, we use `len`. To remove a value based on its key, we use `delete`:

```go
// returns 1
total := len(lookup)

// has no return, can be called on a non-existing key
delete(lookup, "goku")
```

Maps grow dynamically. However, we can supply a second argument to `make` to set an initial size:

```go
lookup := make(map[string]int, 100)
```

If you have some idea of how many keys your map will have, defining an initial size can help with performance.

When you need a map as a field of a structure, you define it as:

```go
type Saiyan struct {
  Name string
  Friends map[string]*Saiyan
}
```

One way to initialize the above is via:

```go
goku := &Saiyan{
  Name: "Goku",
  Friends: make(map[string]*Saiyan),
}
goku.Friends["krillin"] = ... //todo load or create Krillin
```

There's yet another way to declare and initialize values in Go. Like `make`, this approach is specific to maps and arrays. We can declare as a composite literal:

```go
lookup := map[string]int{
  "goku": 9001,
  "gohan": 2044,
}
```

We can iterate over a map using a `for` loop combined with the `range` keyword:

```go
for key, value := range lookup {
  ...
}
```

Iteration over maps isn't ordered. Each iteration over a lookup will return the key value pair in a random order.

## Pointers versus Values

We finished Chapter 2 by looking at whether you should assign and pass pointers or values. We'll now have this same conversation with respect to array and map values. Which of these should you use?

```go
a := make([]Saiyan, 10)
//or
b := make([]*Saiyan, 10)
```

Many developers think that passing `b` to, or returning it from, a function is going to be more efficient. However, what's being passed/returned is a copy of the slice, which itself is a reference. So with respect to passing/returning the slice itself, there's no difference.

Where you will see a difference is when you modify the values of a slice or map. At this point, the same logic that we saw in Chapter 2 applies. So the decision on whether to define an array of pointers versus an array of values comes down to how you use the individual values, not how you use the array or map itself.

## Before You Continue

Arrays and maps in Go work much like they do in other languages. If you're used to dynamic arrays, there might be a small adjustment, but `append` should solve most of your discomfort. If we peek beyond the superficial syntax of arrays, we find slices. Slices are powerful and they have a surprisingly large impact on the clarity of your code.

There are edge cases that we haven't covered, but you're not likely to run into them. And, if you do, hopefully the foundation we've built here will let you understand what's going on.

# Chapter 4 - Code Organization and Interfaces

It's now time to look at how to organize our code.

## Packages

To keep more complicated libraries and systems organized, we need to learn about packages. In Go, package names follow the directory structure of your Go workspace. If we were building a shopping system, we'd probably start with a package name "shopping" and put our source files in `$GOPATH/src/shopping/`.

We don't want to put everything inside this folder though. For example, maybe we want to isolate some database logic inside its own folder. To achieve this, we create a subfolder at `$GOPATH/src/shopping/db`. The package name of the files within this subfolder is simply `db`, but to access it from another package, including the `shopping` package, we need to import `shopping/db`.

In other words, when you name a package, via the `package` keyword, you provide a single value, not a complete hierarchy (e.g., "shopping" or "db"). When you import a package, you specify the complete path.

Let's try it. Inside your Go workspace's `src` folder (which we set up in Getting Started of the Introduction), create a new folder called `shopping` and a subfolder within it called `db`.

Inside of `shopping/db`, create a file called `db.go` and add the following code:

```go
package db

type Item struct {
  Price float64
}

func LoadItem(id int) *Item {
  return &Item{
    Price: 9.001,
  }
}
```

Notice that the name of the package is the same as the name of the folder. Also, obviously, we aren't actually accessing the database. We're just using this as an example to show how to organize code.

Now, create a file called `pricecheck.go` inside of the main `shopping` folder. Its content is:

```go
package shopping

import (
  "shopping/db"
)

func PriceCheck(itemId int) (float64, bool) {
  item := db.LoadItem(itemId)
  if item == nil {
    return 0, false
  }
  return item.Price, true
}
```

It's tempting to think that importing `shopping/db` is somehow special because we're inside the `shopping` package/folder already. In reality, you're importing `$GOPATH/src/shopping/db`, which means you could just as easily import `test/db` so long as you had a package named `db` inside of your workspace's `src/test` folder.

If you're building a package, you don't need anything more than what we've seen. To build an executable, you still need a `main`. The way I prefer to do this is to create a subfolder called `main` inside of `shopping` with a file called `main.go` and the following content:

```go
package main

import (
  "shopping"
  "fmt"
)

func main() {
  fmt.Println(shopping.PriceCheck(4343))
}
```

You can now run your code by going into your `shopping` project and typing:

```
go run main/main.go
```

### Cyclical Imports

As you start writing more complex systems, you're bound to run into cyclical imports. This happens when package A imports package B but package B imports package A (either directly or indirectly through another package). This is something the compiler won't allow.

Let's change our shopping structure to cause the error.

Move the `Item` definition from `shopping/db/db.go` into `shopping/pricecheck.go`. Your `pricecheck.go` file should now look like:

```go
package shopping

import (
  "shopping/db"
)

type Item struct {
  Price float64
}

func PriceCheck(itemId int) (float64, bool) {
  item := db.LoadItem(itemId)
  if item == nil {
    return 0, false
  }
  return item.Price, true
}
```

If you try to run the code, you'll get a couple of errors from `db/db.go` about `Item` being undefined. This makes sense. `Item` no longer exists in the `db` package; it's been moved to the shopping package. We need to change `shopping/db/db.go` to:

```go
package db

import (
  "shopping"
)

func LoadItem(id int) *shopping.Item {
  return &shopping.Item{
    Price: 9.001,
  }
}
```

Now when you try to run the code, you'll get a dreaded *import cycle not allowed* error. We solve this by introducing another package which contains shared structures. Your directory structure should look like:

```
$GOPATH/src
  - shopping
    pricecheck.go
    - db
      db.go
    - models
      item.go
    - main
      main.go
```

`pricecheck.go` will still import `shopping/db`, but `db.go` will now import `shopping/models` instead of `shopping`, thus breaking the cycle. Since we moved the shared `Item` structure to `shopping/models/item.go`, we need to change `shopping/db/db.go` to reference the `Item` structure from `models` package:

```go
package db

import (
  "shopping/models"
)

func LoadItem(id int) *models.Item {
  return &models.Item{
    Price: 9.001,
  }
}
```

You'll often need to share more than just `models`, so you might have other similar folder named `utilities` and such. The important rule about these shared packages is that they shouldn't import anything from the `shopping` package or any sub-packages. In a few sections, we'll look at interfaces which can help us untangle these types of dependencies.

### Visibility

Go uses a simple rule to define what types and functions are visible outside of a package. If the name of the type or function starts with an uppercase letter, it's visible. If it starts with a lowercase letter, it isn't.

This also applies to structure fields. If a structure field name starts with a lowercase letter, only code within the same package will be able to access them.

For example, if our `items.go` file had a function that looked like:

```go
func NewItem() *Item {
  // ...
}
```

it could be called via `models.NewItem()`. But if the function was named `newItem`, we wouldn't be able to access it from a different package.

Go ahead and change the name of the various functions, types and fields from the `shopping` code. For example, if you rename the `Item's` `Price` field to `price`, you should get an error.

### Package Management

The `go` command we've been using to `run` and `build` has a `get` subcommand which is used to fetch third-party libraries. `go get` supports various protocols but for this example, we'll be getting a library from Github, meaning, you'll need `git` installed on your computer.

Assuming you already have git installed, from a shell/command prompt, enter:

```
go get github.com/mattn/go-sqlite3
```

`go get` fetches the remote files and stores them in your workspace. Go ahead and check your `$GOPATH/src`. In addition to the `shopping` project that we created, you'll now see a `github.com` folder. Within, you'll see a `mattn` folder which contains a `go-sqlite3` folder.

We just talked about how to import packages that live in our workspace. To use our newly gotten `go-sqlite3` package, we'd import it like so:

```go
import (
  "github.com/mattn/go-sqlite3"
)
```

I know this looks like a URL but in reality, it'll simply import the `go-sqlite3` package which it expects to find in `$GOPATH/src/github.com/mattn/go-sqlite3`.

### Dependency Management

`go get` has a couple of other tricks up its sleeve. If we `go get` within a project, it'll scan all the files, looking for `imports` to third-party libraries and will download them. In a way, our own source code becomes a `Gemfile` or `package.json`.

If you call `go get -u` it'll update the packages (or you can update a specific package via `go get -u FULL_PACKAGE_NAME`).

Eventually, you might find `go get` inadequate. For one thing, there's no way to specify a revision, it always points to the master/head/trunk/default. This is an even larger problem if you have two projects needing different versions of the same library.

To solve this, you can use a third-party dependency management tool. They are still young, but two promising ones are [goop](https://github.com/nitrous-io/goop) and [godep](https://github.com/tools/godep). A more complete list is available at the [go-wiki](https://code.google.com/p/go-wiki/wiki/PackageManagementTools).

## Interfaces

Interfaces are types that define a contract but not an implementation. Here's an example:

```go
type Logger interface {
  Log(message string)
}
```

You might be wondering what purpose this could possibly serve. Interfaces help decouple your code from specific implementations. For example, we might have various types of loggers:

```go
type SqlLogger struct { ... }
type ConsoleLogger struct { ... }
type FileLogger struct { ... }
```

Yet by programming against the interface, rather than these concrete implementations, we can easily change (and test) which we use without any impact to our code.

How would you use one? Just like any other type, it could be a structure's field:

```go
type Server struct {
  logger Logger
}
```

or a function parameter (or return value):

```go
func process(logger Logger) {
  logger.Log("hello!")
}
```

In a language like C# or Java, we have to be explicit when a class implements an interface:

```go
public class ConsoleLogger : Logger {
  public void Logger(message string) {
    Console.WriteLine(message)
  }
}
```

In Go, this happens implicitly. If your structure has a function name `Log` with a `string` parameter and no return value, then it can be used as a `Logger`. This cuts down on the verboseness of using interfaces:

```go
type ConsoleLogger struct {}
func (l ConsoleLogger) Log(message string) {
  fmt.Println(message)
}
```

It also tends to promote small and focused interfaces. The standard library is full of interfaces. The `io` package has a handful of popular ones such as `io.Reader`, `io.Writer`, and `io.Closer`. If you write a function that expects a parameter that you'll only be calling `Close()` on, you absolutely should accept an `io.Closer` rather than whatever concrete type you're using.

Interfaces can also participate in composition. And, interfaces themselves can be composed of other interfaces. For example, `io.ReadCloser` is an interface composed of the `io.Reader` interface as well as the `io.Closer` interface.

Finally, interfaces are commonly used to avoid cyclical imports. Since they don't have implementations, they'll have limited dependencies.

## Before You Continue

Ultimately, how you structure your code around Go's workspace is something that you'll only feel comfortable with after you've written a couple of non-trivial projects. What's most important for you to remember is the tight relationship between package names and your directory structure (not just within a project, but within the entire workspace).

The way Go handles visibility of types is straightforward and effective. It's also consistent. There are a few things we haven't looked at, such as constants and global variables but rest assured, their visibility is determined by the same naming rule.

Finally, if you're new to interfaces, it might take some time before you get a feel for them. However, the first time you see a function that expects something like `io.Reader`, you'll find yourself thanking the author for not demanding more than he or she needed.

# Chapter 5 - Tidbits

In this chapter, we'll talk about a miscellany of Go's feature which didn't quite fit anywhere else.

## Error Handling

Go's preferred way to deal with errors is through return values, not exceptions. Consider the `strconv.Atoi` function which takes a string and tries to convert it to an integer:

```go
package main

import (
  "fmt"
  "os"
  "strconv"
)

func main() {
  if len(os.Args) != 2 {
    os.Exit(1)
  }

  n, err := strconv.Atoi(os.Args[1])
  if err != nil {
    fmt.Println("not a valid number")
  } else {
    fmt.Println(n)
  }
}
```

You can create your own error type; the only requirement is that it fulfills the contract of the built-in `error` interface, which is:

```go
type error interface {
  Error() string
}
```

More commonly, we can create our own errors by importing the `errors` package and using it in the `New` function:

```go
import (
  "errors"
)


func process(count int) error {
  if count < 1 {
    return errors.New("Invalid count")
  }
  ...
  return nil
}
```

There's a common pattern in Go's standard library of using error variables. For example, the `io` package has an `EOF` variable which is defined as:

```go
var EOF = errors.New("EOF")
```

This is a package variable (it's defined outside of a function) which is publicly accessible (upper-case first letter). Various functions can return this error, say when we're reading from a file or STDIN. If it makes contextual sense, you should use this error, too. As consumers, we can use this singleton:

```go
package main

import (
  "fmt"
  "io"
)

func main() {
  var input int
  _, err := fmt.Scan(&input)
  if err == io.EOF {
    fmt.Println("no more input!")
  }
}
```

As a final note, Go does have `panic` and `recover` functions. `panic` is like throwing an exception while `recover` is like `catch`; they are rarely used.

## Defer

Even though Go has a garbage collector, some resources require that we explicitly release them. For example, we need to `Close()` files after we're done with them. This sort of code is always dangerous. For one thing, as we're writing a function, it's easy to forget to `Close` something that we declared 10 lines up. For another, a function might have multiple return points. Go's solution is the `defer` keyword:

```go
package main

import (
  "fmt"
  "os"
)

func main() {
  file, err := os.Open("a_file_to_read")
  if err != nil {
    fmt.Println(err)
    return
  }
  defer file.Close()
  // read the file
}
```

If you try to run the above code, you'll probably get an error (the file doesn't exist). The point is to show how `defer` works. Whatever you `defer` will be executed after the enclosing function (in this case `main()`) returns, even if it does so violently. This lets you release resources near where it’s initialized and takes care of multiple return points.

## go fmt

Most programs written in Go follow the same formatting rules, namely, a tab is used to indent and braces go on the same line as their statement.

I know, you have your own style and you want to stick to it. That's what I did for a long time, but I'm glad I eventually gave in. A big reason for this is the `go fmt` command. It's easy to use and authoritative (so no one argues over meaningless preferences).

When you're inside a project, you can apply the formatting rule to it and all sub-projects via:

```
go fmt ./...
```

Give it a try. It does more than indent your code; it also aligns field declarations and alphabetically orders imports.

## Initialized If

Go supports a slightly modified if-statement, one where a value can be initiated prior to the condition being evaluated:

```go
if x := 10; count > x {
  ...
}
```

That's a pretty silly example. More realistically, you might do something like:

```go
if err := process(); err != nil {
  return err
}
```

Interestingly, while the values aren't available outside the if-statement, they are available inside any `else if` or `else`.

## Empty Interface and Conversions

In most object-oriented languages, a built-in base class, often named `object`, is the superclass for all other classes. Go, having no inheritance, doesn't have such a superclass. What it does have is an empty interface with no methods: `interface{}`. Since every type implements all 0 of the empty interface's methods, and since interfaces are implicitly implemented, every type fulfills the contract of the empty interface.

 If we wanted to, we could write an `add` function with the following signature:

```go
func add(a interface{}, b interface{}) interface{} {
  ...
}
```

To convert an interface variable to an explicit type, you use `.(TYPE)`:

```go
return a.(int) + b.(int)
```

Note that if the underlying type is not `int`, the above will result in an error.

You also have access to a powerful type switch:

```go
switch a.(type) {
  case int:
    fmt.Printf("a is now an int and equals %d\n", a)
  case bool, string:
    // ...
  default:
    // ...
}
```

You'll see and probably use the empty interface more than you might first expect. Admittedly, it won't result in clean code. Converting values back and forth is ugly and dangerous but sometimes, in a static language, it's the only choice.

## Strings and Byte Arrays

Strings and byte arrays are closely related. We can easily convert one to the other:

```go
stra := "the spice must flow"
byts := []byte(stra)
strb := string(byts)
```

In fact, this way of converting is common across various types as well. Some functions explicitly expect an `int32` or an `int64` or their unsigned counterparts. You might find yourself having to do things like:

```go
int64(count)
```

Still, when it comes to bytes and strings, it's probably something you'll end up doing often. Do note that when you use `[]byte(X)` or `string(X)`, you're creating a copy of the data. This is necessary because strings are immutable.

Strings are made of `runes` which are unicode code points. If you take the length of a string, you might not get what you expect. The following prints 3:

    fmt.Println(len("椒"))

If you iterate over a string using `range`, you'll get runes, not bytes. Of course, when you turn a string into a `[]byte` you'll get the correct data.

## Function Type

Functions are first-class types:

```go
type Add func(a int, b int) int
```

which can then be used anywhere -- as a field type, as a parameter, as a return value.

```go
package main

import (
  "fmt"
)

type Add func(a int, b int) int

func main() {
  fmt.Println(process(func(a int, b int) int{
      return a + b
  }))
}

func process(adder Add) int {
  return adder(1, 2)
}
```

Using functions like this can help decouple code from specific implementations much like we achieve with interfaces.

## Before You Continue

We looked at various aspects of programming with Go. Most notably, we saw how error handling behaves and how to release resources such as connections and open files. Many people dislike Go's approach to error handling. It can feel like a step backwards. Sometimes, I agree. Yet, I also find that it results in code that's easier to follow. `defer` is an unusual but practical approach to resource management. In fact, it isn't tied to resource management only. You can use `defer` for any purpose, such as logging when a function exits.

Certainly, we haven't looked at all of the tidbits Go has to offer. But you should be feeling comfortable enough to tackle whatever you come across.

# Chapter 6 - Concurrency

Go is often described as a concurrent-friendly language. The reason for this is that it provides a simple syntax over two powerful mechanisms: goroutines and channels.

## Goroutines

A goroutine is similar to a thread, but it is scheduled by Go, not the OS. Code that runs in a goroutine can run concurrently with other code. Let's look at an example:

```go
package main

import (
  "fmt"
  "time"
)

func main() {
  fmt.Println("start")
  go process()
  time.Sleep(time.Millisecond * 10) // this is bad, don't do this!
  fmt.Println("done")
}

func process() {
  fmt.Println("processing")
}
```

There are a few interesting things going on here, but the most important is how we start a goroutine. We simply use the `go` keyword followed by the function we want to execute. If we just want to run a bit of code, such as the above, we can use an anonymous function. Do note that anonymous functions aren't only used with goroutines, however.

```go
go func() {
  fmt.Println("processing")
}()
```

Goroutines are easy to create and have little overhead. Multiple goroutines will end up running on the same underlying OS thread. This is often called an M:N threading model because we have M application threads (goroutines) running on N OS threads. The result is that a goroutine has a fraction of overhead (a few KB) than OS threads. On modern hardware, it's possible to have millions of goroutines.

Furthermore, the complexity of mapping and scheduling is hidden. We just say *this code should run concurrently* and let Go worry about making it happen.

If we go back to our example, you'll notice that we had to `Sleep` for a few milliseconds. That's because the main process exits before the goroutine gets a chance to execute (the process doesn't wait until all goroutines are finished before exiting). To solve this, we need to coordinate our code.

## Synchronization

Creating goroutines is trivial, and they are so cheap that we can start many; however, concurrent code needs to be coordinated. To help with this problem, Go provides `channels`. Before we look at `channels`, I think it's important to understand a little bit about the basics of concurrent programming.

Writing concurrent code requires that you pay specific attention to where and how you read and write values. In some ways, it's like programming without a garbage collector -- it requires that you think about your data from a new angle, always watchful for possible danger. Consider:

```go
package main

import (
  "fmt"
  "time"
)

var counter = 0

func main() {
  for i := 0; i < 20; i++ {
    go incr()
  }
  time.Sleep(time.Millisecond * 10)
}

func incr() {
  counter++
  fmt.Println(counter)
}
```

What do you think the output will be?

If you think the output is `1, 2, ... 20` you're both right and wrong. It's true that if you run the above code, you'll sometimes get that output. However, the reality is that the behavior is undefined. Why? Because we potentially have multiple (two in this case) goroutines writing to the same variable, `counter`, at the same time. Or, just as bad, one goroutine would be reading `counter` while another writes to it.

Is that really a danger? Yes, absolutely. `counter++` might seem like a simple line of code, but it actually gets broken down into multiple assembly statements -- the exact nature is dependent on the platform that you're running. If you run this example, you'll see that very often the numbers are printed in a weird order, and/or numbers are duplicated/missing. There are worse possibilities too, such as system crashes or accessing an arbitrary piece of data and incrementing it!

The only concurrent thing you can safely do to a variable is to read from it. You can have as many readers as you want, but writes need to be synchronized. There are various ways to do this, including using some truly atomic operations that rely on special CPU instructions. However, the most common approach is to use a mutex:

```go
package main

import (
  "fmt"
  "time"
  "sync"
)

var (
  counter = 0
  lock sync.Mutex
)

func main() {
  for i := 0; i < 20; i++ {
    go incr()
  }
  time.Sleep(time.Millisecond * 10)
}

func incr() {
  lock.Lock()
  defer lock.Unlock()
  counter++
  fmt.Println(counter)
}
```

A mutex serializes access to the code under lock. The reason we simply define our lock as `lock sync.Mutex` is because the default value of a `sync.Mutex` is unlocked.

Seems simple enough? The example above is deceptive. There's a whole class of serious bugs that can arise when doing concurrent programming. First of all, it isn't always so obvious what code needs to be protected. While it might be tempting to use coarse locks (locks that cover a large amount of code), that undermines the very reason we're doing concurrent programming in the first place. We generally want fine locks; else, we end up with a ten-lane highway that suddenly turns into a one-lane road.

The other problem has to do with deadlocks. With a single lock, this isn't a problem, but if you're using two or more locks around the same code, it's dangerously easy to have situations where goroutineA holds lockA but needs access to lockB, while goroutineB holds lockB but needs access to lockA.

It actually *is* possible to deadlock with a single lock, if we forget to release it. This isn't as dangerous as a multi-lock deadlock (because those are *really* tough to spot), but just so you can see what happens, try running:

```go
package main

import (
  "time"
  "sync"
)

var (
  lock sync.Mutex
)

func main() {
  go func() { lock.Lock() }()
  time.Sleep(time.Millisecond * 10)
  lock.Lock()
}
```

There's more to concurrent programming than what we've seen so far. For one thing, there's another common mutex called a read-write mutex. This exposes two locking functions: one to lock for reading and one to lock for writing. This distinction allows multiple simultaneous readers while ensuring that writing is exclusive. In Go, `sync.RWMutex` is such a lock. In addition to the `Lock` and `Unlock` methods of a `sync.Mutex`, it also exposes `RLock` and `RUnlock` methods; where `R` stands for *Read*. While read-write mutexes are commonly used, they place an additional burden on developers: we must now pay attention to not only when we're accessing data, but also how.

Furthermore, part of concurrent programming isn't so much about serializing access across the narrowest possible piece of code; it's also about coordinating multiple goroutines. For example, sleeping for 10 milliseconds isn't a particularly elegant solution. What if a goroutine takes more than 10 milliseconds? What if it takes less and we're just wasting cycles? Also, what if instead of just waiting for goroutines to finish, we want to tell one *hey, I have new data for you to process!*?

These are all things that are doable without `channels`. Certainly for simpler cases, I believe you **should** use primitives such as `sync.Mutex` and `sync.RWMutex`, but as we'll see in the next section, `channels` aim at making concurrent programming cleaner and less error-prone.

## Channels

The challenge with concurrent programming stems from sharing data. If your goroutines share no data, you needn't worry about synchronizing them. That isn't an option for all systems, however. In fact, many systems are built with the exact opposite goal in mind: to share data across multiple requests. An in-memory cache or a database, are good examples of this. This is becoming an increasingly common reality.

Channels help make concurrent programming saner by taking shared data out of the picture. A channel is a communication pipe between goroutines which is used to pass data. In other words, a goroutine that has data can pass it to another goroutine via a channel. The result is that, at any point in time, only one goroutine has access to the data.

A channel, like everything else, has a type. This is the type of data that we'll be passing through our channel. For example, to create a channel which can be used to pass an integer around, we'd do:

```go
c := make(chan int)
```

The type of this channel is `chan int`. Therefore, to pass this channel to a function, our signature looks like:

```go
func worker(c chan int) { ... }
```

Channels support two operations: receiving and sending. We send to a channel by doing:

```
CHANNEL <- DATA
```

and receive from one by doing

```
VAR := <-CHANNEL
```

The arrow points in the direction that data flows. When sending, the data flows into the channel. When receiving, the data flows out of the channel.

The final thing to know before we look at our first example is that receiving and sending to and from a channel is blocking. That is, when we receive from a channel, execution of the goroutine won't continue until data is available. Similarly, when we send to a channel, execution won't continue until the data is received.

Consider a system with incoming data that we want to handle in separate goroutines. This is a common requirement. If we did our data-intensive processing on the goroutine which accepts the incoming data, we'd risk timing out clients. First, we'll write our worker. This could be a simple function, but I'll make it part of a structure since we haven't seen goroutines used like this before:

```go
type Worker struct {
  id int
}

func (w Worker) process(c chan int) {
  for {
    data := <-c
    fmt.Printf("worker %d got %d\n", w.id, data)
  }
}
```

Our worker is simple. It waits until data is available then "processes" it. Dutifully, it does this in a loop, forever waiting for more data to process.

To use this, the first thing we'd do is start some workers:

```go
c := make(chan int)
for i := 0; i < 5; i++ {
  worker := &Worker{id: i}
  go worker.process(c)
}
```

And then we can give them some work:

```go
for {
  c <- rand.Int()
  time.Sleep(time.Millisecond * 50)
}
```

Here's the complete code to make it run:

```go
package main

import (
  "fmt"
  "time"
  "math/rand"
)

func main() {
  c := make(chan int)
  for i := 0; i < 5; i++ {
    worker := &Worker{id: i}
    go worker.process(c)
  }

  for {
    c <- rand.Int()
    time.Sleep(time.Millisecond * 50)
  }
}

type Worker struct {
  id int
}

func (w *Worker) process(c chan int) {
  for {
    data := <-c
    fmt.Printf("worker %d got %d\n", w.id, data)
  }
}
```

We don't know which worker is going to get what data. What we do know, what Go guarantees, is that the data we send to a channel will only be received by a single receiver.

Notice that the only shared state is the channel, which we can safely receive from and send to concurrently. Channels provide all of the synchronization code we need and also ensure that, at any given time, only one goroutine has access to a specific piece of data.

### Buffered Channels

Given the above code, what happens if we have more data coming in than we can handle? You can simulate this by changing the worker to sleep after it has received data:

```go
for {
  data := <-c
  fmt.Printf("worker %d got %d\n", w.id, data)
  time.Sleep(time.Millisecond * 500)
}
```

What's happening is that our main code, the one that accepts the user's incoming data (which we just simulated with a random number generator) is blocking as it sends to the channel because no receiver is available.

In cases where you need high guarantees that the data is being processed, you probably will want to start blocking the client. In other cases, you might be willing to loosen those guarantees. There are a few popular strategies to do this. The first is to buffer the data. If no worker is available, we want to temporarily store the data in some sort of queue. Channels have this buffering capability built-in. When we created our channel with `make`, we can give our channel a length:

```go
c := make(chan int, 100)
```

You can make this change, but you'll notice that the processing is still choppy. Buffered channels don't add more capacity; they merely provide a queue for pending work and a good way to deal with a sudden spike. In our example, we're continuously pushing more data than our workers can handle.

Nevertheless, we can get a sense that the buffered channel is, in fact, buffering by looking at the channel's `len`:

```go
for {
  c <- rand.Int()
  fmt.Println(len(c))
  time.Sleep(time.Millisecond * 50)
}
```

You can see that it grows and grows until it fills up, at which point sending to our channel start to block again.

### Select

Even with buffering, there comes a point where we need to start dropping messages. We can't use up an infinite amount of memory hoping a worker frees up. For this, we use Go's `select`.

Syntactically, `select` looks a bit like a switch. With it, we can provide code for when the channel isn't available to send to. First, let's remove our channel's buffering so that we can clearly see how `select` works:

```go
c := make(chan int)
```

Next, we change our `for` loop:

```go
for {
  select {
  case c <- rand.Int():
    //optional code here
  default:
    //this can be left empty to silently drop the data
    fmt.Println("dropped")
  }
  time.Sleep(time.Millisecond * 50)
}
```

We're pushing out 20 messages per second, but our workers can only handle 10 per second; thus, half the messages get dropped.

This is only the start of what we can accomplish with `select`. A main purpose of select is to manage multiple channels. Given multiple channels, `select` will block until the first one becomes available. If no channel is available, `default` is executed if one is provided. A channel is randomly picked when multiple are available.

It's hard to come up with a simple example that demonstrates this behavior as it's a fairly advanced feature. The next section might help illustrate this though.

### Timeout

We've looked at buffering messages as well as simply dropping them. Another popular option is to timeout. We're willing to block for some time, but not forever. This is also something easy to achieve in Go. Admittedly, the syntax might be hard to follow but it's such a neat and useful feature that I couldn't leave it out.

To block for a maximum amount of time, we can use the `time.After` function. Let's look at it then try to peek beyond the magic. To use this, our sender becomes:

```go
for {
  select {
  case c <- rand.Int():
  case <-time.After(time.Millisecond * 100):
    fmt.Println("timed out")
  }
  time.Sleep(time.Millisecond * 50)
}
```

`time.After` returns a channel, so we can `select` from it. The channel is written to after the specified time expires. That's it. There's nothing more magical than that. If you're curious, here's what an implementation of `after` could look like:

```go
func after(d time.Duration) chan bool {
  c := make(chan bool)
  go func() {
    time.Sleep(d)
    c <- true
  }()
  return c
}
```

Back to our `select`, there are a couple of things to play with. First, what happens if you add the `default` case back? Can you guess? Try it. If you aren't sure what's going on, remember that `default` fires immediately if no channel is available.

Also, `time.After` is a channel of type `chan time.Time`. In the above example, we simply discard the value that was sent to the channel. If you want though, you can receive it:

```go
case t := <-time.After(time.Millisecond * 100):
  fmt.Println("timed out at", t)
```

Pay close attention to our `select`. Notice that we're sending to `c` but receiving from `time.After`. `select` works the same regardless of whether we're receiving from, sending to, or any combination of channels:

* The first available channel is chosen.
* If multiple channels are available, one is randomly picked.
* If no channel is available, the default case is executed.
* If there's no default, select blocks.

Finally, it's common to see a `select` inside a `for`. Consider:

```go
for {
  select {
  case data := <-c:
    fmt.Printf("worker %d got %d\n", w.id, data)
  case <-time.After(time.Millisecond * 10):
    fmt.Println("Break time")
    time.Sleep(time.Second)
  }
}
```

## Before You Continue

If you're new to the world of concurrent programming, it might all seem rather overwhelming. It categorically demands considerably more attention and care. Go aims to make it easier.

Goroutines effectively abstract what's needed to run concurrent code. Channels help eliminate some serious bugs that can happen when data is shared by eliminating the sharing of data. This doesn't just eliminate bugs, but it changes how one approaches concurrent programming. You start to think about concurrency with respect to message passing, rather than dangerous areas of code.

Having said that, I still make extensive use of the various synchronization primitives found in the `sync` and `sync/atomic` packages. I think it's important to be comfortable with both. I encourage you to first focus on channels, but when you see a simple example that needs a short-lived lock, consider using a mutex or read-write mutex.

# Conclusion

I recently heard Go described as a *boring* language. Boring because it's easy to learn, easy to write and, most importantly, easy to read. Perhaps, I did this reality a disservice. We *did* spend three chapters talking about types and how to declare variables after all.

If you have a background in a statically typed language, much of what we saw was probably, at best, a refresher. That Go makes pointers visible and that slices are thin wrappers around arrays probably isn't overwhelming to seasoned Java or C# developers.

If you've mostly been making use of dynamic languages, you might feel a little different. It *is* a fair bit to learn. Not least of which is the various syntax around declaration and initialization. Despite being a fan of Go, I find that for all the progress towards simplicity, there's something less than simple about it. Still, it comes down to some basic rules (like you can only declare variable once and `:=` does declare the variable) and fundamental understanding (like `new(X)` or `&X{}` only allocate memory, but slices, maps and channels require more initialization and thus, `make`).

Beyond this, Go gives us a simple but effective way to organize our code. Interfaces, return-based error handling, `defer` for resource management and a simple way to achieve composition.

Last but not least is the built-in support for concurrency. There's little to say about goroutines other than they’re effective and simple (simple to use anyway). It's a good abstraction. Channels are more complicated. I always think it's important to understand basics before using high-level wrappers. I *do* think learning about concurrent programming without channels is useful. Still, channels are implemented in a way that, to me, doesn't feel quite like a simple abstraction. They are almost their own fundamental building block. I say this because they change how you write and think about concurrent programming. Given how hard concurrent programming can be, that is definitely a good thing.
