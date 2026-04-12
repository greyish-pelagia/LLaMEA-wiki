# Podstawy Optymalizacji: Od Gradientu do Metaheurystyk

Aby zrozumieć LLaMEA, musisz najpierw rozumieć kontekst: czym jest optymalizacja black-box i dlaczego potrzebujemy metaheurystyk zamiast klasycznych metod gradientowych.

## Formalna definicja problemu optymalizacji

LLaMEA rozwiązuje problem optymalizacji ciągłej black-box:

$$\text{minimize } \mathcal{F}: \mathcal{S} \rightarrow \mathbb{R}$$

gdzie $\mathcal{S} \subseteq \mathbb{R}^d$ to przestrzeń poszukiwań zdefiniowana przez ograniczenia pudełkowe (box constraints): $\mathcal{S} = \times_{i=1}^{d}[l_i, u_i]$, gdzie $l_i < u_i$ dla każdego wymiaru $i$ [[1]]([[1]]).

**Black-box** oznacza, że nie mamy wzoru analitycznego ani gradientu — możemy tylko ewaluować funkcję celu $\mathcal{F}$ w dowolnym punkcie $\vec{x} \in \mathcal{S}$.

## Dlaczego nie gradient?

Klasyczne metody gradientowe (SGD, Adam, Newton-Raphson) wymagają:
1. **Gradientu** — informacji o pochodnych
2. **Wypukłości** (dla gwarancji zbieżności) — lub przynajmniej regularności

W problemach black-box:
- Gradient jest niedostępny (symulacje fizyczne, środowiska dyskretne, orzeczenia "czarnych skrzynek")
- Funkcja celu może być niewypukła, wielomodalna, zaszumiona
- Gradient może istnieć formalnie, ale numeryczne jego obliczenie jest zbyt kosztowne

## Hierarchia metod optymalizacyjnych

```
Metody gradientowe (wymagają gradientu)
├── Gradient Descent / SGD
├── Newton-Raphson
└── L-BFGS
        ↓ (gradient niedostępny)
Metody bezgradientowe (derivative-free)
├── Pattern Search (Hooke-Jeeves)
├── Nelder-Mead (Simplex)
└── Direct Optimization
        ↓ (problemy wielomodalne, złożona geometria)
Metaheurystyki (inspirowane naturą)
├── Evolutionary Algorithms (GA, ES)
├── Particle Swarm Optimization
├── Differential Evolution
└── ...500+ wariantów
```

## Dlaczego metaheurystyki działają?

Metaheurystyki nie wymagają gradientu i są odporne na:
- **Wielomodalność** — wiele lokalnych minimów (rys.1)
- **Nieregularność** — niewypukłe landscape'y
- **Szum** — stochastyczne funkcje celu
- **Ograniczenia** — proste do zakodowania jako kary

Ich siła pochodzi z **inspirowanych naturą** mechanizmów przeszukiwania przestrzeni, które balansują dwie sprzeczne strategie [[1]]([[1]]):
- **Eksploracja** (exploration) — odkrywanie nowych regionów przestrzeni
- **Eksploatacja** (exploitation) — dokładne przeszukiwanie obiecujących regionów

## Box constraints w LLaMEA

LLaMEA rozwiązuje problemy z ograniczeniami pudełkowymi — każdy wymiar $d$ ma swój zakres $[l_i, u_i]$. To dość typowe ograniczenie w problemach inżynieryjnych (np. parametry materiałowe, wymiary konstrukcyjne).

**Zadanie dla czytelnika:** Wyobraź sobie problem optymalizacji kształtu anteny — każdy parametr geometryczny ma fizycznie uzasadnione min/max. Jak zamodelować problem z ograniczeniami nierównościowymi (np. napięcie < 5V)?

Odpowiedź: LLaMEA koncentruje się na **box-constrained continuous optimization**, a bardziej złożone ograniczenia można modelować przez funkcje kary lub transformacje przestrzeni poszukiwań [[1]]([[1]]).

---

**Następna strona:** [[02-evolutionary-computation]] — jak ewolucja biologiczna stała się paradygmatem optymalizacji
