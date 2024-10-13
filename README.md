# Predikce uzavření termínovaného vkladu

**TODO: před každým commitem jupyternootebooku dát clear all output, aby se nemusely dělat pull requesty**

 Seminární práce vychází z datasetu: [Bank Marketing Data Set - Kaggle](https://www.kaggle.com/datasets/alexkataev/bank-marketing-data-set) Cílem je pomocí 20 proměnných zjistit, zda klient banky (Portuguese banking institution) po marketingové kampani uzavřel termínovaný vklad či nikoliv. Cílovou proměnnou je "y" která má dvě hodnoty: "yes" (klient uzavřel termínovaný vklad) a "no" (klient neuzavřel).

## DATA 
Zdroj datasetu: https://archive.ics.uci.edu/ml/datasets/bank+marketing

Data se týkají přímých marketingových kampaní portugalské banky (Portuguese banking institution). Marketingové kampaně byly realizovány přes telefonní hovory. V několika případěch bylo nutné uskutečnit kontakt s klientem vícekrát, pro zjistění, zda došlo k otevření a často bylo třeba provést více než jeden kontakt se stejným klientem, aby bylo možné zjistit, zda byl termínovaný vklad sjednán. 

### Proměnné
Datový soubor obsahuje 20 proměnných: 
- 10 numerických 
- 10 kategorických 
  
a jednu cílovou proměnnou "y", která určuje, zda klient sjednal termínovaný vklad a dosahuje hodnoty "yes" (termínovaný vklad sjednán) a "no" (termínovaný vklad nebyl sjednán).

### Popis proměnných:
**Numerické proměnné**
- **1 - Age:** Věk klienta v letech.
- **2 - Balance:** Zůstatek na účtu klienta (v eurech).
- **3 - Day:** Den v měsíci, kdy byl poslední kontakt s klientem.
- **4 - Duration:** Délka posledního telefonického kontaktu (v sekundách).
- **5 - Campaign:** Počet kontaktů s klientem během aktuální marketingové kampaně.
- **6 - Pdays:** Počet dní od posledního kontaktu (999 znamená, že klient byl nikdy předtím nekontaktován).
- **7 - Previous:** Počet kontaktů s klientem před aktuální kampaní.
- **8 - Emp.var.rate:** Míra zaměstnanecké variability v posledním čtvrtletí (v procentech).
-**9 - Cons.price.idx:** Index cen spotřebitelů (v posledním měsíci).
- **10 - Cons.conf.idx:** Index důvěry spotřebitelů (v posledním měsíci).

**Kategorické proměnné**
- **11 - Job:** Typ zaměstnání klienta (např. zaměstnanec, důchodce, podnikatel atd.).
- **12 - Marital:** Rodinný stav klienta (např. svobodný, ženatý, rozvedený).
- **13 - Education:** Vzdělání klienta (např. základní, střední, vysokoškolské).
- **14 - Default:** Zda má klient úvěrové selhání (ano/ne).
- **15 - Housing:** Zda má klient hypotéku (ano/ne).
- **16 - Loan:** Zda má klient osobní půjčku (ano/ne).
- **17 - Contact:** Způsob kontaktu (např. mobilní, pevná linka).
- **18 - Month:** Měsíc posledního kontaktu (např. leden, únor atd.).
- **19 - Weekday:** Den v týdnu posledního kontaktu (např. pondělí, úterý).
- **20 - Poutcome:** Výsledek předchozí marketingové kampaně (např. úspěšná, neúspěšná, žádná).

**Cílová proměnná**
- **y (Subscription)**:  Binární proměnná indikující, zda klient podepsal termínovaný vklad (ano/ne).