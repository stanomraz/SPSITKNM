
# Efektový DSP Multipedal pre Gitaru (Filip Rechtorík)
- **Názov projektu**: Efektový DSP Multipedal pre Gitaru
- **Meno riešiteľa**: Filip Rechtorík

---

## Dôvod a okolnosti zavedenia riešenia
Klasický gitarový pedalboard so samostatnými efektovými pedálmi prináša viacero praktických nevýhod — zložitú kabeláž, potrebu vlastného napájania pre každý pedál a nutnosť počas vystúpenia opakovane sa skláňať a prepínať jednotlivé efekty nohou. Cieľom projektu je tieto nevýhody odstrániť spojením viacerých efektov do jedného DSP pedála, ktorý zároveň umožňuje meniť ich parametre na diaľku — priamo z gitary alebo z telefónu. Hráč tak získa väčšie pohodlie a rýchlejší prístup k nastaveniam počas hrania, bez zbytočného fyzického zaťaženia.

---

## Slovné zadanie, popis projektu od zákazníka
Pedál využíva viacero známych gitarových efektov — Wah, Pitch Shift a tretí efekt (výber zatiaľ nie je finálny) — spolu s noise gate, čím dosahuje takmer profesionálnu úroveň spracovania zvuku. Spracovanie zvuku zabezpečuje DSP (Digital Signal Processing) realizované pomocou Daisy Seed. Pedál sa ovláda otočnými potenciometrami a footswitchmi na výber efektu a úpravu jeho intenzity — tieto možnosti však nie sú obmedzené len na fyzický pedál, ale je možné ich ovládať aj na diaľku. Práve to je hlavnou inováciou tohto projektu.

---

## Zoznam modulov projektu a ich významných atribútov

1. **Fyzický pedál

- Atribúty: stav footswitchov (aktívny efekt), poloha potenciometrov/expression pedálu
- Unikátna identifikácia objektov: pedal.id

2. **Guitar Mounted Remote

- Atribúty: typ pripojenia (Bluetooth), stav pripojenia, stav ovládacích prvkov (gombíky)
- Unikátna identifikácia objektov: guitarRemote.id

3. **Webová aplikácia (UI)

- Atribúty: vybraný profil nástroja, aktuálne zobrazené hodnoty parametrov
- Unikátna identifikácia objektov: webapp.id

4. **DSP / efektový modul

- Atribúty: aktívny efekt, hodnoty parametrov efektu, stav noise gate
- Unikátna identifikácia objektov: effect.id

5. **Profily nástrojov

- Atribúty: názov profilu (typ gitary/basy), predvolené hodnoty parametrov pre daný profil
- Unikátna identifikácia objektov: profile.id

---

## Systémové požiadavky FURPS
1. **Funkčnosť (Functionality - F)**
   - Možnosť zobraziť pamäť závad
   - Čítanie meraných hodnôt z ECU
   - Testovanie aktuátorov a resetovanie parametrov

2. **Vhodnosť k použitiu (Usability - U)**
   - Užívateľsky prívetivý rozhranie
   - Intuitívne ovládanie pre profesionálov aj laikov

3. **Spoľahlivosť (Reliability - R)**
   - Nízka miera zlyhaní, konzistentná diagnostika
   - Obnovenie systému v prípade zlyhania

4. **Výkon (Performance - P)**
   - Rýchla diagnostika s nízkou spotrebou zdrojov

5. **Schopnosť údržby (Supportability - S)**
   - Jednoduché aktualizácie a testovanie systému
   - Podpora pre nové modely vozidiel

---

## Kritické situácie
1. **Systémové**
   - Výpadok napájania: Systém nie je schopný vykonať diagnostiku bez napájania.
   - Zlyhanie hardware: Poškodenie senzorov alebo ECU vedie k nepresnej diagnostike.

2. **Aplikačné**
   - Problémy s komunikáciou medzi diagnostickým zariadením a OBD-II portom vozidla.

---

## Tri situácie definujúce hranice systému
1. **Ideálny scenár**
   - Systém úspešne vykoná diagnostiku, zobrazuje chybové kódy a poskytuje potrebné informácie pre opravu vozidla.

