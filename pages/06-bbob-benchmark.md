# Benchmark BBOB i IOHprofiler: Jak Mierzyć Jakość Algorytmu

**Wynik algorytmu jest tak dobry jak benchmark na którym go testujesz.** Ta strona wyjaśnia dlaczego BBOB jest standardem w optymalizacji i jak LLaMEA wykorzystuje IOHprofiler do automatycznego benchmarkowania.

## Problem: jak porównać algorytmy optymalizacyjne?

Powiedzmy, że masz nowy algorytm i twierdzisz że jest lepszy od CMA-ES. Co to właściwie znaczy?

- "Lepszy na jednej funkcji"?
- "Lepszy szybciej"?
- "Lepszy na średniej z 10 uruchomień"?
- "Lepszy w 90% przypadków na każdej funkcji"?

Bez **ustandaryzowanego benchmarku** każdy może ogłosić sukces swojej metody na własnych, dogodnie dobranych testach.

## BBOB — Black Box Optimization Benchmark

BBOB to **standard de facto** w społeczności optymalizacyjnej [[1]]([[1]])[[2]]([[2]]). Zawiera:

### 24 funkcje testowe

Funkcje są starannie dobrane aby reprezentować różne wyzwania optymalizacyjne [[1]]([[1]]):

| Kategoria | Przykładowe funkcje | Co testują |
|-----------|--------------------|-----------|
| Separowalne | Sphere, Ellipsoidal | Podstawowa zbieżność |
| Zależne od współrzędnych | Rotated Ellipsoidal | Warunkowanie |
| Multimodalne | Rastrigin, Schaffer | Lokalne minima |
| Hiperplan | Rosenbrock, Discus | Iteracyjne zbieżność |
| Szerokie optimum | Schwefel, Gallagher | Eksploracja |

### Instancje

Każda funkcja ma **15 niezależnych instancji** (różne minima lokalne, przesunięte optimum). Testowanie na wielu instancjach chroni przed **overfittingiem** do konkretnej geometrii [[1]]([[1]]).

### Wymiary

Testy w wymiarach: **2, 3, 5, 10, 20, 40**. LLaMEA koncentruje się na 5D, 10D, 20D [[1]]([[1]]).

## IOHprofiler — automatyczny benchmark runner

**IOHprofiler** to framework który automatycznie [[1]]([[1]]):
1. Uruchamia twój algorytm na każdej funkcji × instancji × wymiarze
2. Zapisuje **przebieg zbieżności** (funkcja celu vs. numer ewaluacji)
3. Produkuje **statystykę** (średnia, mediana, sukces ratio)
4. Generuje **wykresy** (ECDF — Empirical Cumulative Distribution Function)

### IOHexperimenter vs IOHanalyzer

- **IOHexperimenter** — runner: uruchamia eksperymenty
- **IOHanalyzer** — analizator: wizualizuje i porównuje wyniki

Razem pozwalają na **w pełni automatyczne, powtarzalne porównanie** nowego algorytmu z baselines.

## Kluczowa metryka: Expected Runtime (ERT)

**ERT (Expected Runtime)** to standardowa metryka w BBOB — średnia liczba ewaluacji potrzebna do osiągnięcia progu jakości $\mathcal{F} - f_{target}$ [[1]]([[1]]).

$$ERT(f, \text{algorithm}) = \text{średnia liczba ewaluacji do } f(\vec{x}) \leq f_{target}$$

Niższy ERT = lepszy algorytm.

## Jak LLaMEA wykorzystuje BBOB?

LLaMEA jest **sprzężone z IOHexperimenter** jako pętla ewaluacyjna [[1]]([[1]])[[2]]([[2]]):

```
LLM.generate_algorithm_code()
         ↓
IOHexperimenter.run(code, BBOB_functions=[f1,...,f24], dims=[5,10,20])
         ↓
ERT_scores = {f1: 1234, f2: 567, ...}
         ↓
LLM.evaluate_and_suggest_improvements(ERT_scores)
         ↓
goto GENERUJ
```

To **automatycznie zamyka pętlę**: nie ma ręcznego uruchamiania, analizy, decyzji — wszystko dzieje się w ramach frameworka.

## Co oznacza "wygrywamy z CMA-ES"?

LLaMEA twierdzi że wygenerowane algorytmy są lepsze od [[1]]([[1]]):
- CMA-ES z default hyperparameters
- CMA-ES z tuned hyperparameters  
- Differential Evolution (DE)

"**Lepsze**" oznacza: **niższy ERT (szybsza zbieżność) na większości funkcji BBOB w danym wymiarze**.

Ale uwaga — to nie znaczy że na **każdej** funkcji i **każdej** instancji. BBOB raportuje średnie, i LLaMEA wygrywa na średniej lub w sensie **ERT aggregated over all functions** [[1]]([[1]]).

## Znaczenie dla praktyka

Jeśli masz prawdziwy problem optymalizacyjny:
1. Możesz go zgłosić do BBOB (jeśli jest ciągły, bezgradientowy)
2. Możesz uruchomić CMA-ES / DE jako baselines
3. Możesz użyć LLaMEA do automatycznego wygenerowania lepszego algorytmu
4. Wynik będzie **reprodukowalny i porównywalny** z literaturą

---

**Następna strona:** [[07-experimental-results]] — co dokładnie LLaMEA osiąga
