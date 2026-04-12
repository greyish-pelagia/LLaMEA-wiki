# Rdzeń LLaMEA: Pętla Ewolucyjna z LLM jako Generatorem

**To jest serce LLaMEA** — strona którą chciałbyś przeczytać gdybyś czytał tylko jedną.

## Główna innowacja

Tradycyjne podejścia do automatycznego projektowania algorytmów (np. modularny CMA-ES, Modular DE) wymagają **eksperta** który zdefiniuje przestrzeń modułów [[1]]([[1]]). LLaMEA eliminuje to ograniczenie: LLM (np. GPT-4) jest traktowany jako **generator czarnych skrzynek kodu** — na wejściu dostaje opis problemu i informację zwrotną z benchmarku, na wyjściu produkuje kod nowego algorytmu [[1]]([[1]])[[2]]([[2]]).

## Pętla ewolucyjna LLaMEA krok po kroku

```
┌─────────────────────────────────────────────────────────────┐
│  1. GENERUJ                                                     │
│     LLM (GPT-4) generuje kod algorytmu metaheurystycznego     │
│     na podstawie: opisu problemu + historii ewaluacji          │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│  2. EWALUUJ                                                     │
│     IOHexperimenter uruchamia algorytm na BBOB benchmarku      │
│     i zwraca metryki: wartość funkcji celu, zbieżność, itp.   │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│  3. SELEKCJA + MUTACJA                                         │
│     Najlepsze algorytmy (lub ostatni) są wybierane            │
│     i przekazywane z powrotem do LLM jako kontekst mutacji     │
└─────────────────────────────────────────────────────────────┘
                              ↓
                              └──────────→ (powtórz)
```

Źródło diagramu: [[2]]([[2]])

## Szczegóły każdego kroku

### Krok 1: Generacja przez LLM

LLM dostaje **prompt** zawierający [[1]]([[1]]):
- Opis problemu optymalizacyjnego (funkcja celu, ograniczenia, wymiarność)
- Instrukcję wyjściową: kod Pythona z algorytmem metaheurystycznym
- Opcjonalnie: informację zwrotną z poprzednich iteracji ("algorytm X miał problem z eksploatacją, zaproponuj wariant")

Model GPT-4 jest tu kluczowy — ma wiedzę o:
- Strukturach kodu metaheurystyk (pętle, warunki, operatory)
- Konwencjach nazewnictwa i stylu
- Matematycznych konceptach optymalizacji

### Krok 2: Automatyczna ewaluacja

Wygenerowany kod jest [[1]]([[1]])[[2]]([[2]]):
1. **Wykonywany** na benchmarku BBOB (24 funkcje testowe, instancje 5D/10D/20D)
2. **Ewaluowany** przez IOHexperimenter — ten sam framework co dla porównań论文owych
3. **Metryki zbierane** — przebieg zbieżności, wartość końcowa, liczba ewaluacji

### Krok 3: Selekcja i mutacja

LLaMEA implementuje typową selekcję ewolucyjną [[2]]([[2]]):
- **Elitaryzm** — najlepsze algorytmy przechodzą bez zmian
- **Mutacja** — najlepszy algorytm jest "wracany" do LLM z prośbą o wariant z modyfikacjami
- Warianty: zmiana wielkości populacji, modyfikacja operatora, dodanie nowej fazy

## Co sprawia, że to działa?

### LLM jako "unikalny punkt w przestrzeni"
GPT-4 może generować kod algorytmu który jest **nową kombinacją** struktur i wzorców — nie tylko rekombinacją istniejących modułów, ale czymś potencjalnie nigdy nie widzianym w literaturze [[1]]([[1]]).

### Automatyczny benchmark zamyka pętlę
Bez IOHprofiler/LLaMEA byłby tylko "ciekawym pomysłem" — feedback w postaci twardych liczb (porównanie z CMA-ES) jest krytyczny [[1]]([[1]]).

### Brak ograniczeń przestrzeni modułów
Modularny CMA-ES jest ograniczony do kombinacji predefiniowanych modułów. LLM może wygenerować zupełnie nową architekturę algorytmiczną [[1]]([[1]]).

## Co LLM faktycznie generuje?

Według arXiv paper [[1]]([[1]]), LLM generuje algorytmy w **języku Python** które:
- Implementują strategie przeszukiwania lokalnego (local search)
- Używają populacji osobników
- Zawierają operatory mutacji/crossover specyficzne dla domeny
- Integrują wiedzę o funkcjach benchmarkowych z dyskretną reprezentacją rozwiązań

Przykładowy pseudokod generowanego algorytmu [[1]]([[1]]):
```
class GeneratedOptimizer:
    def __init__(self, dim, bounds):
        self.population = self.initialize(dim, bounds)
        self.best = min(self.population)
    
    def step(self):
        # LLM-generated mutation logic
        offspring = self.mutate(self.best)
        # LLM-generated selection logic
        self.population = self.select(self.population, offspring)
        self.best = min(self.population)
```

## Iteracje i wyniki

LLaMEA uruchamia wiele generacji (pokoleń) ewolucji [[1]]([[1]])[[2]]([[2]]):
- W każdej iteracji: generacja → ewaluacja → selekcja
- Proces trwa aż kryteria zatrzymania (np. budżet ewaluacji)
- Końcowy wynik: najlepszy algorytm z całej ewolucji

---

**Następna strona:** [[05-architecture]] — jak to jest zaimplementowane
