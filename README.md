# Priručka git

## Inštalácia

### Windows

### Mac

### Linux

## Popis priestorov v git

| Working directory    | Staging area          | Local repository       | Remote repository |
| -------------------- | --------------------- | ---------------------- | ----------------- |
| git init             |                       |                        |                   |
| git add _files_ ---> |                       |                        |                   |
|                      | git commit -m "" ---> |                        |                   |
|                      |                       | git push _branch_ ---> |                   |

### Working directory

### Staging area

### Local repository

### Remote repository

## Konfigurácia

```bash
git config --global user.name "Užívateľské meno pre git"
git config --global user.email "email používaný pre git"
```

## Inicializácia projektu

```bash
mkdir git-learning
cd git-learning
touch index.html
```

Následne inicalizujeme vytvorený adresár pre git

```bash
git init
```

Toto vytvorí `.git` adresár vo vnútri projektu. Adresár s našim projektom a podadresárom `.git` budeme odteraz volať **Working directory**

```bash
git status
```

## Pridanie súboru do staging area

mali by sme vidieť súbor index.html ako "Untracked files", čo znamená, že git vie, že tento súbor bol pridaný ale git ho ešte neeviduje. To napravíme cez príkaz

```bash
git add index.html
```

Ak chceme pridať viacero súborov (napr. sme ich vytvorili 5 a nechceme všekty pridávať ručne), môžeme tak učiniť cez príkaz

```bash
git add .
```

Ak chceme filtrovať, ktoré súbory chceme pridať do novej verzie, môžeme použiť tzv. wildcards. Napr. sme v projekte vytvorili 15 obrázkov a chceme do novej verzie pridať iba práve tieto obrázky ale nechceme ukladať zmeny v iných súboroch. Môžeme tak učiniť cez

```bash
git add *.png
```

V prípade, že sme pridali súbor, ktorý nechceme nakoniec v novej verzii projektu, môžeme ho odobrať zo "staged" stavu cez príkaz

```bash
git restore --staged index.html
```

```bash
git restore --staged .
```

čo zapríčiní, že sa vrátime do stavu ako keby sme nič nepridávali do zmien (na lokálnom disku v projekte sa nič nezmení).
Následne môžeme vytvoriť novú verziu projektu pomocou

```bash
git commit -m "vytvorili sme index.html"
```

`-m` Pridá komentár ku zmene

`-m` Druhé `-m` pridá širši popis zmeny

_Príklad_

```bash
git commit -m "Pridanie funkcie pre vyhľadávanie zamestnancov" -m "Vytvorenie funkcie smartSearch() v súbore utils/search.js a následná implementácia v súbore index.html"
```

Ak napr. chceme rovno commitnúť zmeny bez toho aby sme muselí písať git add,je možné tak urobiť pomocou skráteného zápisu

```bash
git add -am "Vytvorili sme index.html"
```

Toto znamená, že pridá všetky zmenené súbory do novej verzie projektu a vytvorí commit s komentárom.
Toto však funguje iba pre súbory ktoré git už eviduje. To znamená, že ak vytvoríme nový súbor napr. "app.js", musíme ho najskôr pridať cez git add.
Stav všetkých verzií aj s komentármi si môžeme pozrieť cez

```
git log
```

V prípade, že projekt vetvíme a chceme k tomu aj graf, ktorý je schopný vygenerovať konzola, môžeme si log okrášliť napr. pomocou

```
git log --graph --decorate --abbrev-commit --all
```

V prípade, že chceme vypísať commity na jeden riadok, môžeme si výstup naformátovať pomocou

```bash
git log --pretty=oneline
```

Zmeny oproti lokálnej verzii v porovnaní s git môžeme vypísať pomocou  
_Červená (znak "-") značí riadok ktorý zmizol v lokálnej verzii a zelená (znak "+") znamená pridanie._

```bash
git diff
```

Môže sa stať, že nejaký súbor sme lokálne uložili ale zistili sme, že je v ňom napr. chyba a chceme sa vrátiť k verzii súboru, ktorá je ako posledná na git-e. Môžeme použiť

```bash
git checkout -- index.html
```

Stratíme však zmeny zmeny v danom súbore ktoré sme mali na uložené na disku a budú nahradené tou verziou, ktorá je ako posledná v gite.

Pomocou git checkout môžeme aj skákať medzi verziami niektorého súboru. Ako vidno na obrázkoch vyššie, každá verzia má so sebou nejaký "hash", ktorý slúži ako jedinečný identifikátor pre danú verziu. Hash je dlhý ako je vidno na obrázku kde sme vypisovali všetky zmeny na jeden riadok, stačí však skopírovať prvých 6 znakov čo je vidieť na obrázku vyššie kde je formátovaný výstup s vetvením (tam je použitý na výpis krátky hash).

Ak sa teda chceme vrátiť ku konkrétnej verzii projektu, stačí napísať

```bash
git checkout a872877
```

pričom "a872877" je práve unikátny hash pre verziu ku ktorej sa chceme vrátiť.

> Pozor, toto vráti celý projekt a všetky zmeny na lokálnom disku sa stratia. Platí to aj pre nové súbory, t.j. ak sa vo verzii ku ktorej sa vraciame taký súbor nie je, súbor sa z lokálneho disku vymaže.

V prípade, že sa chceme dostať naspať na poslednú verziu, môžeme tak učiniť pomocou

```bash
git checkout master
```

## Práca s GitHub

> Štandartne sa volá hlavná vetva (branch) `master`. Avšak v súčasnosti ju GitHub na počet žiadostí užívateľov už premenoval na `main`. To znamená, že v nových projekto sa môže volať `main` ako v príklade nižšie ale môže to byť aj `master`. Aká vetva je tá hlavna Vám napovie sám GitHub po založení projektu

### Vytvorenie nového projektu a zápis na GitHub

```bash
echo "# git-learning" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:zrebec/git-learning.git
git push -u origin main
```

### Pridanie existujúceho projektu s local repository na GitHub

```bash
git remote add origin git@github.com:zrebec/git-learning.git
git branch -M main
git push -u origin main
```
