---
layout: post
img: https://jekyllrb.com/img/logo-2x.png
---
E' estremamente semplice scrivere un articolo. Solo il primo paragrafo comparirà nella pagina news come sintesi.
<!-- more -->


# Il titolo dell'articolo ha la riga che inizia con l'hashtag


	---
	layout: post 		serve per applicare il giusto template quindi lasciarlo così
	membro: Thomas Bertani	Il membro o ditta associata o autrice dell'articolo
	ruolo: Membro Fondatore	Ruolo dell'associato. "membro AssoB.it" è sufficiente
	img: /img/thomas.jpg 	Immagine che accompagna l'articolo
	---

## Questo è un titolo di secondo livello (corrisponde a un h2 in html)

> Questa è una citazione

guardate come viene.

*Questo testo è in corsivo*

**Questo testo è in grassetto.**

**Questa è una frase in grassetto con una parola in _corsivo_ in mezzo.**


Questa é una lista non ordinata:

* elemento uno
* elemento due

Questa é una tabella:

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell

Questa é un'altra tabella.

| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

Si può anche allineare a destra o sinistra

| Left-Aligned  | Center Aligned  | Right Aligned |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |


Questo è codice:

```
print(hello world!)
```

Jekyll offre anche un supporto potente per il codice snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Date un'occhiata a [Jekyll docs][jekyll] per ottenere informazioni su come avere il massimo da jekyll e sopratutto usate questo paragrafo per vedere come sono fatti i collegamenti ipertestuali.
File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
