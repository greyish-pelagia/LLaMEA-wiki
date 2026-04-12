# Metaheurystyki: Jak Strategia Przeszukuje Przestrzeń Rozwiązań

**Metaheurystyka** to ramowy algorytm wysokiego poziomu, który dostarcza "heurystyk ogólnych" (general-purpose heuristics) do rozwiązywania trudnych obliczeniowo problemów optymalizacyjnych [^1]. W przeciwieństwie do algorytmu konkretnego (np. "sortowanie przez scalanie"), metaheurystyka to **strategia** którą można instantate dla różnych problemów.

## Czym metaheurystyka różni się od heurystyki?

| Cecha | Heurystyka | Metaheurystyka |
|-------|-----------|----------------|
| Zakres | Specyficzna dla problemu | Ogólna (domain-independent) |
| Adaptacyjność | Statyczna | Dynamicznie dostosowuje się |
| Gwarancje | Często brak | Brak gwarancji optimum |
| Siła | Silna na jednym problemie | Praktyczna na wielu |

## Dwie składowe każdej metaheurystyki

Każda metaheurystyka balansuje fundamentalny trade-off [^1][^2]:

**1. Eksploracja (Exploration)** — odkrywanie nowych regionów przestrzeni poszukiwań
- Unikanie utknięcia w lokalnych minimach
- Badanie nieznanych obszarów

**2. Eksploatacja (Exploitation)** — dokładne przeszukiwanie obiecujących regionów  
- Zawężanie poszukiwań wokół najlepszych znalezionych rozwiązań
- Intensyfikacja wiedzy

```
Zbyt dużo eksploracji  →  losowe błądzenie, brak zbieżności
Zbyt dużo eksploatacji →  utknięcie w lokalnym minimum
```

## Klasyczne metaheurystyki

### Simulated Annealing (SA)
Inspiracja: wyżarzanie metali. Algorytm "chłodzenia" — początkowo akceptuje też gorsze rozwiązania (wysoka temperatura), z czasem coraz bardziej restrykcyjny.

### Tabu Search
Pamięć krótkoterminowa — lista tabu (zakazanych ruchów) zapobiega cyklom i pozwala wychodzić z lokalnych minimów.

### Variable Neighborhood Search (VNS)
Systematyczne zmiany struktury sąsiedztwa — gdy VNS utknie, zmienia definicję "sąsiedztwa".

### Iterated Local Search (ILS)
Łączy losowe perturbacje z intensywnym przeszukiwaniem lokalnym.

## Metaheurystyki inspiracji biologicznej (główny nurt w EC)

**Ewolucyjne:** GA, ES, DE, CMA-ES — manipulacja populacją osobników

**Rojowe:** PSO (ptaki), ACO (mrówki), BA (nietoperze), WOA (wieloryby) — agenty komunikujące się przez środowisko

**Pozostałe:** Jaya, Rao, Harris Hawks, Salp Swarm — mniej "ukorzenione" biologicznie

## Problem 500+ metaheurystyk

Autorzy LLaMEA słusznie zauważają [^1]: w literaturze istnieje ponad 500 zaproponowanych metaheurystyk, ale większość to niewielkie modyfikacje istniejących metod, a **systematyczne porównanie z SOTA (state-of-the-art) jest rzadkością**.

Problem:
- Nowa metaheurystyka pojawia się, jest "inspirowana" nową metaforą
- Brak rygorystycznego porównania z CMA-ES czy DE
- Publikacja często na podstawie kilku testowych funkcji
- Brak wiedzy o tym, co faktycznie działa lepiej

LLaMEA **systematycznie rozwiązuje** ten problem przez automatyczne generowanie i benchmarkowanie.

## Modularny design metaheurystyk

Nowoczesne podejście: zamiast projektować jeden algorytm, projektuj **moduły** które można rekombinować [^1]:
- Moduł inicjalizacji
- Moduł mutacji
- Moduł crossover
- Moduł selekcji
- Moduł restartacji

To pozwala na przestrzeń milionów kombinacji — ale nadal wymaga eksperta do definiowania modułów.

**LLaMEA idzie dalej** — zamiast rekombinować istniejące moduły, LLM **generuje zupełnie nowy kod algorytmu** [^1][^2].

---

**Następna strona:** [04 — Rdzeń LLaMEA](pages/04-llamea-core-loop) — jak LLM wchodzi do pętli ewolucyjnej
