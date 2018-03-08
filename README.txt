TEMA 2
Gorgovan Alina-Valentina 314CB

Fisiere: main.c functii.c struct.h

_struct.h_

Acest fisier cuprinde mai intai definitiile structurilor, macrodefinitii pentru accesul maiusor la diferite campuri si anteturile functiilor din functii.c.
Prima structura, TCelula, descrie o celula din lista simplu inlantuita generica.
Pentru stiva am scris structura TStiva, care cuprinde dimensiunea unui element in stiva si are tipul size_t d si adresa varfului stivei care este un pointer la inceputul unei liste generice simplu inlantuite.
Pentru coada am scris structura TCoada, care cuprinde dimensiunea unui element din coada si doua adrese de tipul TLista care pointeaza catre inceputul listei simplu inlantuite si catre sfarsitul acesteia.
Structura TParanteza reprezinta tipul elementelor cu care am lucrat si are doua campuri: id-ul parantezei si tipul acesteia.
Macrodefinitiile usureaza accesul campurilor din structuri.

_main.c_

Fisierul include doar functia main in care sunt apelate celelalte functii din fisierul functii.c. Dupa initializare variabilelor, stivelor si cozilor, se intra intr-o bucla si in functie de numele operatiei citit in variabila op_name se citesc si restul variabilelorutile pentru apelul functiei respective. Dupa urmeaza apelul functiei.
La sfarsit se apeleaza functiile de dealocare de memorie si se eliberereaza pointerii folositi.

_functii.c_

AlocCelula
Functia primeste ca argumente un informtia si aloca spatiu de dimensiunea d intr-o celula de tipul TCelula*. Functia returneaza celula alocata.

AlocStiva
Functia aloca memorie pentru o structura de tipul TStiva*, testeaza daca s-a alocat si initiaza campul dime cu d, primit ca parametru, si varful stivei devine NULL.

AlocCoada
Functia aloca memorie pentru o strutura de tipul TCoada*, testeaza alocarea si initiaza campurile din structura, inceputul si sfarsitul cozii cu NULL si dimensiunea dime cu d

InitS 
Functia InitS aloca memorie pentru un vectori de structuri de tip TStiva cu n elemente.
Mai intai genereaza vectorul de adrese de structuri TStiva si dupa aloca fiecare stiva s[i] cu ajutorul functiei AlocStiva. Functia returneza vectorul de structuri de tip void**.

InitC
Functia InitC aloca memorie pentru un vectori de structuri de tip TCoada cu n elemente. Asemenea functiei InitS, se aloca fiecare structura din vector cu functia AlocCoada. Functia returneza vectorul de structuri de tip void**.

Push
Functia Push introduce in stiva s primita ca argument elementul ae primit ca argument.
Mai intai aloca o celula cu ajutorul AlocCelula si dupa realizeaza o inserare la inceput de lista. Se leaga noua celula de lista si se muta Varful stivei pe noua celula. Functia returneaza 1 daca s-a inserat cu succes in stiva si 0 daca nu s-a putut realiza inserarea.

Pop
Functia Pop extrage elementul din varful stivei si il returneaza.
Mai intai initializez un auxiliar cu valoarea varfului stivei, copiez informatia din varful stivei in elementul ae, mut varful stivei, eliberez memorie si dupa returnez elementul extras.

intrq
Functia introduce in coada c primita ca parametru elementul ae.
Mai intai se aloca o celula cu informatia ae, dupa se leaga noua celula de restul cozii.
Daca coada este vida atunci si sfarsitul cozii si inceputul cozii devin noua celula, iar daca coada este nevida se leaga celula de sfarsit si avanseaza sfarsitul. Functia returneaza 1 daca s-a inserat cu succes in coada si 0 daca nu s-a putut realiza inserarea.

extrq
Functia extrq extrage primul element introdus in coada. 
Se copiaza mai intai la adresa ae informatia de la inceputul cozii, avanseaza inceputul si se returneaza elementul extras.

AfiParanteza
Functia scrie tipul dintr-o structura TParanteza primita ca parametru in fisierul de output.

prints
Functia printeaza vectorul de structuri de tip TStiva*.
Mai intai aloc o stiva auxiliara d si un element p pentru a realiza extragerile.
Primul pas este de a rasturna fiecare stiva s[i] din vector pentru a putea fi printata de la baza la varf. Rasturnarea se face dand pop din stiva s[i] si push in d.
Mai departe se extrag pe rand elementele din d, se afiseaza cu ajutorul functiei 
AfiParanteza si se introduc in stiva initiala s[i].

printq
Functia printeaza vectorul de structuri de tip TCoada*.
Mai intai aloc o stiva auxiliara d si un element p pentru a realiza extragerile.
La primul pas se extrag din coada elementele, se afiseaza si se introduc in coada
auxiliara. Urmeaza ca elementele sa fie extrase din coada auxiliara si reintroduse in cea initiala.

perechi
Pentru a realiza functiile corrects si correctq am implementat aceasta functie care compara daca doua elemente de tipul TParanteza sunt perechi.

corrects si correctq
Observatie:Nu e implementata destul de corect, cele doua teste picate nu merg doar din cauza acestor doua functii care nu merg doar pe un singur caz si pe care nu am reusit sa le optimizez astfel incat sa mearga pe toate cazurile.

Mai intai am initiat niste variabile carora in functie de valoarea pe care o aveau continuam sa adun numarul de paranteze sau ma opream. M-am gandit sa schimb id-urile si sa fi in ordine crescatoare astfel incat sa imi dau seama de pozitia unei paranteze in stiva. De exemplu daca citesc o paranteza inchisacare nu are pereche desi ar trebui sa se opreasca si sa reia de la 0 adunarea nu se intampla asa.
In principiu functia extrage un element din stiva, daca este o paranteza inchisa il introduce intr-o stiva auxiliara. Daca elementul este o paranteza deschisa si stiva auxiliara este goala atunci se trece mai departe.
Daca stiva auxiliara nu este goala atunci cu ajutorul functiei perechi vede daca cele doua parantezese potrivesc. Daca se potrivesc se aduna la variabila l 2 si se compara cu maximul. Daca se citeste o paranteza deschisa ce nu este pereche cu cea di varful stivei  se reinitializeaza variabilele si se goleste stiva auxiliara.
Se repeta pana la sfarsitul stivei.

Daca insa ramane ceva in stiva auxiliara se calculeaza lungimea de la ultimul element extras pana la cel din stiva si lungimea de la cel din stiva la primul element extras si se returneaza maximul dintre aceste  valori.

sorts
Functia sorteaza o coada primita ca parametru.
Se extrage un element din stiva, se introduce intr-o stiva auxiliara daca aceasta este goala.
Daca nu este goala, cat timp elementul extras este mai mare decat cel din varful stivei auxiliare atunci se extrage elementul din varful stivei auxiliare si se reintroduce in stiva initiala.
Astfel in stiva auxiliara se vor afla elementele in ordine descrescatoare iar dupa rasturnare in stiva initiala
acestea vor fi in ordine crescatoare.

sortq
Algoritmul merge pe acelasi principiu ca cel de la sorts.


_Observatie_ : Functiile corrects si correctq nu merg pe un singur caz si de aceea imi pica pe checker testele 7 si 8. Toate celelalte functii merg ok si nu am nici pierderi de memorie.

