# A Proposito di Questo Libro

## Licenza

"The Little Go Book" è rilasciato sotto la licenza Attribution-NonCommercial-ShareAlike 4.0 International. Non dovresti aver pagato per leggere questo libro.

Sei libero di copiare, distribuire, modificare e mostrare il libro. Tuttavia, ti chiedo solo di attribuire sempre questo libro a me, Karl Seguin, e non usarlo per scopi commerciali.

Puoi vedere il testo completo della licenza qui:

<https://creativecommons.org/licenses/by-nc-sa/4.0/>

## Ultima Versione

Puoi trovare l'ultima versione di questo libro qui:
<https://github.com/karlseguin/the-little-go-book>

Questa è la traduzione in Italiano, di Francesco Malatesta. Puoi trovarla qui:
<https://github.com/francescomalatesta/the-little-go-book>

# Introduzione

Ho sempre avuto un rapporto di amore/odio con l'idea di imparare un nuovo linguaggio. Da una parte, infatti, i linguaggi sono fondamentali per il nostro lavoro: studiarli in un crto modo ha un impatto notevolissimo. Hai presente quel momento *aha!* che va a ridefinire le aspettative che abbiamo nei confronti di quel linguaggio? Ecco. Dall'altra parte, però, il design di un linguaggio è qualcosa di "incrementale". Impari nuove parole chiave, tipi, per poi passare al coding style e via, verso le librerie, community, paradigmi. A volte ci chiediamo se ne valga la pena davvero.

Beh, la verità è che *dobbiamo* andare avanti. A voler essere più precisi, dovremmo sempre essere tutto sommato contenti di imparare qualcosa di nuovo. Piano piano, un passo alla volta, possiamo fare nostre tutte quelle nozioni che nel tempo hanno un'importanza sempre maggiore: leggibilità, performance, testabilità, gestione delle dipendenze, documentazione, profiling e così via.

Certo una domanda resta: **perché proprio Go?**. Per quanto mi riguarda, le ragioni fondamentali sono due. In primis, perché è un linguaggio relativamente semplice con una altrettanto relativamente semplice standard library. La "sostanza" alla base di Go è proprio questa: semplificare la complessità vista in molti linguaggi negli ultimi anni. Anche l'altra ragione non è da sottovalutare però: Go sarà un ottimo strumento per completare l'arsenale di un qualsiasi sviluppatore.

Go è stato costruito come linguaggio di sistema (parliamo di sistemi operativi, driver per device e così via) e di conseguenza può essere facilmente "appetibile" per tutti gli sviluppatori C e C++. Tuttavia, stando a quello che il team di Go riporta, la fetta più grande dell'utenza di Go non è quella dei system developer. Al contrario: è quella degli application developer! Come mai? Sembra che tanti, tra coloro che costruiscono siti, servizi web, applicazioni desktop e non solo, si manifesti una necessità sempre più crescente di un certo numero di sistemi che facciano da "cuscinetto" tra il software di alto livello (applicazione) e quello di basso livello (sistema).

Può essere un sistema di messaging, caching, analisi dei dati intensiva, tool da linea di comando. I sistemi crescono in termini di complessità e di conseguenza aumenta la ricerca di software che "aiuti" l'infrastruttura. Certo, si tratta sempre di cose che possiamo implementare con Python o Ruby ma avere a disposizione un sistema di tipi più rigido e maggiori performance certo non è da sottovalutare. Detto questo, nulla ti vieta di usare Go per costruire siti web. Ci sono molti che lo fanno ma è anche vero che l'espressività di altri linguaggi può essere più adatta allo scopo. Diamo a Cesare quel che è di Cesare, insomma.

Ad ogni modo, ci sono anche altre aree in cui Go eccelle. Ad esempio, non esiste il concetto di dipendenza nel momento in cui viene eseguito un programma scritto in Go. Non bisogna preoccuparsi di quale JVM è installata, tantomeno quale versione. Anche per questo motivo Go sta diventando sempre più popolare tra tutti quelli che ne fanno uso per costruire tool da linea di comando.

Insomma, Go è indubbiamente un ottimo uso del tuo tempo. Anche perché non dovrai spendere chissà quanto tempo per impararlo ad usare: in poco tempo infatti potrai già implementare un sacco di applicazioni utili e renderti conto da solo del suo potenziale.

## Una Nota dall'Autore