2. **Hranične riešiteľný scenár**
   - Systém nedokáže identifikovať konkrétnu závadu, ale poskytne návrh na ďalšiu diagnostiku.

3. **Situácie, ktoré systém nezvládne**
   - Systém nie je schopný vykonať diagnostiku v prípade úplného zlyhania ECU alebo riadiacej jednotky.

---

## Kontext prostredia
Systém bude implementovaný ako samostatné riešenie, ktoré nebude závislé od existujúcich systémov. Bude musieť zohľadňovať rôzne environmentálne faktory, ako je teplota, vlhkosť a typ terénu, ktoré môžu ovplyvniť diagnostiku.

---

## Charakteristika aktérov a prostredia
- **Aktéri**: Mechanik, technik, výrobca automobilov, majiteľ vozidla
- **Prostredie**: Auto servis, mobilné zariadenia, diagnostické nástroje

---

## Use Case diagram
- **Minimálne 5 modulov a 2 aktéry**
- Doporučené maximum: 5 modulov s využitím `include` a `extend` vzťahov.

---

## Scenáre - konkrétna implementácia Use Case

**1. Vyhľadávanie kódového chybového hlásenia**  
   - **Názov**: Vyhľadanie chybového kódu P0300  
   - **Kontext**: Mechanik chce diagnostikovať problém s motorom vozidla.  
   - **Level zanoření Use Case**: Hlavný scénar  
   - **Aktéri**: Mechanik  
   - **Stakeholdeři a zájmové osoby**: Mechanici, majitelia vozidiel  
   - **Vstupné podmienky**: Mechanik má prístup k OBD-II diagnostickej jednotke  
   - **Výstupné podmienky**: Zobrazenie chybového kódu  
   - **Minimálny výstup**: Zobrazenie chybového kódu  
   - **Ideálny výstup**: Zobrazenie detailných informácií o závade

**Hlavný scénár**:  
1. Mechanik pripojí OBD-II jednotku k vozidlu.  
2. Systém vykoná diagnostiku a zobraziť chybový kód.

**Rozšírenie**:  
- Ak diagnostika zlyhá, zobrazí sa chybová hláška a mechanik sa musí pripojiť manuálne.

---

## Sekvenčný diagram
- Vytvorte sekvenčný diagram, ktorý ukáže interakcie medzi mechanikom, diagnostickým nástrojom a vozidlom.

---

## Triedny diagram
- Zobraziť triedy ako `Vehicle`, `ECUDiagnosticTool`, `OBD2_Codes` a ich vzťahy.

---

# Rozšírenie FURPS analýzy pre projekt diagnostického softvéru pre automobily

## 1. **S.M.A.R.T. Ciele (Specific, Measurable, Achievable, Relevant, Time-bound)**
Táto metodika pomáha definovať jasné a merateľné ciele, ktoré by mal systém splniť. Použitie tejto analýzy môže byť veľmi užitočné na určenie konkrétnych cieľov pre implementáciu systému:
- **Specific (Špecifické)**: Čo presne má systém robiť? (napr. čítanie diagnostických kódov)
- **Measurable (Merateľné)**: Ako budeme hodnotiť úspech? (napr. doba odozvy systému pri diagnostike)
- **Achievable (Dosiahnuteľné)**: Je tento cieľ realistický s dostupnými zdrojmi?
- **Relevant (Relevantné)**: Má tento cieľ skutočne hodnotu pre používateľov systému?
- **Time-bound (Časovo ohraničené)**: Kedy by mal byť cieľ dosiahnutý?

---

## 2. **SWOT analýza (Strengths, Weaknesses, Opportunities, Threats)**
SWOT analýza je skvelý nástroj na hodnotenie silných a slabých stránok systému, ako aj príležitostí a hrozieb, ktoré môžu ovplyvniť jeho úspešnosť:
- **Strengths (Silné stránky)**: Aké sú hlavné výhody systému (napr. vysoká spoľahlivosť)?
- **Weaknesses (Slabé stránky)**: Kde má systém slabiny (napr. obmedzená podpora pre staršie modely vozidiel)?
- **Opportunities (Príležitosti)**: Aké príležitosti existujú pre rozšírenie systému (napr. pripojenie na mobilné aplikácie)?
- **Threats (Hrozby)**: Aké externé faktory by mohli ohroziť systém (napr. technológie konkurentov)?

