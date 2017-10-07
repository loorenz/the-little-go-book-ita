## Sul Libro ##
[The Little Go Book](http://openmymind.net/The-Little-Go-Book/) è un libro, gratuito, che introduce al linguaggio Go.

Questo libro è stato scritto da [Karl Seguin](http://openmymind.net), già autore di:

* [Scaling Viki](http://openmymind.net/scaling-viki/)
* [The Little Redis Book](http://openmymind.net/2012/1/23/The-Little-Redis-Book/)
* [The Little MongoDB Book](http://openmymind.net/2011/3/28/The-Little-MongoDB-Book/)
* [Foundations of Programming](http://openmymind.net/FoundationsOfProgramming.pdf)

## Licenza ##
Questo libro è distribuito sotto la licenza  [Attribution-NonCommercial-ShareAlike 4.0 International](<http://creativecommons.org/licenses/by-nc-sa/4.0/>).

## Traduzioni ##

* [Spagnolo](https://github.com/raulexposito/the-little-go-book/tree/master/es) di Raúl Expósito
* [Cinese](https://github.com/songleo/the-little-go-book_ZH_CN) di Songleo
* [Cinese Tradizionale](https://github.com/kevingo/the-little-go-book) di KevinGo
* [Vietnamita](https://github.com/quangnh89/the-little-go-book/blob/master/vi/readme.md) di Quang Nguyễn
* [Italiano](https://github.com/francescomalatesta/the-little-go-book) di Francesco Malatesta

## Formati ##
Questo libro è stato scritto in [Markdown](http://daringfireball.net/projects/markdown/) e convertito in PDF usando [Pandoc](http://johnmacfarlane.net/pandoc/).

Il TeX template fa uso del [Lena Herrmann's JavaScript highlighter](http://lenaherrmann.net/2010/05/20/javascript-syntax-highlighting-in-the-latex-listings-package).

Il formato Kindle ed ePub è ottenuto sempre grazie a [Pandoc](http://johnmacfarlane.net/pandoc/).

## Come Generare il Libro ##
I package qui di seguito sono per Ubuntu. Se usi altri sistemi operativi, comunque, la procedura non dovrebbe essere così diversa.

### PDF

#### Requisiti

Package:

* `pandoc`
* `texlive-xetex`
* `texlive-latex-extra`
* `texlive-latex-recommended`

Avrai bisogno di [alcuni font](https://github.com/karlseguin/the-little-redis-book/blob/master/common/pdf-template.tex#L11).

Se vuoi, sentiti libero di cambiarli, ma conta che potrebbero [causare qualche problema](https://github.com/karlseguin/the-little-redis-book/issues/26).

#### Generare il Libro

Esegui `make it/go.pdf`.

### ePub

#### Dipendenze

Package:

* `pandoc`

#### Generare il Libro

Run `make it/go.epub`.

### Mobi

#### Dipendenze

Packages:

* `pandoc`

Avrai bisogno di [KindleGen](http://www.amazon.com/gp/feature.html?ie=UTF8&docId=1000765211) installato sulla tua macchina.

#### Generare il Libro

Run `make it/go.mobi`.

## Immagine di Copertina ##
In questo repository troverai anche il PSD dell'immagine della copertina del libro. Il font usato è [Comfortaa](http://www.dafont.com/comfortaa.font).