Prima di scrivere questo libro ho esitato molto. Per varie ragioni. Innanzitutto, la documentazione ufficiale di Go, in particolare [Effective Go](https://golang.org/doc/effective_go.html), è un'ottima risorsa.

Inoltre, devo ammettere di essermi trovato un po' "a disagio" nello scrivere un libro su un linguaggio. Quando ho scritto "The Little MongoDB Book" ho dato per scontate alcune delle nozioni fondamentali da conoscere. Stessa cosa per "The Little Redis Book".

Qui il discorso è diverso: sapevo che non avrei potuto fare le stesse assunzioni. Insomma, come fare per capire quanto tempo spendere per parlare delle interfacce in Go sapendo che per alcuni l'argomento è nuovo, ma per altri basta un *"Go ha le interfacce"*?

Detto questo, se qualche passaggio dovesse sembrarti più oscuro del previsto, fammelo presente! Te ne sarei davvero grato.

# I Primi Passi

Se vuoi iniziare a "giocare" un po' con Go puoi dare un'occhiata al [Go Playground](https://play.golang.org/), un tool che ti permette di eseguire codice online senza dover installare nulla sulla tua macchina. Tra l'altro, il Go Playground viene spesso usato quando si chiede aiuto nei forum come [questo qui](https://groups.google.com/forum/#!forum/golang-nuts), o in posti come StackOverflow.

Installare Go, comunque, è piuttosto semplice. Puoi farlo partendo dai sorgenti ovviamente, anche se è molto più comodo usare i binari pre-compilati. Basta dare uno sguardo alla [pagina dei download](https://golang.org/dl/) sul sito ufficiale e trovare quello per la tua piattaforma.

Ora, se escludiamo alcuni esempi basilari, Go è stato progettato per "lavorare" nel momento in cui il tuo codice si trova in quello che viene definito "workspace". In poche parole, parliamo di una cartella al cui interno trovi altre cartelle `bin`, `pkg` ed `src`. Occhio, perché potresti essere tentato di impostare un progetto seguendo il tuo gusto personale. Non farlo: non è questo il caso. Go ha un modo tutto suo di gestire l'organizzazione del codice che inizialmente potrebbe farti storcere il naso.

Tendenzialmente, io metto tutto il mio codice in `~/code`. Di conseguenza, `~/code/blog` conterrà il mio blog. Per Go, il mio workspace è `~/code/go` ed il mio blog in Go si troverà in `~/code/go/src/blog`.

Per capirci: crea una cartella `go` con una sottocartella `src` al suo interno dove pensi metterai il tuo codice delle tue applicazioni Go.

Vediamo, ora, come installare Go su OSX / Linux e Windows.

## OSX / Linux

Scarica il file `tar.gz` per la tua piattaforma. Per OSX probabilmente ti interesserà `go#.#.#.darwin-amd64-osx10.8.tar.gz`, dove `#.#.#` è l'ultima versione di Go.

Estrai tutto in `/usr/local` tramite `tar -C /usr/local -xzf go#.#.#.darwin-amd64-osx10.8.tar.gz`.

Sistema quindi due variabili di sistema:

  1. `GOPATH` che punterà al tuo workspace. Nel mio caso, ad esempio, è `$HOME/code/go`.
  2. Aggiungi quindi il path dei binari di Go alla variabile `PATH`;

Puoi fare tutto questo da shell, con due `echo`.

    echo 'export GOPATH=$HOME/code/go' >> $HOME/.profile
    echo 'export PATH=$PATH:/usr/local/go/bin' >> $HOME/.profile

Per "attivare" queste variabili riavvia la shell, o esegui `source $HOME/.profile` in quella corrente.

Esegui il comando `go version`. Se vedi dell'output simile a `go version go1.3.3 darwin/amd64`, è fatta!

## Windows

Scarica l'ultima versione in formato zip. Se sei su un sistema x64 vorrai usare `go#.#.#.windows-amd64.zip`, dove `#.#.#` è l'ultima versione di Go.

Estrai il tutto in una cartella a tua scelta. `c:\Go` va più che bene.

Anche in questo caso dovrai lavorare su due variabili di sistema.

  1. `GOPATH` che punterà al tuo workspace. Nel mio caso, ad esempio, è `c:\users\goku\work\go`.
  2. Aggiungi `c:\Go\bin` alla variabile `PATH`.

Puoi gestire le variabili d'ambiente tramite `Variabili d'Ambiente` nel tab `Avanzate` del pannello di controllo `Sistema`. Occhio, in alcune versioni di Windows questa nomenclatura potrebbe cambiare leggermente.

Una volta fatto tutto, apri un prompt e digita `go version`. Se è andato tutto bene dovresti vedere un output simile a `go version go1.3.3 windows/amd64`.

# Capitolo 1 - Le Basi

Go è un linguaggio compilato e basato su tipizzazione statica. Presenta una sintassi che ricorda il C e gestisce autonomamente la garbage collection. Bello tutto, ma che significa?

## Compilazione

La compilazione è quel processo di "traduzione" del codice sorgente in un linguaggio di basso livello (come assembly, nel caso di Go), o magari altri linguaggi intermedi (come avviene per Java e C#).

A volte può rivelarsi poco piacevole lavorare con un linguaggio compilato: la procedura può essere lenta e iterare velocemente significa spendere comunque minuti oppure ore ad aspettare la compilazione. Per fortuna, la velocità di compilazione è uno degli obiettivi più importanti del design di Go.

C'è da dire che i programmi scritti in linguaggi poi compilati tendono ad essere eseguiti più velocemente e non hanno bisogno di dipendenze (questa cosa vale almeno per C, C++, Go).

## Static Typing

Per "static typing" o "tipizzazione statica" si intende un concetto molto semplice: ogni variabile deve avere un tipo ben specifico (`int`, `string`, `bool` e così via). La cosa avviene in due modi: dichiarando esplicitamente il tipo della variabile o, a volte, lasciando questo compito al compilatore. Vedremo a breve alcuni esempi.

C'è molto da dire sullo static typing: sono convinto però che sia ancora più comprensibile guardando il codice. Se sei abituato a lavorare con linguaggi dalla tipizzazione dinamica, all'inizio troverai il tutto un po' poco agevole, quasi burocratico. Non hai torto ma, come ho già detto, ci sono dei vantaggi. Specialmente quando il linguaggio è compilato.

## Sintassi C-Like

Dire che un linguaggio ha una sintassi C-Like (in italiano "simile al C") significa che se hai già lavorato con C, C++, Java, JavaScript o C#, molto probabilmente troverai Go familiare. Almeno per quanto riguarda la sintassi: ad esempio `&&` è effettivamente un AND booleano, `==` viene invece usato per le uguaglianze e le `{` parentesi `}` vengono usate per creare degli scope.

I linguaggi C-Like inoltre presentano, in genere, il punto e virgola a fine linea e le parentesi per delimitare le condizioni. In questo caso, Go non ne fa uso, anche se le parentesi possono essere comunque usate per gestire le precedenze nei controlli. Ecco un esempio:

```go
if name == "Leto" {
  print("the spice must flow")
}
```

Nel caso semplice qui sopra le parentesi non servono. Qui di seguito invece...

```go
if (name == "Goku" && power > 9000) || (name == "gohan" && power < 4000)  {
  print("super Saiyan")
}
```

... le parentesi sono effettivamente molto utili perché ci permettono di gestire l'ordine dei controlli.

## Garbage Collection

Alcune variabili, una volta create, hanno un ciclo di vita facilmente individuabile. Una variabile locale di una funzione, ad esempio, cessa di esistere nel momento in cui la funzione è stata eseguita. In altri casi, tuttavia, questo ciclo non è così ovvio... almeno per il compilatore. Pensiamo ad una variabile il cui valore viene ritornato da una funzione, o ad una reference ad un'altra variabile. In situazioni del genere può essere indubbiamente più difficile definire a priori un ciclo di vita. Senza la garbage collection, il compito di "eliminare" la variabile ad un certo punto spetta allo sviluppatore.

Come? In C, ad esempio, devi letteralmente chiamare una funzione `free(str);` su quella variabile.

I linguaggi con garbage collection però, come Ruby, Python, Javascript, C# ed ovviamente Go) sono capaci di tenere traccia di tutto e liberare la memoria appena possibile. Certo, la garbage collection aggiunge overhead ai nostri software. Tuttavia, il "prezzo" da pagare è l'assenza di tanti bug noiosi e magari difficili da trovare.

## Il Nostro Primo Programma Go

Ok, basta parlare, è arrivato il momento di scrivere, compilare ed eseguire il nostro primo programma! Apriamo il nostro editor di testo preferito e riportiamo questo codice:

```go
package main

func main() {
  println("it's over 9000!")
}
```

Salviamo il file come `main.go`. Per ora salvalo dove vuoi: non c'è bisogno di lavorare dentro il workspace Go.

Apri quindi una shell/prompt nella directory in cui hai salvato il file. Nel mio caso, `cd ~/code`. Esegui il programma con:

```
go run main.go
```

Se tutto è andato a dovere, dovresti leggere *it's over 9000!*.

Ok, adesso fermi tutti: che significa tutto questo? Abbiamo compilato il nostro codice oppure no? Facciamo un po' di chiarezza. Innanzitutto, `go run` è un comando molto utile che compila il nostro codice *e poi* lo esegue. Usa una cartella temporanea per effettuare tutte le operazioni, dopodiché esegue il nostro codice ed infine pulisce tutto. A tutti gli effetti, quindi, la compilazione c'è.

Aggiungendo l'opzione `--work` al comando run puoi vedere quale cartella verrà usata.

```
go run --work main.go
```

Per compilare esplicitamente il codice, invece, dovrai usare `go build`:

```
go build main.go
```

L'esecuzione di questo comando genererà un eseguibile `main`, pronto ad essere usato. Non scordare, se sei su Linux/OSX, di aggiungere il prefisso `./` all'eseguibile (`./main`).

L'idea alla base di tutto quello che vedi è semplice: in fase di sviluppo, usare al volo `go run` è molto utile. Al momento del deploy, però, dovrai usare `go build` e poi eseguire il programma.

### Main

Immagino che il codice del nostro primo programma sia abbastanza comprensibile: tutto quello che abbiamo fatto è stato creare una funzione e stampare una stringa con la funzione `printLn`. Come puoi facilmente immaginare, `go run` ha eseguito esattamente quella funzione perché, in Go, il punto di ingresso di un'applicazione è la funzione `main` in un package `main`. Semplice no?

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

Avrai inoltre notato la notazione `fmt.Println` per chiamare la funzione `Println`: è leggermente differente rispetto a ciò che puoi vedere in altri linguaggi. Ne parleremo, tuttavia, in un secondo momento.

Una cosa molto interessante da sapere è che Go è molto rigido per quello che riguarda l'import di package. Se un package non viene usato ma ne è specificato l'import, la compilazione non va a buon fine. Non ci credi? Prova ad eseguire questo codice:

```go
package main

import (
  "fmt"
  "os"
)

func main() {
}
```

Otterrai due errori riguardanti `fmt` ed `os`, appunto. Noioso? Si, vero. Nel tempo però imparerai ad apprezzarlo: importare qualcosa che non ti serve infatti aumenta il tempo di compilazione.

Detto questo, apro una piccola parentesi per farti notare una cosa davvero interessante. Come puoi vedere tu stesso, la documentazione della standard library fa il suo lavoro egregiamente. Guarda qui, ad esempio: <https://golang.org/pkg/fmt/#Println>. Si tratta della reference relativa alla funzione `Println` che abbiamo usato.

Ecco la cosa interessante: sei in viaggio, non hai accesso ad internet ma hai bisogno della documentazione. Come fare? Semplice:

```
godoc -http=:6060
```

Questo comando mette su al volo un server contenente la stessa identica documentazione. Non devi fare altro che puntare il tuo browser verso `http://localhost:6060`.

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

Un po' come succede per gli import, inoltre, Go non ti permette di compilare il tuo programma se hai variabili che poi non vengono usate. Questo esempio:

```go
func main() {
  name, power := "Goku", 1000
  fmt.Printf("default power is %d\n", power)
}
```

non viene compilato perché `name` è stata dichiarata ma non usata. Anche in questo caso, all'inizio sarà un po' frustrante... ma nel lungo periodo ti aiuterà a tenere il codice pulito e leggibile.

C'è tanto da sapere riguardo le variabili ed il loro assegnamento. Per ora, ricordiamoci queste semplici regole:

* se usiamo `var NAME TYPE` le dichiariamo e assegnamo loro il valore di default;
* se usiamo `NAME := VALUE` le dichiariamo e assegnamo loro il valore VALUE. Il tipo verrà "capito" automaticamente dal compilatore;

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

Come si fa ad usare una funzione che ritorna due valori? Ecco un esempio d'uso:

```go
value, exists := power("goku")
if exists == false {
  // qui gestiamo un eventuale errore...
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

Adesso tutto questo, forse, ti dice poco. In futuro però troverai molto utile avere funzioni che ritornano più valori. Troverai altrettanto utile poter scartare un certo valore ritornato con `_`.

## Prima di Proseguire

Molto probabilmente, in questo momento stai pensando di vedere tanti piccoli "pezzettini" di questo linguaggio. Pezzettini che non ancora compongono un'immagine ben definita. Nessun problema: è normale, soprattutto adesso.

Se vieni da un linguaggio dinamico, alcune cose ti sembreranno noiose, quasi controintuitive. Se vieni da linguaggi a tipizzazione statica, invece, dovresti trovarti a tuo agio. Un po' alla volta, però, sono sicuro apprezzerai in ogni caso la pulizia verso la quale sarai portato.

# Capitolo 2 - Strutture

Go non è un linguaggio orientato agli oggetti come C++, Java, Ruby o C#. Non ha oggetti, niente ereditarietà, nessun concetto associabile alla programmazione orientata agli oggetti che conosciamo, come polimorfismo od overloading.

In Go esistono le strutture, alle quali possiamo associare dei metodi. C'è anche una semplice (ma efficace) forma di composizione di queste strutture. Il risultato? Codice probabilmente più semplice, anche se a volte sentirai la mancanza di ciò che viene offerto dallo sviluppo orientato agli oggetti. (Varrebbe la pena ricordare che nell'antica battaglia del *composition over inheritance* Go è uno dei primi linguaggi che ha preso una posizione ben precisa).

Insomma, Go è abbastanza lontano dall'OOP. Tuttavia, ci sono alcune similitudini che vale la pena notare nella definizione di una struttura e di una classe. Facciamo subito un esempio: ecco una struttura. La chiameremo `Sayian`.

```go
type Saiyan struct {
  Name string
  Power int
}
```

Non è poi così illeggibile, vero?

## Dichiarazioni ed Inizializzazioni

Nel capitolo precedente, parlando delle variabili, abbiamo dato uno sguardo ai tipi "base" presenti in Go, come interi e stringhe. Ora che la nostra "conversazione" a riguardo si sta ampliando, vale la pena spiegare il concetto di puntatore (pointer) nelle prossime righe.

Dunque: abbiamo definito la nostra struttura. Diamo, adesso, un valore ad una variabile di questo tipo.

```go
goku := Saiyan{
  Name: "Goku",
  Power: 9000,
}
```

*Nota:* la virgola `,` nella struttura è necessaria anche dopo l'ultimo elemento della struttura. Senza, infatti, il compilatore restituisce un errore.

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

Non sempre avrai bisogno di accedere al valore di una variabile: in alcuni casi avrai bisogno di un puntatore a quella variabile, a quel valore. Puoi vedere un puntatore come un indirizzo specifico di memoria. Il "posto" dove trovare quel valore. Un po' come "essere a casa" e "avere l'indirizzo di casa", per capirci.

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

Sai dirmi quale sarà il suo output? Cosa? 19000?

Sbagliato. La funzione `Super`, certo, aggiunge 10000 al valore di `Power`... ma l'argomento passato alla funzione è comunque una copia del "goku originale" che si trova in `main`. Nello scope di `main`, quindi, `Power` rimane 9000.

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

Guarda bene: abbiamo fatto due piccole, ma importantissime, modifiche. Innanzitutto abbiamo aggiunto l'operatore `&`, che serve ad ottenere l'indirizzo della variabile su cui viene usato. Viene infatti chiamato l'operatore "address of". Come conseguenza, quindi, abbiamo modificato il tipo di parametro che `Super` si aspetta. Non più un `Saiyan` dunque, bensì un `*Saiyan` (o *puntatore a Saiyan*). C'è quindi una relazione tra `Saiyan` e `*Saiyan`, anche se rimangono due tipi separati e distinti.

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

Se alcune cose non ti sono chiarissime, rileggi più di una volta questa parte. Sentiti libero di fare qualche prova in più con il codice. In ogni caso non temere: continueremo ad affrontare la questione puntatore/valore più avanti.

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
fmt.Println(goku.Power) // ... stamperà "19001"
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

Sta a te decidere quale usare. Tieni a mente che molti trovano più comoda la seconda, nel caso in cui ci siano anche dei campi da inizializzare, visto che il risultato è più leggibile.

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

Ad ogni modo, a prescindere da quale sia l'approccio scelto, ricorda che scegliere il "factory pattern" visto poco sopra è molto utile: puoi separare il resto del tuo codice da tutti i dettagli relativi all'allocazione.

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
  private Person person;

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

Nonostante l'overaloading non sia qualcosa di "specifico" delle strutture, vale la pena comunque darci un'occhiata e capire come implementare una cosa del genere in Go. Di base, Go *non* supporta l'overloading. Quindi vedrai (e scriverai) spesso funzioni come `Load`, `LoadById`, `LoadByName` e così via.

Ora, dato che la composizione implicita è un (comodo) trucco del compilatore, possiamo anche "sovrascrivere" una funzione per un tipo composto. Abbinando il codice qui sotto a quello visto nell'esempio precedente...

```go
func (s *Saiyan) Introduce() {
  fmt.Printf("Hi, I'm %s. Ya!\n", s.Name)
}
```

... avremo due diverse versioni di `Introduce`. Quella della struttura `Person` sarà disponibile comunque tramite `s.Person.Introduce()`.

## Puntatori Vs. Valori

Scrivendo il codice dei tuoi programmi in Go, spesso ti chiederai: *devo usare un puntatore oppure direttamente un valore?* Beh, un valore non è una cattiva scelta in casi come:

* assegnamento di una variabile in locale;
* campo in una struttura;
* valore di ritorno di una funzione;
* parametro di una funzione;
* ricevente di un metodo;

Per il resto... nel dubbio, usa un puntatore. Ricorda che passare un valore (e non un puntatore) ad una funzione è un ottimo modo per preservare l'immutabilità. Può essere il comportamento di cui hai bisogno, altre volte invece no.

Considera poi, comunque, i costi di creazione di una copia di una tale struttura. Più la struttura è grande, meno conviene. In altri casi però potresti avere strutture semplici, come questa:

```go
type Point struct {
  X int
  Y int
}
```

... inutile direi che qui il costo di copia della struttura è rilevante quasi quanto l'accesso diretto, senza troppo overhead.

Insomma, la regola d'oro è: valuta caso per caso. La pratica rende perfetti.

## Prima di Proseguire

Questo capitolo ti ha dato una prima infarinatura sulle strutture, su come crearne un'istanza e come rendere queste strutture "ricevitori" di una funzione. Abbiamo inoltre aggiunto i puntatori al nostro bagaglio.

Nei prossimi capitoli aggiungeremo altra carne al fuoco: nuove strutture e approfondimenti sui meccanismi di questo linguaggio.

# Capitolo 3 - Map, Array e Slice

Fino ad ora abbiamo visto i tipi di base, già disponibili, e le strutture. Adesso facciamo un passo avanti: scopriamo Map, Array e Slice.

## Array

Se vieni da Python, Ruby, Perl, Javascript, PHP (ed altri) avrai probabilmente già presente il concetto di *array dinamico*. Sono array la cui dimensione è variabile, e aumenta o diminuisce in base alle necessità. In Go, come in altri linguaggi, gli array sono "fissi", nel senso che quando ne dichiariamo uno dobbiamo specificarne la dimensione. Una volta dichiarata, tale dimensione non può cambiare.

```go
var scores [10]int
scores[0] = 339
```

L'array qui in alto può contenere fino a 10 elementi, da `scores[0]` a `scores[9]`. Accedere ad un elemento oltre questo range significherà scatenare un errore in fase di compilazione (o runtime, in base al contesto).

Se vogliamo, possiamo inizializzare un array insieme ai suoi valori. Così:

```go
scores := [4]int{9001, 9333, 212, 33}
```

Per ottenere la lunghezza di un array possiamo usare la funzione `len`. Un'altra funzione, `range`, può essere invece usata per iterare tra i suoi elementi.

```go
for index, value := range scores {

}
```

Gli array fanno bene il lavoro lavoro... ma sono rigidi. Molto rigidi, come puoi vedere. Spesso, infatti, non sappiamo a priori quale sarà la dimensione di un insieme di elementi: abbiamo bisogno di un'altra struttura.

## Slice

In Go è piuttosto raro l'usare direttamente un array. Tendenzialmente si usano altre strutture che si chiamano "slice", molto leggere, il cui compito è rappresentare una "porzione" di array. Possiamo creare uno slice in vari modi: vediamoli.

```go
scores := []int{1,4,293,4,9}
```

Come puoi notare, in questo esempio non abbiamo dichiarato la dimensione della struttura tra le parentesi quadre. Per capire la differenza, scopriamo un altro modo di creare slice: la funzione `make`.

```go
scores := make([]int, 10)
```

Abbiamo usato `make` al posto di `new` perché creare uno slice non consiste soltanto nell'allocare memoria. Nello specifico, stiamo allocando l'array sottostante ed inizializzando lo slice che lo "conterrà". Qui in alto abbiamo appena dichiarato uno slice che ha una lunghezza pari a 10 ed una capacità pari a 10.

```go
scores := make([]int, 0, 10)
```

Qui, invece, abbiamo creato uno slice di lunghezza 0 ma con capacità pari a 10. Confuso, vero? Adesso capirai meglio con qualche esempio.

```go
func main() {
  scores := make([]int, 0, 10)
  scores[7] = 9033
  fmt.Println(scores)
}
```

Questo esempio qui sopra restituisce un errore. Perché? Semplice: il nostro slice ha una lunghezza pari a zero. Certo, l'array sottostante ha 10 elementi, tuttavia bisogna "espandere" il nostro slice per accedervi. Per espandere uno slice si può usare la funzione `append`.

```go
func main() {
  scores := make([]int, 0, 10)
  scores = append(scores, 5)
  fmt.Println(scores) // stampa [5]
}
```

Abbiamo "aumentato" la lunghezza dello slice fino a 5. Il codice dell'esempio precedente, tuttavia, porterebbe ugualmente ad un errore. Riproviamo così:

```go
func main() {
  scores := make([]int, 0, 10)
  scores = scores[0:8]
  scores[7] = 9033
  fmt.Println(scores)
}
```

Con l'istruzione `scores[0:8]` abbiamo ridimensionato ulteriormente la lunghezza dello slice. C'è un limite massimo a cui possiamo arrivare? Certo: è la capacità dell'array sottostante che, in questo caso, è pari a 10.

Beh, in realtà, più che *è* bisognerebbe dire *sarebbe*... già, perché `append` è speciale. Se l'array sottostante è pieno, si occupa autonomamente di creare un array più grande, copiare i valori e sistemare tutto autonomamente. Molto comodo! Facciamo subito una prova per capirne di più.

```go
func main() {
  scores := make([]int, 0, 5)
  c := cap(scores)
  fmt.Println(c)

  for i := 0; i < 25; i++ {
    // qui aumentiamo, con append, la dimensione del nostro array
    scores = append(scores, i)

    if cap(scores) != c {
      c = cap(scores)
      fmt.Println(c)
    }
  }
}
```

La capacità iniziale di `scores` era 5. Tuttavia, per arrivare a mantenere 25 valori dovrà essere ridimensionato tre volte: a 10, 20 e a 40.

Ecco un ultimo esempio:

```go
func main() {
  scores := make([]int, 5)
  scores = append(scores, 9332)
  fmt.Println(scores)
}
```

Qui, l'output sarà `[0, 0, 0, 0, 0, 9332]`. Cosa? Pensavi fosse `[9332, 0, 0, 0, 0]`? Beh, in realtà, se ci pensi, i primi cinque elementi dello slice hanno già un valore: quello di default, 0!

Riassumendo, ecco quali sono i quattro modi di inizializzare uno slice.

```go
names := []string{"leto", "jessica", "paul"}
checks := make([]bool, 10)
var names []string
scores := make([]int, 0, 20)
```

Quando usare quale? Il primo non ha bisogno di molte spiegazioni. Lo usi quando sai quali valori metterai nello slice. Il secondo è comodo quando devi andare a scrivere in punti specifici dello slice. Così:

```go
func extractPowers(saiyans []*Saiyans) []int {
  powers := make([]int, len(saiyans))
  for index, saiyan := range saiyans {
    powers[index] = saiyan.Power
  }
  return powers
}
```

Il terzo non è altro che uno slice "vuoto" e può essere usato insieme ad `append`, per aggiungere nuovi elementi quando necessario.

L'ultimo modo ci permette di specificare una capacità iniziale: utile se abbiamo un'idea di massima di quanti elementi avremo al suo interno.

Ricorda: anche se conosci la capacità, puoi sempre usare `append`. Alla fine è questione soprattutto di preferenza personale.

```go
func extractPowers(saiyans []*Saiyans) []int {
  powers := make([]int, 0, len(saiyans))
  for _, saiyan := range saiyans {
    powers = append(powers, saiyan.Power)
  }
  return powers
}
```

Gli slice, in Go, sono un concetto molto interessante e potente rispetto al classico array. Esiste anche in altri linguaggi: in JavaScript c'è il metodo `slice`, in Ruby puoi usare la sintassi `[START..END]`, in Python invece `[START:END]`. In questi linguaggi viene sempre creata una copia dell'array, che viene "affettata" e restituita. Ecco un esempio in Ruby:

```ruby
scores = [1,2,3,4,5]
slice = scores[2..4]
slice[0] = 999
puts scores
```

L'output? Chiaramente `[1, 2, 3, 4, 5]`. Perché `slice` è una copia. Ecco lo stesso esempio in Go.

```go
scores := []int{1,2,3,4,5}
slice := scores[2:4]
slice[0] = 999
fmt.Println(scores)
```

Stavolta l'output è `[1, 2, 999, 4, 5]`.

Cosa è cambiato? Facciamo un altro esempio, qualcosa di classico: vogliamo trovare il primo spazio in una stringa (perché lo slicing funziona anche sulle stringhe) dopo i primi cinque caratteri. Ecco come faremmo usando JavaScript:

```js
haystack = "the spice must flow";
console.log(haystack.indexOf(" ", 5));
```

In Go useremmo gli slice:

```go
strings.Index(haystack[5:], " ")
```

Come puoi notare dall'esempio, `[X:]` è una scorciatoia che sta per *da X alla fine*, mentre `[:X]` sta per *dall'inizio ad X*. Occhio però, perché Go non supporta indici negativi. Per prendere tutti gli elementi di uno slice tranne l'ultimo, ad esempio, dovremmo fare così:

```go
scores := []int{1, 2, 3, 4, 5}
scores = scores[:len(scores)-1]
```

Ecco un altro esempio: rimuovere un elemento da uno slice in corrispondenza di uno specifico indice.

```go
func main() {
  scores := []int{1, 2, 3, 4, 5}
  scores = removeAtIndex(scores, 2)
  fmt.Println(scores)
}

func removeAtIndex(source []int, index int) []int {
  lastIndex := len(source) - 1

  source[index], source[lastIndex] = source[lastIndex], source[index]
  return source[:lastIndex]
}
```

Prima di andare avanti, diamo un'occhiata ad un'altra funzione built-in di Go: `copy`. Questa funzione è ottima per capire come gli slice possono cambiare il modo in cui scriviamo codice in Go. Normalmente, un metodo che copia dei valori da un array ad un altro ha cinque parametri: li chiameremo `source`, `sourceStart`, `count`, `destination` e `destinationStart`. Con gli slice ne bastano due:

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

Se vuoi (anzi, te lo consiglio) prenditi del tempo e gioca con questo codice. Prova più varianti per capire bene il meccanismo che c'è sotto. Che succede se cambi la chiamata `copy` con qualcosa come `copy(worst[2:4], scores[:5])`? Sporcati le mani!

## Map

Le mappe in Go sono quelle cose che negli altri linguaggi vengono chiamate hashtable o dizionari. Lavorano esattamente come ti aspetti: definisci una chiave ed un valore per quella chiave, puoi prendere un valore partendo da una chiave, cambiarlo, cancellarlo.

Proprio come gli slice, le mappe possono essere create con `make`.

```go
func main() {
  lookup := make(map[string]int)
  lookup["goku"] = 9001
  power, exists := lookup["vegeta"]

  // stampa 0, false
  // (0 è il default per un intero)
  fmt.Println(power, exists)
}
```

Per ottenere il numero di chiavi presenti, usa `len`. Per rimuovere un valore partendo dalla sua chiave, usa `delete`.

```go
// ritorna 1
total := len(lookup)

// non ritorna nulla, può essere chiamato su una chiave non esistente
delete(lookup, "goku")
```

Le mappe crescono dinamicamente: se vogliamo però possiamo comunque assegnare una dimensione iniziale come secondo parametro di `make`.

```go
lookup := make(map[string]int, 100)
```

Come al solito, se hai un'idea di quante chiavi avrai, più o meno, il definire una dimensione iniziale può aiutare a livello di performance.

Puoi usare una mappa come campo di una struttura. Basta definirla così:

```go
type Saiyan struct {
  Name string
  Friends map[string]*Saiyan
}
```

... ed ecco come dare un amico a Goku!

```go
goku := &Saiyan{
  Name: "Goku",
  Friends: make(map[string]*Saiyan),
}
goku.Friends["krillin"] = ... // Krilin!
```

C'è anche un altro modo di dichiarare ed inizializzare dei valori in Go. Come quando usiamo `make`, questo metodo è specifico per mappe ed array. Possiamo dichiararlo come "composite literal":

```go
lookup := map[string]int{
  "goku": 9001,
  "gohan": 2044,
}
```

Iterare tra i valori di una mappa è semplice: basta usare il `for`, combinato con `range`.

```go
for key, value := range lookup {
  ...
}
```

L'iterazione in una mappa non è ordinata. Ogni iterazione ritornerà le coppie chiave/valore in un ordine casuale.

## Puntatori Vs. Valori

Abbiamo finito il secondo capitolo cercando di capire quando conviene usare un puntatore e quando una variabile. Perché non continuare la conversazione allargandola ad array e mappe?

Guarda queste due istruzioni:

```go
a := make([]Saiyan, 10)

// oppure ...

b := make([]*Saiyan, 10)
```

Molti sviluppatori pensano che passare `b` ad una funzione sia più efficiente. In realtà, quello che viene passato è una copia dello slice, che è già una reference. Di conseguenza, non c'è un'enorme differenza.

Quello che interessa lo vedrai nel momento in cui modificherai i valori dello slice o della mappa. Si applica la stessa identica logica che abbiamo visto nel secondo capitolo, che si può riassumere in: non importa molto quello che fai con l'array o la mappa in sè, l'unica cosa che può influenzare la tua decisione è cosa devi fare con i singoli valori.

## Prima di Proseguire

Gli array e le mappe in Go funzionano più o meno come negli altri linguaggi. Se sei abituato agli array dinamici dovrai adattarti ad un paio di piccole cose, vero, ma come hai visto `append` risolve molti dei tuoi problemi facilmente. Gli slice sono un ulteriore miglioramento del concetto.

Ci sono anche altri casi particolari, ma non è nel mio interesse coprirli per ora. Meglio fare qualcosa di interessante, qualcosa di più "pratico"... per cui proseguiamo!

# Capitolo 4 - Organizzazione del Codice ed Interfacce

In questo capitolo daremo uno sguardo a come organizzare il codice di un nostro progetto Go.

## Package

Abbiamo visto come eseguire e compilare dei programmi molto semplici. Le cose però cambiano in caso di progetti più complessi. In Go, i nomi dei package seguono la struttura delle directory nel workspace. Se non ricordi di cosa sto parlando, è la cartella il cui path corrisponde alla variabile d'ambiente `$GOPATH` (se hai bisogno, riguarda i capitoli precedenti, è un buon momento). Quindi, supponendo di lavorare ad un software dedicato ad un e-commerce, ci ritroveremo ad avere un package "shopping" il cui codice si trova in `$GOPATH/src/shopping`.

Ovviamente non possiamo tenere tutto in una sola cartella. Potremmo ad esempio avere una parte del software dedicata alla comunicazione con il database: creeremo una sottocartella `$GOPATH/src/shopping/db` ed il package sarà chiamato `db`. Per accederci da un altro package, quindi, dovremo "importare" `shopping/db`.

Insomma: con la parola chiave `package` definisci il package in cui ti trovi specificando una singola parola. Quando ne importi uno, invece, specifichi tutta la gerarchia.

Ti vedo confuso: non ti preoccupare, facciamo un bell'esempio pratico.

Vai nella cartella `src` del tuo workspace. Al suo interno, crea una cartella `shopping`, dopodiché una cartella `db` come sottocartella di `shopping` appena creata. Qui crea un file `db.go`.

Ecco il suo codice:

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

Il nome del package è esattamente quello della cartella in cui si trova il file. Come puoi vedere non stiamo accedendo davvero ad un database: sto solo facendo un esempio di organizzazione del codice che potrebbe tornarti utile.

Detto questo, torna nella cartella `shopping` e crea un nuovo file `pricecheck.go`. Ecco il suo contenuto:

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

Probabilmente starai pensando che importare `shopping/db` sia superfluo, perché siamo già in `shopping`. Non è così: in realtà stai importando `$GOPATH/src/shopping/db`. Potresti, infatti, ritrovarti a dover importare un altro package in un'altra cartella (ad esempio un package `altropackage/db`). In tal caso, `altropackage/db` corrisponderebbe a `$GOPATH/src/altropackage/db`.

Se stai costruendo un tuo package non hai bisogno d'altro oltre a quello che hai appena visto. Per costruire un eseguibile, invece, avrai bisogno anche di un `main`. Facciamolo subito: nella cartella `shopping` crea una cartella `main`, ed al suo interno un file `main.go`.

Eccone i contenuti:

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

Ci siamo! Prova ad eseguire il tutto, dalla cartella `shopping`, con un bel...

```
go run main/main.go
```

### Import Ciclici

Più diventerai bravo con Go, maggiore sarà la complessità dei software che scriverai. Prima o poi, te l'assicuro, ti ritroverai in quella situazione in cui un package A importa un package B ma il package B, a sua volta, ha bisogno di qualcosa del package A (direttamente o indirettamente, tramite un terzo package).

Una cosa del genere però non è consentita dal compilatore! Vediamo di scatenare volontariamente l'errore per capirne qualcosa di più.

Sposta la definizione di `Item` da `shopping/db/db.go` in `shopping/pricecheck.go`. Il file `pricecheck.go` adesso dovrebbe essere così:

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

Prova ad eseguire il codice: otterrai un paio di errori da `db/db.go` a proposito di `Item` che viene visto come non definito. Ha perfettamente senso: `Item` non esiste più nel package `db`; è stato spostato nel package shopping. Dobbiamo cambiare anche `shopping/db/db.go` così:

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

Prova ad eseguire il codice adesso: eccolo, l'errore *import cycle not allowed*! Come risolverla, una cosa del genere? Semplice: introduciamo un altro package che conterrà le nostre strutture "condivise".

La struttura delle cartelle adesso sarà così:

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

`pricecheck.go` importerà `shopping/db`, mentre `db.go` adesso importerà `shopping/models` invece di  `shopping`, rompendo il circolo vizioso. Abbiamo mosso `Item` in `shopping/models/item.go`, quindi dovremo modificare `shopping/db/db.go` in modo tale da fargli prendere `Item` dal package `models`:

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

Spesso ti troverai a condividere molto più di un semplice `model`. Un altro classico esempio sono le cartelle `utilities`. Organizzare il codice in questo modo rompe gli import ciclici e aiuta a tenere il codice più pulito.

Certo, dobbiamo ancora vedere le interfacce, che migliorano ancora di più le cose: non adesso però.

### Visibilità

Go usa una semplice regola per definire quali funzioni e quali tipi sono visibili al di fuori di un package. Se il nome della funzione o del tipo inizia per una lettera maiuscola, allora è visibile. Altrimenti rimane nello scope del package, ben nascosto.

La cosa si applica anche ai campi delle strutture. Se un campo inizia con una lettera maiuscola, allora solo il codice all'interno dello stesso package potrà accedervi.

Supponiamo, ad esempio, che un nostro file `items.go` abbia una funzione come questa di seguito.

```go
func NewItem() *Item {
  // ...
}
```

Potremmo richiamarla tranquillamente con `models.NewItem()`. Tuttavia, se la funzione si fosse chiamata `newItem`, richiamarla in quel modo, da un altro package, non sarebbe stato possibile!

Prova direttamente tu, per capire meglio! Cambia nomi ai campi, ai tipi, a tutto quello che vuoi per vedere come il codice e l'esecuzione cambiano!

### Gestione dei Package

Il comando `go` che abbiamo usato finora con `run` e `build` ha anche un altro "sottocomando": `get`, che si occupa di prendere librerie di terze parti per usarle nei nostri progetti. `go get` supporta vari protocolli: facciamo un semplice esempio che prende un package da Github. Occhio, perché avremo bisogno di Git installato in locale.

Torna alla shell/prompt e digita:

```
go get github.com/mattn/go-sqlite3
```

`go get` si occuperà di tirare giù la dipendenza e memorizzarla nel workspace. Guarda tu stesso, in `$GOPATH/src`! Vedrai una cartella `github.com` ed al suo interno una cartella `mattn`. Qui troverai il package, in una cartella `go-sqlite3`.

Abbiamo visto poco fa come si importa un package presente nel nostro workspace... e infatti ecco come portare nel nostro progetto il package appena scaricato:

```go
import (
  "github.com/mattn/go-sqlite3"
)
```

Sembra quasi un URL... ma non è così: in realtà è la struttura delle cartelle che abbiamo visto prima, visto che il package è in `$GOPATH/src/github.com/mattn/go-sqlite3`.

### Dependency Management

La bellezza di `go get` non finisce di certo qui. Una cosa molto interessante da sapere è che se esegui `go get` nella cartella di un progetto, questo scandirà ogni singolo file, cercherà tra gli import le librerie di terze parti e le scaricherà automaticamente.

Il nostro stesso codice diventa un `Gemfile`, o un `package.json`, per capirci.

Se invece esegui `go get -u` i vari package verranno aggiornati automaticamente. Se ne vuoi aggiornare uno in particolare allora usa `go get -u NOME_PACKAGE`.

Certo, c'è un bel problema con `go get` da tenere in considerazione: non c'è modo di specificare una revisione specifica di una libreria: punterà sempre a master/head/trunk/default. Un bel problema se dovessi aver bisogno, per due progetti diversi, di due versioni diverse della stessa libreria.

Per risolvere il problema puoi comunque usare un tool di management delle dipendenze di terze parti. Ce ne sono vari tra cui scegliere su [questa pagina della go-wiki](https://github.com/golang/go/wiki/PackageManagementTools).

Al momento, comunque, la community sta cercando di risolvere la cosa proponendo un tool standard, [dep](https://github.com/golang/dep).

## Interfacce

Le interfacce sono dei tipi che definiscono un contratto ma non un'implementazione. Una cosa del genere:

```go
type Logger interface {
  Log(message string)
}
```

Niente di assurdo: semplicemente questa interfaccia recita "se vuoi implementarmi devi specificare un metodo Log nella tua implementazione, con questa sintassi".

A cosa può servire una cosa del genere? Beh, le interfacce servono a disaccoppiare il tuo codice dalle implementazioni specifiche. Tenendoci sull'esempio dell'interfaccia `Logger`, infatti, potremmo avere:

```go
type SqlLogger struct { ... }
type ConsoleLogger struct { ... }
type FileLogger struct { ... }
```

Considera, inoltre, che usando le interfacce al posto dell'implementazione concreta puoi facilmente cambiare (e testare) l'implementazione sottostante senza impattare troppo sulla manutenibilità del codice. Un fattore da non sottovalutare.

Come usare un'interfaccia? Semplice: esattamente come qualsiasi altro tipo.

```go
type Server struct {
  logger Logger
}
```

Puoi usarla anche come parametro di una funzione!

```go
func process(logger Logger) {
  logger.Log("hello!")
}
```

In linguaggi come C# o Java bisogna esplicitare quando una classe implementa un'interfaccia:

```csharp
public class ConsoleLogger : Logger {
  public void Logger(message string) {
    Console.WriteLine(message)
  }
}
```

In Go questo avviene implicitamente. Se la tua struttura ha una funzione `Log` con un parametro `string` e nessun valore di ritorno... allora può essere usata come `Logger`. Può sembrare strano, ma questo approccio rende il codice meno verboso.

```go
type ConsoleLogger struct {}
func (l ConsoleLogger) Log(message string) {
  fmt.Println(message)
}
```

L'idea di fondo è (come avviene anche altrove) promuovere la creazione di piccole interfacce, tagliate per compiti specifici. La standard library di Go è piena di queste interfacce: basta pensare a `io`, package che ne contiene varie come `io.Reader`, `io.Writer` e così via.

Le interfacce possono inoltre partecipare nella composizione di un'altra struttura. Inoltre, le interfacce possono essere tranquillamente composte da altre interfacce. Ad esempio, `io.ReadCloser` è un'interfaccia composta da `io.Reader` ed `io.Closer`.

Infine, come già detto prima, le interfacce vengono usate anche per evitare gli import ciclici: se non passiamo un'implementazione (ma un'interfaccia), le dipendenze "dirette" (e quindi anche cicliche) sono sempre più limitate.

## Prima di Proseguire

In questo capitolo ti ho dato vari consigli su come strutturare il tuo codice. Sono tanti piccoli suggerimenti, è vero, ma con il tempo capirai meglio quale approccio usare. All'inizio ti sentirai come "limitato" in alcune scelte. Dopo i tuoi primi progetti più seri con Go inizierai a prenderci la mano, vedrai.

Il modo in cui Go gestisce la visibilità di tipi, funzioni e campi è abbastanza semplice ed efficace. E consistente.

Se già conosci il concetto di interfaccia, la sezione che ho dedicato a loro in questo capitolo non dovrebbe averti dato problemi. Se non ci hai mai lavorato, considera che potresti avere bisogno di tempo prima di prenderci la mano. Sono uno strumento potentissimo.

# Capitolo 5 - Pillole

In questo quinto capitolo seguiremo un ordine più "casuale", alla scoperta di tante altre piccole chicche di Go.

## Gestione degli Errori

In Go non vengono usate eccezioni. Il modo migliore di gestire gli errori è attraverso i valori di ritorno. Prendiamo una funzione già esistente, `strconv.Atoi`, che prende una stringa per convertirla in intero.

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

Se vuoi puoi creare un tuo errore, per adattarlo alle tue esigenze. L'unica cosa di cui devi essere assicurarti è di aderire al contratto dell'interfaccia `error`, questa qui di seguito:

```go
type error interface {
  Error() string
}
```

Possiamo anche creare i nostri errori importando il package `errors` ed usandone la funzione `New`.

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

C'è un pattern abbastanza diffuso nella standard library di Go riguardo l'uso di errori e variabili. Ad esempio, il package `io` ha una variabile `EOF` definita così:

```go
var EOF = errors.New("EOF")
```

Viene definita al di fuori di una funzione, è accessibile all'esterno (la prima lettera del nome `EOF` è maiuscola, dopotutto). Svariate funzioni ne fanno uso all'interno di questo package ed ovviamente possiamo usarla anche noi, come "consumatori" della libreria.

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

Un'ultima nota prima di proseguire: Go presenta due funzioni `panic` e `recover`. Per dirla brevemente, `panic` è simile al lancio di un'eccezione e `recover`, come puoi ben immaginare, è come un `catch`. Vengono usate, comunque, molto raramente.

## Defer

Come già detto in precedenza, Go ha un suo garbage collector che ci aiuta a tenere pulita la memoria. Tuttavia, alcune risorse richiedono un rilascio esplicito. Ad esempio, dobbiamo sempre richiamare il `Close()` sui file dopo averli usati. E si sa: è sempre un attimo scordarsi il `Close` e fare un casino. La soluzione di Go? La keyword `defer`:

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
  // leggi qui l file...
}
```

Ok, se provi ad eseguire questo codice sicuramente otterrai un errore (il file non esiste). Il punto è mostrarti come funziona `defer`. In poche parole, quello che segue `defer` verrà eseguito esattamente alla fine della funzione in cui è scritto. In questo esempio, `file.Close()` verrà eseguito esattamente dopo la fine di `main`. In questo modo ci occupiamo di aprire e chiudere un file "nello stesso punto", rendendo le cose più ordinate.

## go fmt

Molti dei programmi scritti in Go seguono le stesse regole di formattazione. Ad esempio, il tab viene usato per indentare, le parentesi graffe vanno sulla stessa linea dello statement e così via.

Lo so, tu probabilmente hai il tuo stile e vuoi continuarlo ad usare. Beh, è quello che ho fatto anche io ma sono sincero: felicissimo di averlo abbandonato. Il motivo? Il comando `go fmt`. Semplicissimo da usare, una volta lanciato "pulisce" il tuo progetto rimettendo in riga tutto il tuo codice, sistemando la formattazione, ordinando gli import e così via.

Basta un...

```
go fmt ./...
```

Provalo!

## If "Inizializzati"

Ecco un'altra chicca interessante: Go supporta quello che si può definire un "if modificato", in cui il valore può essere inizializzato appena prima di essere valutato:

```go
if x := 10; count > x {
  ...
}
```

Ok, questo qui sopra è abbastanza stupido. Ecco, guarda questo:

```go
if err := process(); err != nil {
  return err
}
```

Simpatico, vero?

## Interfacce Vuote e Conversioni

Nella maggior parte dei linguaggi orientati agli oggetti c'è tendenzialmente una classe, spesso chiamata `object`, che fa da "superclasse" per tutte le altre. Go non possiede il concetto di ereditarietà e non ha questa superclasse. Ha tuttavia un'interfaccia vuota, senza metodi. Interessante, se pensi che:

* ogni tipo implementa tutti i... 0 metodi dell'interfaccia vuota;
* le interfacce vengono implementate implicitamente;

... ogni tipo in Go rispetta effettivamente questa interfaccia vuota!

Se volessi, potresti scrivere una cosa del genere:

```go
func add(a interface{}, b interface{}) interface{} {
  ...
}
```

... per creare una "somma" di due elementi di qualsiasi tipo. Certo, poi dovresti implementarla. Per convertire una "variabile interfaccia" in un tipo specifico, usa `.(TYPE)` così:

```go
return a.(int) + b.(int)
```

Occhio, perché se il tipo sottostante non dovesse essere `int` alla fine ne verrà fuori un errore.

Se ti interessa, c'è anche un "type switch" da usare in queste occasioni:

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

Vero, non è codice pulitissimo e convertire i valori in questo modo può essere pericoloso: è bene comunque conoscere questa possibilità.

## Stringhe e Array di Byte

Le stringhe e gli array di byte sono molto simili. Possiamo infatti convertirne uno nell'altro facilmente:

```go
stra := "the spice must flow"
byts := []byte(stra)
strb := string(byts)
```

Questo modo di convertire le variabili è abbastanza comune anche nel contesto degli altri tipi. Alcune funzioni, ad esempio, si aspettano un `int32` o un `int64`. Potresti ritrovarti a fare una cosa del genere:

```go
int64(count)
```

Ricorda comunque che usando `[]byte(X)` o `string(X)` stai creando una copia del dato. Le stringhe, infatti, sono sempre immutabili.

Le stringhe sono fatte di `runes` (rune), punti unicode. Il che significa che calcolando la lunghezza di alcune stringhe non otterrai un risultato "giusto". Un esempio:

    fmt.Println(len("椒"))

Iterando su una stringa usando `range` otterrai queste rune, non dei byte.

## Tipi di Funzione

Le funzioni sono un tipo first-class.

```go
type Add func(a int, b int) int
```

puoi usare questo tipo ovunque, per un campo o come parametro, o come valore di ritorno.

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

Usare le funzioni in questo modo ti aiuta a disaccopiare il codice dalle specifiche implementazioni, un po' come facciamo già con le interfacce.

## Prima di Proseguire

Abbiamo dato uno sguardo ai vari aspetti dello sviluppo in Go. In questo capitolo abbiamo visto come vengono gestiti gli errori (ad alcuni questo modo non piace, sappilo), come rilasciare una certa risorsa nel modo più adeguato e tante altre piccole chicche.

Una cosa è certa: non abbiamo visto tutto quello che Go può offrirci. Tuttavia, con questa prima infarinatura dovremmo essere capaci di gestire al meglio la maggior parte delle situazioni.

Manca soltanto una cosa, a questo punto...

# Capitolo 6 - Concorrenza

Go viene spesso descritto come un linguaggio concurrent-friendly, cioè orientato alla concorrenza. Il motivo è presto spiegato: offre una sintassi davvero molto semplice per risolvere questo tipo di problema. In questo capitolo esploreremo i due meccanismi chiave: goroutine e channel.

## Le Goroutine

Una goroutine è simile ad un thread, con la differenza di essere schedulato da Go e non dal sistema operativo. Il codice che viene eseguito in una goroutine può essere seguito in parallelo con altro codice. Vediamo un esempio:

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

Ok, qui ci sono un paio di cose interessanti da conoscere, ma concentriamoci sulla più importante: come avviare una goroutine. La keyword da usare è `go`, seguita dalla funzione che vogliamo eseguire. Nulla ci vieta di usare una funzione anonima al posto del codice qui in alto, sia chiaro. Ecco, qualcosa del genere:

```go
go func() {
  fmt.Println("processing")
}()
```

Le Goroutine sono semplici da creare, come vedi, ed hanno un piccolissimo overhead. Di base, più goroutine potranno essere eseguite sullo stesso thread del sistema operativo. Il threading model a cui si fa riferimento viene descritto come il M:N, nel senso che abbiamo M thread dell'applicazione che girano su N thread del sistema operativo.

Il rapporto non è quindi 1:1. Il risultato è che su un hardware decente è possibile far girare, contemporaneamente, milioni di goroutine!

Inoltre, tutta la complessità del mapping e scheduling delle goroutine è nascosta allo sviluppatore. Noi diciamo semplicemente "ok, questo codice dovrebbe essere eseguito in modo asincrono" e Go si occupa del resto.

Adesso torniamo per un secondo al nostro esempio: ti starai chiedendo perché mai abbiamo usato lo `Sleep` per fermare l'applicazione. Domanda legittima: la verità è che omettendo l'istruzione il processo principale termina prima dell'esecuzione della goroutine! Certo, nel lavoro di tutti i giorni non è qualcosa che si può fare: scopriamo come coordinare il nostro codice e fare le cose per bene!

## Sincronizzazione

Creare una goroutine, come abbiamo visto, è roba da poco. Così facili che è un attimo arrivare a crearne quante a bizzeffe. Tuttavia, il codice concorrente va coordinato. Ed ecco che arriviamo, così, al secondo strumento che ci viene messo a disposizione da Go: i channel. Prima di guardare i channel da vicino, però, vediamo un po' di cose sulle basi della programmazione concorrente.

Scrivere codice concorrente richiede attenzione. Nello specifico, tanta attenzione su dove e come leggi (e scrivi). In un certo senso è come sviluppare senza un garbage collector: devi pensare ai tuoi dati da una diversa angolazione, stando attenti ai vari pericoli che ci si possono parare davanti.

Facciamo un esempio:

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

Rispondi: quale pensi sarà l'output di questo codice?

Se stai per dirmi `1, 2, 3, 4 ... 20` reggiti forte: hai sia ragione che torto! Mi spiego: è assolutamente che vero che, di tanto in tanto, eseguendo questo codice otterrai quel risultato, in sequenza. Tuttavia, la realtà è diversa: il comportamento di questo codice è indefinito perché abbiamo più goroutine che vengono eseguite contemporaneamente. Che scrivono tutte nella variabile `counter`. Una di queste goroutine potrebbe leggerne il valore mentre un'altra ci scrive sopra.

Fidati se ti dico che è una cosa decisamente pericolosa. Quel `counter++`, piccolo ed indifeso, una volta compilato viene spezzato in tante istruzioni assembly e... la natura della loro esecuzione, di conseguenza, cambia in base alla piattaforma su cui vengono eseguite. I numeri quindi verranno stampati in un'ordine strano, a volte alcuni di questi numeri mancheranno, altre volte li vedrai duplicati. Per assurdo, la stessa applicazione potrebbe crashare.

L'unica cosa "concorrente" che puoi fare in tutta sicurezza è leggere quella variabile. Puoi avere tutti i lettori di questo mondo lì, appesi, ma qualsiasi scrittura deve essere sincronizzata. Ci sono vari modi di raggiungere l'obiettivo: il più comune di tutti è l'uso di un mutex:

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

Un mutex non fa altro he serializzare gli accessi al codice sotto lock. Abbiamo definito il nostro lock con `lock sync.Mutex`. Di default il valore di `sync.Mutex` è "unlocked", sbloccato.

Sembra semplice, vero? Lo è, anche se l'esempio che hai appena visto, devo ammetterlo, è ingannevole. C'è infatti tutta una serie di bug che si possono presentare quando si parla di programmazione concorrente. In primis perché non è sempre così ovvio capire quale codice si vuole "proteggere": può sembrare comodo usare un lock che copre un bel po' di codice, ma non è la cosa migliore da fare. Anche perché rischiamo di fare un progetto per un'autostrada a dieci corsie e finire comunque con una stradina a corsia singola.

Un altro problema riguarda i deadlock. Con un singolo lock il problema non si pone, ma cosa succede se si "accavallano" più lock insieme? Devi sapere che è straordinariamente semplice trovarsi nella situazione in cui la goroutine A effettua un lock A ma ha bisogno di accedere all'elemento sotto un lock B, mentre una goroutine B sta bloccando del codice tramite il lock B che a sua volta ha bisogno di accesso al lock A. Una cosa del genere è difficile da capire, figuriamoci da debuggare.

Volendo, possiamo creare un deadlock con un solo lock... basta scordarsi di sbloccarlo a fine esecuzione! Guarda qui:

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

La programmazione concorrente non è comunque così semplice. C'è tanto da conoscere e da sapere, l'argomento è davvero ampio. Ad esempio, c'è un altro tipo di mutex chiamato "read-write mutex". Permette di gestire un lock per la scrittura ed uno per la lettura. Questa distinzione ti permette, volendo, di avere più lettori contemporaneamente mentre i vari "scrittori" devono mettersi in fila. Oltre alle funzioni `Lock` ed `Unlock` già viste ce ne sono altre due: `RLock` ed `RUnlock`, dove `R` sta per *Read*, ovviamente.

La programmazione concorrente però non consiste solo nel serializzare gli accessi alle scritture e via. C'è anche, come dicevamo prima, la parte di coordinazione delle goroutine. Lo so che forse ci speravi, ma mettere in sleep il processo per dieci millisecondi non è la soluzione migliore (soprattutto la più elegante).

Ricorda che per situazioni molto semplici i mutex sono una soluzione più che sufficiente. Esistono, usali! Per situazioni più complesse, invece... è arrivato il momento di scoprire i `channel` e capire a cosa servono.

## Channel

Quando si parla di programmazione concorrente, la vera sfida è una sola: la condivisione dei dati. Se le tue goroutine non condividono dati, non hai bisogno di sicnronizzarle e coordinarle. Non è, però, una scelta che puoi fare sempre. In realtà la maggior parte dei sistemi esistenti viene costruita con questo specifico obiettivo: condividere dati nel contesto di più richieste, contemporaneamente. Un ottimo esempio è un sistema di cache in-memory, o magari un database.

In Go, i channel si occupano di rendere più semplice la programmazione concorrente portando i dati "al di fuori" del quadro generale. Immagina i channel come un canale di comunicazione tra diverse goroutine, che così facendo possono passarsi dei dati. Il risultato? In un qualsiasi momento dell'esecuzione del nostro codice, solo una goroutine ha accesso effettivamente al dato.

Un channel, come qualsiasi altra cosa, ha un tipo. Viene incluso anche il tipo di dato che passeremo nel canale. Ad esempio, per creare un channel che dovrà "passare" un intero, scriveremo:

```go
c := make(chan int)
```

Questo channel è di tipo `chan int`. Per passarlo ad una funzione, la sintassi è:

```go
func worker(c chan int) { ... }
```

Come puoi immaginare, i channel supportano due operazioni: l'invio...

```
CHANNEL <- DATO
```

... e la ricezione.

```
VAR := <-CHANNEL
```

La freccia, come puoi notare, punta nella direzione in cui il dato procede.

Un'ultima cosa prima di buttarci nel primo esempio pratico: ricevere ed inviare ad un canale è un'operazione bloccante. Quando riceviamo da un canale, l'esecuzione della goroutine non continua fin quando il dato non è disponibile. Allo stesso modo funziona l'invio: se il dato non viene ricevuto, l'esecuzione non prosegue.

Consideriamo ora un sistema con dei dati in ingresso che vogliamo gestire in goroutine separate: una necessità abbastanza comune. Eseguire tutto su una singola goroutine significherebbe mandare in timeout i client e non è quello che vogliamo. Per prima cosa, quindi, scriveremo il nostro worker. Una semplice funzione che renderò parte di una struttura.

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

Il nostro worker, come vedi, è semplice. Aspetta che un certo dato sia disponibile, quindi lo "processa". Come vedi, l'operazione viene ripetuta all'infinito: significa che appena ci saranno dati disponibili questi verranno processati.

Ci siamo: creiamo ed avviamo alcuni worker.

```go
c := make(chan int)
for i := 0; i < 5; i++ {
  worker := &Worker{id: i}
  go worker.process(c)
}
```

Dopodiché... beh, diamo loro del lavoro da fare.

```go
for {
  c <- rand.Int()
  time.Sleep(time.Millisecond * 50)
}
```

Ecco qui di seguito il codice completo.

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

Non sappiamo quale worker si prenderà un certo dato. Quello che sappiamo (e che Go garantisce) è che il dato mandato ad un channel verrà ricevuto da un singolo ricevitore. Non di più. Se ci fai caso, l'unico "stato" effettivamente condiviso è il channel, che può ricevere e mandare in modo concorrente senza problemi.

### Buffered Channel

Nell'esempio visto poco fa, davamo "in pasto" al nostro channel un intero ogni cinquanta millisecondi. Tutto regolare, ma... se arrivassero più dati di quanti possano essere gestiti? Facciamo un esperimento, cambiando il codice del worker come segue:

```go
for {
  data := <-c
  fmt.Printf("worker %d got %d\n", w.id, data)
  time.Sleep(time.Millisecond * 500)
}
```

Piano piano, i dati vengono rimandati indietro, al channel. Non c'è più nessun ricevitore disponibile!

Serve una soluzione: ce ne sono varie e quella più popolare è creare un buffer per questi dati.

Se nessun worker è disponibile, memorizziamo i dati in arrivo in una specie di "coda". In Go, i channel hanno questa capacità di default: non dobbiamo fare altro che specificare la lunghezza di questa coda come segue.

```go
c := make(chan int, 100)
```

Facendo questa modifica inizierai a risolvere il problema. Tuttavia, l'esecuzione non è comunque ottimale. I buffered channel non aggiungono una maggiore capacità: creano soltanto un "cuscinetto" per ammortizzare dei picchi particolarmente fastidiosi. Il nostro esempio funziona, invece, in maniera diversa: mettiamo continuamente dati nel channel, troppi per i nostri worker.

Prova a modificare come segue il codice del ciclo:

```go
for {
  c <- rand.Int()
  fmt.Println(len(c))
  time.Sleep(time.Millisecond * 50)
}
```

Noterai tu stesso che, dopo un'accelerazione iniziale, i dati inizieranno ad essere rimessi puntualmente nel channel.

### Select

Insomma, anche con il buffering prima o poi la coda si riempie, ed inizierai a scartare messaggi. Non possiamo mettere a disposizione una quantità infinita di memoria per gestire ogni situazione! In nostro soccorso ci viene in aiuto il `select`.

A livello sintattico, il `select` assomiglia molto ad uno switch. Permette di specificare del codice da eseguire quando il channel non è disponibile.

Per prima cosa, però, rimuoviamo il buffering dal nostro channel, in modo tale da avere un esempio più pulito.

```go
c := make(chan int)
```

Bene: ora cambiamo il loop `for` visto prima.

```go
for {
  select {
  case c <- rand.Int():
    // codice opzionale
  default:
    // questa parte può essere lasciata vuota
    // se si vuole scartare "silenziosamente" il dato
    fmt.Println("dropped")
  }
  time.Sleep(time.Millisecond * 50)
}
```

Facendo un rapido calcolo, la situazione è la seguente: inseriamo nel channel 20 messaggi al secondo. I nostri worker ne possono gestire 10 al secondo. La metà dei messaggi viene quindi scartata.

L'esecuzione ora è più fluida, ma il problema rimane. Chiaramente questo è solo un assaggio di quello che puoi fare con `select`: il suo scopo è soprattutto gestire più di un canale per volta. Ad esempio, con `select` potremmo specificare più `case` con più canali. Se nessuno di questi canali è disponibile, allora viene eseguito il codice in `default`.

### Timeout

Un'altra possibilità, se si vuole scongiurare il problema del lock, è adottare un timeout. In questo modo il blocco è tale soltanto per un certo periodo di tempo e non all'infinito.

Per specificare un timeout possiamo usare la funzione `time.After`. Vediamone un uso pratico riprendendo il nostro esempio.

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

La funzione `time.After` ritorna un channel. Possiamo quindi inserirlo come case nella `select`. Il canale in questione accetta un'altra scrittura solo dopo i 100 millisecondi. Per capirci meglio, ecco come potrebbe apparire un'implementazione di `After`:

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

Ok, torniamo alla `select` adesso. Ci sono ancora un paio di cose che vale la pena farti notare, prima di concludere.

Innanzitutto, cosa succede se non specifichiamo un `default`? Prova tu stesso: ricorda che il `default` serve a chiarire cosa fare se non ci sono channel disponibili.

Inoltre, `time.After` ritorna un channel di tipo `chan time.Time`. Nell'esempio qui sopra scartiamo il valore che è stato mandato ma... se volessimo riceverlo?

```go
case t := <-time.After(time.Millisecond * 100):
  fmt.Println("timed out at", t)
```

Attenzione quindi alle nostre `select`. Fai caso al fatto che si, stiamo inviando a `c` ma stiamo ricevendo da `time.After`. Volendo fare un piccolo riassunto, ecco come funziona una `select`:

* viene scelto il primo channel disponibile;
* se più di un channel è disponibile, allora viene scelto casualmente;
* se non ci sono channel disponibili, il caso `default` viene scelto;
* se non c'è un `default`, la `select` diventa bloccante;

Sappi che è abbastanza comune vedere una `select` dentro un `for`.

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

## Prima di Proseguire

Se sei nuovo al mondo della programmazione concorrente, tutto questo ti sembrerà "troppo". Non temere, è normale: è un argomento che richiede pratica, studio e cura. Go, nel suo piccolo, cerca di renderlo più digeribile.

Le goroutine cercano di astrarre tutto quello che serve per eseguire del codice concorrente, mentre i channel aiutano ad eliminare alcuni bug fastidiosi che possono sbucare quando abbiamo bisogno di condividere dei dati tra più goroutine. Chiaramente, usare questi strumenti non eliminerà tutti i possibili bug: non succede mai. Ricordatelo. Aiuta, però, pensare al cambio di approccio: dal "codice pericoloso" ad un insieme di messaggi che vengono mandati da una goroutine all'altra.

Detto questo, non scordiamoci che le primitive come quelle presenti nel package `sync` (come il Mutex) non sono il male. A volte ti serviranno e ne farai buon uso. Ne sono certo.

# Conclusioni

Recentemente ho sentito descrivere Go come un linguaggio *noioso*. Noioso perché tutto sommato semplice da imparare, da scrivere e, soprattutto, da leggere. Se però ci fai caso, ho usato tre capitoli per spiegare i tipi, come funzionano, come dichiarare le variabili e tutto il resto.

Se vieni dai linguaggi a tipizzazione statica non credo tu abbia avuto problemi. Per te sarà stato, al massimo, una rinfrescata di alcuni concetti che già conoscevi. Puntatori, slice e così via.

Se invece vieni dal mondo dei linguaggi dinamici, probabilmente in questo piccolo libro di cose da imparare ne hai viste abbastanza. Senza contare tutta la parte relativa alla sintassi per l'inizializzazione e dichiarazione. Comprendere le cose fondamentali, come l'allocazione della memoria, è importantissimo.

Oltre questo però Go ci aiuta ad organizzare, in modo semplice, il nostro codice. Attraverso le interfacce, la gestione degli errori come valori di ritorno e quel `defer` per la gestione delle risorse.

Infine, non scordiamoci il supporto built-in per la concorrenza. Ci sono le goroutine, essenziali ma che fanno bene il loro lavoro. Poi abbiamo i channel, più complessi. Senza contare le basi, come il mutex visto in precedenza. A tal proposito, trovo sia fondamentale conoscere le basi prima di arrivare ai wrapper di alto livello. Una volta imparate ad usare bene tutte queste strutture, tutte queste astrazioni, capisci che sono a tutti gli effetti il fondamento per qualcosa di diverso. Lo dico perché cambiano, in un certo senso, il modo in cui scrivi e pensi al tuo codice quando fai programmazione concorrente. E visto e considerato quanto possa essere difficile la programmazione concorrente... beh, non è poi così male no?