---

## 3. **Risk Analysis (Analýza rizík)**
Risk analýza sa zameriava na identifikáciu a hodnotenie potenciálnych rizík spojených s vývojom a implementáciou systému:
- **Technologické riziká**: Napríklad problémy s integráciou nových modelov vozidiel alebo zmeny v OBD-II protokole.
- **Projektové riziká**: Napríklad oneskorenie v implementácii alebo nepredvídané náklady.
- **Bezpečnostné riziká**: Riziká spojené s ochranou dát a citlivých informácií.

---

## 4. **UML (Unified Modeling Language) Diagramy**
Okrem FURPS analýzy môžu študenti využiť aj rôzne UML diagramy, ako sú:
- **Triedne diagramy**: Ukazujú štruktúru systému a jeho komponenty (triedy a objekty) s atribútmi a metódami.
- **Sekvenčné diagramy**: Ukazujú časovú posloupnosť udalostí a interakcií medzi rôznymi komponentami systému.
- **Stavové diagramy**: Zobrazujú rôzne stavy systému a prechody medzi nimi na základe určitých podmienok.
- **Aktivitné diagramy**: Vizualizujú tok aktivít v systéme a rozhodovanie medzi rôznymi operáciami.

---

## 5. **Agilné metodiky (Scrum, Kanban)**
Pre projektový manažment je možné použiť agilné metodiky na riadenie vývoja systému. Tieto metodiky sú obzvlášť užitočné pri dynamických projektoch, kde sa môže meniť rozsah a požiadavky:
- **Scrum**: Metodika, ktorá sa zameriava na pravidelné iterácie a tým aj rýchlejšie nasadzovanie nových funkcií.
- **Kanban**: Vizualizuje pracovný tok a umožňuje sledovať stav jednotlivých úloh v reálnom čase.

---

## 6. **Testovacia analýza (Testovanie kvality)**
Kvalitné testovanie je neoddeliteľnou súčasťou každého systému. Testovacia analýza by mala zahŕňať:
- **Unit Testing (Jednotkové testy)**: Testovanie jednotlivých komponentov systému.
- **Integration Testing (Integračné testy)**: Testovanie interakcie medzi rôznymi časťami systému.
- **Acceptance Testing (Akceptačné testy)**: Overenie, či systém spĺňa požiadavky používateľa a obchodné ciele.

---

## 7. **Vývojový životný cyklus (SDLC - Software Development Life Cycle)**
Pre štruktúrovaný vývoj môže byť užitočné dodržiavať niektorý z modelov vývojového životného cyklu:
- **Waterfall**: Tradičný prístup s fázami ako analýza, návrh, implementácia a testovanie.
- **Agile**: Flexibilnejší prístup s častými iteráciami a zlepšovaním systému.

---

# Zhrnutie
Na obohatenie tvojej video analýzy FURPS môžeš zvážiť pridanie ďalších metodík a nástrojov ako:
- **S.M.A.R.T. Ciele** na definovanie konkrétnych a merateľných cieľov.
- **SWOT analýza** na hodnotenie silných a slabých stránok systému.
- **Risk Analysis** na identifikáciu a hodnotenie potenciálnych rizík.
- **UML diagramy** na vizualizáciu a detailnejšie pochopenie systému.
- **Agilné metodiky** na riadenie projektu a iteratívny vývoj.
- **Testovacia analýza** na zabezpečenie kvality systému.
- **SDLC modely** na riadenie vývoja.

Tieto metódy a analýzy môžu študentom pomôcť lepšie pochopiť rôzne aspekty systému a jeho vývoja, čo je veľmi užitočné pri implementácii skutočných softvérových riešení.

