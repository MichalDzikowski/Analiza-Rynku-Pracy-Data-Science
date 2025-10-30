# Analiza-Rynku-Pracy-Data-Science

Projekt ten jest szczegółową analizą zbioru danych "Data Science Jobs Salaries" (Kaggle), obejmującego ponad 200 ofert pracy z lat 2020-2021. Celem analizy było zidentyfikowanie kluczowych czynników wpływających na wysokość wynagrodzeń oraz zrozumienie  trendów na rynku pracy w branży Data Science.
Źródło:https://www.kaggle.com/datasets/saadaliyaseen/decoding-data-science-careers-salaries-and-insights

## 1. Cel Projektu

Głównym celem projektu było przeprowadzenie analizy eksploracyjnej (EDA), aby odpowiedzieć na następujące pytania biznesowe:

1.  **Jakie są najbardziej poszukiwane stanowiska** w branży Data Science?
2.  **Jak poziom doświadczenia** (`Entry`, `Mid`, `Senior`, `Executive`) wpływa na wysokość zarobków i ich rozpiętość?
3.  **Jak zmieniały się mediany zarobków** w czasie (w latach 2020-2021)?
4.  **W których krajach** oferowane są najwyższe wynagrodzenia?
5.  **Czy wielkość przedsiębiorstwa** (`Mała`, `Średnia`, `Duża`) ma  wpływ na oferowane pensje?

## 2. Proces Analityczny

Analiza została przeprowadzona w notatniku Jupyter, krok po kroku, obejmując następujące etapy:

### Etap I: Wczytanie i Czyszczenie Danych (ETL)

1.  **Wczytanie Danych:** Załadowanie pliku `Data Science Jobs Salaries.csv` do ramki danych `pandas`.
2.  **Zrozumienie struktury danych:** Przeprowadzenie inspekcji (`.info()`, `.head()`) wykazało, że zbiór jest w dużej mierze czysty i nie posiada brakujących wartości (`NaN`).
3.  **Czyszczenie i Mapowanie Danych:**
    * **Poziomy Doświadczenia:** Kolumna `experience_level` została zmapowana ze skrótów (`EN`, `MI`, `SE`, `EX`) na pełne, czytelne nazwy (np. `Entry-level (Początkujący)`, `Senior-level (Senior)`).
    * **Rok Pracy:** Zidentyfikowano "zanieczyszczenia" w kolumnie `work_year` (np. wartości `2021e`). Kolumna została wyczyszczona za pomocą wyrażeń regularnych (`.str.extract(r'(\d{4})')`), aby wyizolować 4-cyfrowy rok, a następnie przekonwertowana na typ numeryczny.

### Etap II: Analiza Eksploracyjna i Wizualizacja

1.  **Analiza Stanowisk:** Zastosowano `value_counts()` na kolumnie `job_title`, aby zidentyfikować 10 najczęściej występujących stanowisk.
2.  **Analiza Zarobków:** We wszystkich analizach płacowych użyto **mediany** (zamiast średniej), aby uzyskać wyniki bardziej odporne na skrajnie wysokie lub niskie oferty (outliery).
3.  **Agregacja Danych:** Użyto `groupby()` do obliczenia mediany `salary_in_usd` w podziale na:
    * `experience_level_full` (Poziom doświadczenia)
    * `work_year_cleaned` (Rok)
    * `company_location` (Lokalizacja firmy)
    * `company_size` (Wielkość firmy)
4.  **Wizualizacja:** Stworzono interaktywne wykresy (słupkowe, liniowe i pudełkowe) przy użyciu biblioteki `Altair` i zapisano je jako pliki `.html`.


## 3. Wnioski Analityczne

### Wniosek 1: Doświadczenie jest kluczowym czynnikiem wzrostu płac
Analiza rozkładu zarobków (boxplot) wyraźnie pokazuje, że pensje rosną wraz z poziomem doświadczenia. Co ważniejsze, znacząco rośnie również **rozpiętość (widełki)** wynagrodzeń – na poziomie `Senior` i `Executive` rozrzut płac jest nieporównywalnie większy niż na poziomie `Entry`, co wskazuje na dużą wartość specjalistycznej wiedzy.

<img width="869" height="483" alt="salary_vs_experience" src="https://github.com/user-attachments/assets/9e2ef4df-0c1e-4ccf-bc19-3f10daf145e2" />


### Wniosek 2: Zmiana pensji w latach 2020-2021
Analiza trendów czasowych pokazuje, że Entry-level odnotował niewielki wzrost zarobków, co może wynikać z rosnącego zapotrzebowania na młodszych specjalistów. Mid-level oraz Executive poziomy wykazały spadek wynagrodzeń, co sugeruje większą konkurencję oraz stabilizację stawek w wyższych segmentach.Senior-level utrzymał relatywnie stabilne wynagrodzenie, z lekkim wzrostem w ostatnich latach. Trend może odzwierciedlać zmiany rynkowe- automatyzację procesów, zwiększoną dostępność specjalistów oraz rozwój narzędzi AI

<img width="1032" height="382" alt="salary_growth_trends" src="https://github.com/user-attachments/assets/2b58e9ee-c585-44c3-9564-8e4ec6dc5e62" />


### Wniosek 3: Dominacja Japonii oraz Stanów Zjednoczonych na rynku płac
Analiza geograficzna (ograniczona do 10 krajów z największą liczbą ofert)  wskazuje, że **Stany Zjednoczone oraz Japonia** oferują zdecydowanie najwyższą medianę wynagrodzeń. Różnica ta jest znacząca w porównaniu do innych dużych rynków, takich jak Wielka Brytania (`GB`), Kanada (`CA`) czy Niemcy (`DE`).

<img width="869" height="364" alt="salary_by_country" src="https://github.com/user-attachments/assets/16018c9f-20f2-48c4-a0dc-9197c3b2dc6d" />


### Wniosek 4: Wielkość przedsiębiorstwa ma znaczenie
Analiza wykazała, że **średnie (`M`) i duże (`L`) firmy płacą więcej** niż małe (`S`). Mediana pensji w dużych przedsiębiorstwach była najwyższa. Sugeruje to, że choć  małe firmy mogą kusić innymi benefitami, to stabilne, dojrzałe organizacje oferują statystycznie wyższe wynagrodzenie bazowe.

<img width="869" height="434" alt="salary_by_company_size" src="https://github.com/user-attachments/assets/ba6e2ef2-60ca-4a19-8fb3-512efb94c40c" />



## 4. Wykorzystane Technologie

* **Język:** Python
* **Środowisko:** Jupyter Notebook
* **Analiza Danych:**
    * **Pandas:** 
* **Wizualizacja Danych:**
    * **Altair:**
