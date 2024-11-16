# Predikce uzavření termínovaného vkladu
 Seminární práce vychází z datasetu: [Bank Marketing Data Set - Kaggle](https://www.kaggle.com/datasets/alexkataev/bank-marketing-data-set) Cílem je pomocí 20 proměnných zjistit, zda klient banky (Portuguese banking institution) po marketingové kampani uzavřel termínovaný vklad či nikoliv. Cílovou proměnnou je "y" která má dvě hodnoty: "yes" (klient uzavřel termínovaný vklad) a "no" (klient neuzavřel).

## DATA 
Zdroj datasetu: https://archive.ics.uci.edu/ml/datasets/bank+marketing

Data se týkají přímých marketingových kampaní portugalské banky (Portuguese banking institution). Marketingové kampaně byly realizovány přes telefonní hovory. V několika případěch bylo nutné uskutečnit kontakt s klientem vícekrát, pro zjistění, zda došlo k otevření termínovaného vkladu a často bylo třeba provést více než jeden kontakt se stejným klientem, aby bylo možné zjistit, zda byl termínovaný vklad sjednán. 

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


## PŘEDZPRACOVÁNÍ DAT
- Označení chybějícíh hodnot: Chybějící hodnoty 'unknown' nahrazeny hodnotami NA
- Vytvoření nové proměnné 'age_group', který vzniká rozdělením sloupce 'age' do intervalů
- Vytvoření nové proměnné 'year'
- Vytvoření nových intervalů pro proměnné "previous" a "campaign"
- Odstranění nepotřebných sloupců: "pdays", "duration", "nr.employed","poutcome","contact", "age"
- Standardizace numerických sloupců: 'emp.var.rate', 'cons.price.idx', 'cons.conf.idx', 'euribor3m'
- Vytvoření kopie předzpracovaného datasetu a uložení jako data_cleaned.csv
- Oddělení atributů - features a cílové proměnné - targer
- Vytvoření proměnných feature_cols a odstranění cílové proměnné 'y', aby zůstaly pouze proměnné, které se budou používat jako vstupy do modelu
- Rozdělení dat na testovací a trénovací v poměru 20/80
- Ošetření chybějících hodnot. Chybějící hodnoty označené NA jsme nahradili módem
- Převod proměnných typu object nebo category na číselné hodnoty 0 = no, 1 = yes a kategorizace
- Převedení y_train a y_test pro binární hodnoty
- Vyrovnání tříd pomocí over_sampler

## MODELOVÁNÍ
V této části jsme trénovaly tři různé modely: 
- Logistickou regresi, 
- Rozhodovací strom, 
- Random forest. 
  
Pro každý model jsme použily manuální nastavení i křížovou validaci, abychom ověřily, který model poskytuje nejlepší výsledky.

1. **Logistická regrese:** Model byl trénován s maximálním počtem iterací 10 000 a také jsme využily křížovou validaci s těmito parametry: cv = 5 a Cs= 1.
2. **Rozhodovací strom:** Tento model byl trénován s hloubkou stromu 3. Po optimalizaci hyperparametrů jsme získali nejlepší model pomocí GridSearchCV s těmito parametry: max_depth= 4 a min_samples_leaf=4. V obou případech jsme rozkodovací stromy vizualizovaly. 
3. **Random forest:** Vytvořily jsme model s 100 estimátory a maximální hloubkou stromů 5. Po ladění hyperparametrů pomocí GridSearchCv jsme získaly nejlepší model s těmito parametry: max_depth= 5, min_samples_leaf=2.

## LADĚNÍ HYPERPARAMETRŮ
Hyperparametry byly laděny zejména u modelů Rozhodovacího stromu a Random forest pomocí GridSearchCV. Model logisticé regrese jsme provedly znovu s křížovou validací.

U **rozhodovacího stromu** jsme ladily parametry jako max_depth, min_samples_leaf, a criterion. Nejlepším modelem byl strom s hloubkou 4, kritériem entropy a min_samples_leaf=4.

U **Random forest** jsme ladily parametry jako criterion, max_depth, a min_samples_leaf. Nejlepším modelem byl ten s kritériem entropy, hloubkou 5 a min_samples_leaf=2.

## EVALUACE MODELŮ
Evaluace byla provedena na základě klíčových metrik, jako je přesnost, precision, recall a F1-score, a dále jsme vše hodnotily na základě matice záměn a logistickou regresi i na zkladě ROC křivky.

- **Logistická regrese** Obě verze modelu vykazují podobné výsledky,  dosahují celkové přesnosti 73, 74 % a jsou konzistentní napříč foldy. Dobře předpovídají, že klient neuzavře termínovaný vklad (precision 95 %). U třídy 1 - uzavření vkladu mají modely nízkou precision a mají i vysokou míru falešných pozitiv.
  - ROC křivka ukázala, že oba modely překonávají náhodný klasifikátor, přičemž manuálně nastavená logistická regrese mírně překonala model optimalizovaný křížovou validací.
- **Rozhodovací strom** a strom s laděnými hyperparametry dosáhly téměř totožných výsledků. Přesnost modelů byla 82, 83 % a správně identifikují 59% klientů, kteří uzavřou vklad.
- **Random forest** stejně jako předchozí model má stejné výsledky v případě manuálně laděného modelu a v případě modelu s laděnymi hyperparametry. Přesnost modelů je 82 % a správně identifikují 60 % zákazníků, kteří uzavřou vklad.