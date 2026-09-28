---
marp: true
theme: gaia
paginate: false
html: true
style: |
  pre {
    font-size: 0.7em;
  }
  section {
    print-color-adjust: exact;
    -webkit-print-color-adjust: exact;
  }
  h1, h2,h3, h4 {
    text-align: center;
  }
  section.two-columns {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }
  section.two-columns h1, h2, h3, p {
    grid-column: span 2;
  }
  section.two-columns pre {
    margin: 0;
  }
  section.centered-image img {
    display: block;
    margin: 0 auto;
  }
  .red { color: red; }
  img { display: block; margin: 0 auto; }
---
<!-- _class: lead -->
# Boterham met jam(stack)
### static websites op GitHub met Hugo
<!-- 
Waar gaat dit over: hosting van een plain 
html website op Github, en site generatie met Hugo dmv een Github workflow on demand,
getriggerd door git push.
Dit is 1 voorbeeld, je kunt kiezen voor andere
hosting, andere generator, enz. 
Verder zullen we kijken naar form handling. Ook 
hier 1 alternatief van vele.
Opzet berust op 3 pijlers: Hugo, Git, en Github: pages en actions. Over elk valt heel veel te vertellen maar daar is niet genoeg tijd voor.
Presentatie geeft een vogelvlucht van de onderwerpen!
-->

---
## Wie ben ik
* semi gepensioneerd software engineer
* contributor [ksml.io](https://ksml.io) (in dienst)

* [github.com/tonvanbart](github.com/tonvanbart)

---
## Website hosting (vaak)
* Veelal Wordpress
* Bekend platform: groot ecosysteem
  (plugins, themes)
* Hosting moet PHP en MySQL ondersteunen
  meer "attack surface": bijhouden!
* Pagina's worden "on demand" gegenereerd


<!--
In veel gevallen: Wordpress. Niets mis mee, algemeen bekend, plugins, themes, ecosysteem.
Er zijn consequensties: LAMP stack, hosting moet MySQL en PHP hebben.
Onderhoud noodzakelijk (hacking!) hosting is duurder, of zelf doen.
Self hosting: idem, hou je thuisnetwerk veilig.
Omdat pagina's "on the fly" worden gegenereerd kan de site trager aanvoelen en zwaarder zijn voor de server.
-->

---
## Alternatief: statische websites
* "plain" HTML
* hosting kan goedkoop of gratis
* snel (geen on demand page generatie)
* minimaal attack surface

<!-- 
Statische websites zijn een goedkoop alterntief. Consequentie: hand coded HTML? 
Niemand heeft zin om dat met de hand bij te houden 
(styling, templating enz)
Bv. aanpassing nav menu is veel handmatig werk 
op iedere pagina.
-->

---
## Statische website generator
* Content tekst (markdown) plus templates
* Jekyll (Ruby), Pelican (Python), Eleventy (node), <span class="red">Hugo</span> (Go)...

![width:800px](./out/markdown/markdown.svg)

<!--
Een statische website generator kan zorgen voor uniforme 
layout, styling enz.
Content wordt geschreven in versimpelde markup (Markdown), 
de generator zorgt er voor dat de nodige pagina's (opnieuw)
worden gegenereerd.
Waarom Hugo? Simpele install (1 executable), Golang templating die ik al een beetje kende.
Site bouw is snel (maakt voor mijn kleine site niet uit)
-->

---
<!-- _class: two-columns -->
## Markdown
<!--
* lichtgewicht markup
* human readable, machine translatable
* zie [markdown.org](https://markdown.org)
-->
Lichtgewicht markup; human readable, machine translatable
Zie [markdown.org](https://markdown.org)

```html
<h1>header level 1</h1>
<h2>level 2</h2>
<p>Paragraph tekst</p>
<p>Tweede paragraph</p>
<a href="http://www.example.com">hyperlink</a>
```

```markdown
# header level 1
## level 2
Paragraph tekst

Tweede paragraph
[hyperlink](http://www.example.com)
```
<!-- 
Markdown is een lichtgewicht manier om formatting toe te 
voegen aan plain text.
Gebruikt in bijv. Wikipedia, GitHub README en deze presentatie (Marp)!
-->
---
## Markdown: front matter
Metadata waar de generator iets mee kan:
```markdown
---
title: "Project kicked off"
date: 2026-08-01
summary: "The hugo-demo project is up and running."
---

We've started this demo project to show how easy it is to host a Hugo site
on GitHub Pages, deployed via GitHub Actions.
```
<!-- 
Frontmatter bevat metadata: gegevens over de pagina. Een site generator kan hier iets mee
b.v. de post op een blogpagina voorzien van een datum.
-->
---
## Git
Git is: versiebeheer voor code; 
"Wie heeft wat wanneer gedaan, en waarom?"

* `git init`: breng deze folder onder versiebeheer
* `git add`: voeg deze file/wijziging toe aan de administratie
* `git commit`: leg deze wijziging(en) definitief vast

```shell
> git commit -m 'blogpost over nllgg toegevoegd'
```
<!-- 
Git in 2 minuten: hou de historie bij van een reeks van files in een directory (en subdirs).
Git slaat de diff op, met de datum, gebruikersnaam en commit message.
-->

---
## Git remotes
Meerdere versies van een Git repo, op verschillende machines.
Hiermee kunnen ontwikkelaars samen werken aan een repo

* `git remote add {NAAM} {URL}`: voeg de remote op url {URL} toe als {NAAM}
* `git push {NAAM}`: stuur de hele historie naar de remote
* `git pull {NAAM}`: haal de historie op uit de remote

---
## Github
Centrale plek om een remote op te slaan; gratis voor OSS.
Naast een Git remote biedt Github extra voorzieningen: project wiki, <span class="red">CI/CD workflows</span>, issue tracking, <span class="red">project websites</span>, en meer.
<p>

```shell
git remote add origin git@github.com:ownernaam/reponaam.git
```

---
## Het plan
![width:550px](./out/workflow/workflow.svg)

