# Obliczenia Ewolucyjne: Algorytmy InsPIrowane Biologią

**Obliczenia ewolucyjne** (Evolutionary Computation, EC) to klasa algorytmów optymalizacyjnych inspirowanych Darwinowską teorią ewolucji. Zamiast jednego rozwiązania, EC utrzymuje **populację** kandydatów i iteracyjnie ją ulepsza przez mechanizmy: **selekcja**, **krzyżowanie** i **mutacja** [[1]]([[1]]).

## Fundamentalna analogia

| Biologia | Obliczenia Ewolucyjne |
|----------|----------------------|
| Osobnik (fenotyp) | Wektor parametrów $\vec{x}$ |
| Genom (genotyp) | Kod algorytmu / wektor decyzyjny |
| Fitness | Wartość funkcji celu $\mathcal{F}(\vec{x})$ |
| Środowisko | Problem optymalizacyjny |
| Selekcja | Przetrwanie najlepszych |
| Mutacja | Losowa zmiana genów |
| Krzyżowanie | Rekombinacja materiału genetycznego |

## Algorytmy ewolucyjne — portfolio

### Genetic Algorithm (GA) — Holland, 1975
Najstarszy i najbardziej znany. Reprezentacja: binarna lub rzeczywista. Operatory: selekcja ruletkowa, krzyżowanie jednopunktowe, mutacja bitowa.

### Evolution Strategy (ES) — Rechenberg, Schwefel, 1970s
Reprezentacja rzeczywista. Nacisk na **samosterującą się mutację** (self-adaptive mutation). Wariant **CMA-ES** (Covariance Matrix Adaptation ES) to obecnie jeden z najpotężniejszych solverów bezgradientowych [[1]]([[1]]).

### Differential Evolution (DE) — Storn & Price, 1997
Specjalizowany w optymalizację ciągłą. Operatory oparte na różnicach wektorów populacji. Bardzo skuteczny na problemach wielomodalnych.

### Particle Swarm Optimization (PSO) — Kennedy & Eberhart, 1995
Inspirowany stadnym zachowaniem ptaków/ryb. Cząsteczki "latają" po przestrzeni, pamiętając własne najlepsze i globalne najlepsze pozycje.

## Schemat ogólny algorytmu ewolucyjnego

```
INITIALIZE population P with random individuals
EVALUATE fitness of each individual in P
WHILE not TERMINATION_CRITERION:
    SELECT parent individuals from P (fitness-based)
    RECOMBINE pairs to produce offspring
    MUTATE offspring (random changes)
    EVALUATE fitness of offspring
    SELECT individuals for next generation from P ∪ offspring
END WHILE
RETURN best individual found
```

## Dlaczego EC działają? Teoria schematów

Holland wprowadził **teorię schematów** (Schema Theorem) — każdy osobnik reprezentuje mnóstwo schematów (wzorców bitowych). Krótkie, niskiego rzędu, wysokofitnessowe schematy są eksponencjalnie replikowane w populacji. To tłumaczy exploracyjność GA.

## CMA-ES — najważniejszy algorytm w tym obszarze

**Covariance Matrix Adaptation Evolution Strategy** to obecnie *de facto* standard w optymalizacji ciągłej bezgradientowej [[1]]([[1]]). Kluczowe mechanizmy:

1. **Adaptacja macierzy kowariancji** — automatyczne uczenie się struktury landscape'u funkcji celu
2. **Samosterująca się wariancja mutacji** — globalna skala kroków dostosowuje się do odległości od optimum
3. **Brak hiperparametrów do strojenia** — działa "out-of-the-box" na szerokiej klasie problemów

LLaMEA porównuje się z CMA-ES jako jednym z baseline'ów i **wygrywa** z nim na BBOB w 5D [[1]]([[1]]).

## Limitacje tradycyjnych EC

1. **Projektowanie operatorów wymaga ekspertyzy** — mutacja/crossover dla nowej domeny to sztuka
2. **Zależność od reprezentacji** — binarna vs. rzeczywista, kodowanie ma znaczenie
3. **500+ metaheurystyk** — większość to niewielkie warianty, bez systematycznego porównania [[1]]([[1]])

**LLaMEA rozwiązuje punkt #1** — LLM automatycznie projektuje operatory i strukturę algorytmu, nie człowiek.

---

**Następna strona:** [[03-metaheuristics-explained]] — metaheurystyki jako wyższy poziom abstrakcji
