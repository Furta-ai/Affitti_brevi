# Progetto: Analisi degli affitti brevi Airbnb a Venezia (SSADA)

Questo è il repository contenente il mio progetto per il corso di Strumenti per l'Analisi dei Dati Aziendali (SSADA) dell'Università di Padova (A.A. 2025/2026).

L'idea alla base del lavoro è quella di esplorare e capire come funziona il mercato di Airbnb a Venezia. Ho fatto diverse analisi per cercare di estrarre informazioni utili sia descrivendo quello che c'è oggi, sia provando a fare delle previsioni.

## Cosa c'è nel progetto?

Ho diviso il lavoro in diverse aree di analisi:

1. **Analisi Descrittive e Mappe:** Ho iniziato guardando la distribuzione degli annunci. Quanti sono? Dove si concentrano di più? Quanto costano in media? Ho anche creato delle mappe interattive (usando il pacchetto Leaflet in R) per far vedere graficamente la densità degli appartamenti e la loro posizione nel comune di Venezia.
2. **Modellazione Predittiva:** Qui ho cercato di prevedere il prezzo notturno di un Airbnb in base alle sue caratteristiche (numero di stanze, posizione, recensioni, ecc.). Ho usato diversi algoritmi di machine learning come Random Forest, Gradient Boosting (GBM), e modelli additivi generalizzati (GAM), per poi confrontarli e vedere quale performa meglio.
3. **Analisi di Diffusione:** Ho studiato come è cresciuto il numero degli host nel tempo. Usando i modelli di Bass e Prophet ho provato a modellare la curva di adozione di Airbnb a Venezia da quando è nato fino ad oggi.
4. **Regole Associative (Market Basket Analysis):** Sfruttando le "amenities" (i servizi offerti: Wi-Fi, aria condizionata, piscina, ecc.), ho usato le regole associative per capire quali servizi vengono offerti spesso insieme e cosa distingue un annuncio di lusso da uno base.
5. **Analisi Testuale:** Ho guardato le recensioni scritte dagli utenti per fare un po' di text mining e capire quali sono gli aspetti più discussi e se ci sono lamentele ricorrenti.

## Struttura delle cartelle

Tutto il codice principale è scritto in R e si trova in script `.Rmd` o `.R`. 

- **Analisi/**: Qui dentro ci sono tutti i file `.Rmd` divisi per argomento (Descrittive, Modellazione, Diffusione, Mappe, Regole Associative). C'è anche uno script Python (`scraping_airbnb.py`) che ho usato per fare un po' di web scraping per i prezzi in periodo di Mostra del Cinema al Lido.
- **Modelli/**: In questa cartella vengono salvati i risultati dei modelli per non doverli riaddestrare ogni volta.
- **dati/**: Contiene i dataset. I dati di partenza li ho presi principalmente da *Inside Airbnb*, ma li ho integrati con dati di *AirROI* e altre fonti (tipo confini amministrativi e capacità ricettiva del Comune).

## Nota sui dati pesanti

Ho caricato tutto il necessario per rendere le analisi riproducibili fin da subito, ma **i file di grosse dimensioni (sopra i 50MB) non sono stati inclusi** per via dei limiti di GitHub. Nello specifico:
- Manca `reviews.csv` (che pesa quasi 300MB). Se vi serve far girare l'analisi testuale, potete scaricarlo direttamente dalla pagina di Inside Airbnb per Venezia (snapshot di settembre 2024) e metterlo nella cartella `dati/`.
- Mancano i file `.rds` dei modelli più pesanti (tipo Random Forest o MERF). Se lanciate il file `Modellazione.Rmd`, R li ricalcolerà da zero e li salverà in automatico sul vostro PC.

## Come eseguire il codice

Se volete riprodurre il progetto sul vostro computer:
1. Aprite il file `Progetto-SSADA-Airbnb.Rproj` con RStudio. In questo modo i percorsi di tutti i file saranno impostati correttamente in automatico.
2. Prima di lanciare le analisi vere e proprie, eseguite gli script `Pulizia.R` e `pulizia_airroi.R` (nella cartella `Analisi/`) per ottenere i dataset puliti pronti per i modelli.
3. Dopo di che, aprite il file `.Rmd` che vi interessa e usate il tasto *Knit* per generare il report (in PDF o HTML).

Assicuratevi di aver installato i pacchetti necessari per R. Ne ho usati diversi, tra cui: `tidyverse`, `sf`, `leaflet`, `randomForestSRC`, `gbm`, `prophet`, `lme4` e `arules`.
