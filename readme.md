# Maskininlärning/AI-projekt: Fake news identifier

## Problem: Identifiera fake news

I dagens samhälle har spridningen av falska nyheter (fake news) blivit ett allt större problem, särskilt genom digitala medier. Detta leder till att människor blir vilseledda, vilket påverkar beslut på både individuell och samhällsnivå. Målet med detta projekt är att utveckla en maskininlärningsmodell för att identifiera falska nyheter baserat på artiklarnas textinnehåll.

## Målsättning

Målet med projektet är att skapa en klassificeringsmodell som kan skilja mellan sanna och falska nyhetsartiklar. För att uppnå detta kommer jag:

1. Samla in data: Använda ett dataset som innehåller både falska och sanna nyheter.
2. Utföra dataförberedelse: Rensa, bearbeta och förstå data.
3. Skapa och utvärdera modeller: Träna olika maskininlärningsmodeller och jämföra deras prestanda.
4. Implementera en slutgiltig modell: Implementera och optimera den bästa modellen.

## Dataset

För detta projekt kommer jag att använda datasetet "Fake News Detection" från Kaggle. Det innehåller artiklar från olika källor, märkta som antingen sanna eller falska.

#### Datasetets egenskaper:

* Antal rader: 20,800+
* Kolumner:
    * `id`: Unikt identifieringsnummer för artikeln
    * `title`: Titel på artikeln
    * `author`: Författare till artikeln
    * `text`: Själva artikeln
    * `label`: Klassifikation av artikeln (0 = sann, 1 = falsk)

#### Typ av problem

Detta är ett klassificeringsproblem där målet är att förutsäga `label` baserat på artikelns innehåll. Datasetet är märkt (labeled), vilket innebär att jag kan använda övervakad maskininlärning (supervised learning).


## Tekniska Krav
Projektet är utvecklat i Python och använder flera bibliotek för datahantering och maskininlärning:

* Pandas: För datahantering och manipulation.
* Scikit-learn: För att skapa och utvärdera maskininlärningsmodeller.
* NLTK: För textbearbetning och språkanalytiska funktioner.
* TfidfVectorizer: För att omvandla text till en lämplig feature representation.
* Jupyter Notebook

## Modellbeskrivning
I projektet används en Random Forest Classifier för att identifiera falska nyheter. Random Forest är en ensembleinlärningsmetod som fungerar genom att konstruera flera beslutsträd vid träningstiden och utger den klass som är modalvärdet av klasserna (klassificering) av de enskilda träden.

#### Varför Random Forest?

* Robusthet mot överanpassning: Till skillnad från enkla beslutsträd tenderar Random Forest att undvika överanpassning till träningsdata, vilket gör det mycket effektivt för praktiska tillämpningar.
* Hantering av stora datamängder: Modellen kan hantera stora datamängder med hög dimension utan betydande prestandaförlust, vilket är idealiskt för textdata som ofta innehåller många unika ord.
* Funktionens betydelse: Random Forest kan också ge insikt i vilka funktioner (ord eller fraser i vårt fall) som är mest betydelsefulla för att skilja mellan falska och sanna nyheter.

#### Modellparametrar
Modellen har konfigurerats med följande parametrar:

* n_estimators: 100 - Antalet träd i skogen. Flertal träd kan öka precisionen men också beräkningstiden.
* max_depth: Ingen - Träden tillåts expandera utan begränsning, kontrollerad av min_samples_split.
* min_samples_split: 2 - Det minsta antalet prover som krävs för att dela en intern nod.

#### Träning av modellen
Modellen tränas med hjälp av följande dataframställning:

* Förbehandling av textdata: Textdata måste först renas och vektoriseras. Detta inkluderar att ta bort oväsentliga tecken, användning av TF-IDF för att omvandla text till en lämplig feature representation.
* Inlärningsprocess: Användningen av fit-metoden för att träna modellen på de förberedda träningsdatan.

#### Utvärdering
Modellens prestanda utvärderas genom att använda valideringsdata, där vi mäter noggrannhet, precision, recall och F1-score. En konfusionsmatris används också för att ge en tydlig bild av modellens prestanda över olika klasser.