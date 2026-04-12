# Wyniki Eksperymentalne: Co LLaMEA Faktycznie Osiąga

Ta strona podsumowuje kluczowe wyniki eksperymentalne z arXiv paper [^1] i blogu [^2]. Bez ściemniania — co konkretnie działa, a co wymaga zastrzeżeń.

## Główne twierdzenie

> LLaMEA generuje algorytmy metaheurystyczne które **przewyższają lub dorównują** CMA-ES i Differential Evolution na BBOB, przy czym algorytmy te zostały **automatycznie wygenerowane** bez ręcznego projektowania [^1].

## Wyniki liczbowe

### Na 5 wymiarach (5D)

LLaMEA wygrywa z:
- **CMA-ES (default)** — na większości z 24 funkcji BBOB
- **CMA-ES (tuned)** — konkurencyjne
- **Differential Evolution (DE)** — przewyższa na prawie wszystkich funkcjach

### Na 10 i 20 wymiarach

Wyniki są **konkurencyjne**, choć pełne wygrane są trudniejsze do uzyskania. LLaMEA nie widziało tych wymiarów podczas generacji — sukces w 10D/20D to **ekstrapolacja** [^1].

### Jakość wygenerowanych algorytmów

Wygenerowane algorytmy to nie proste warianty istniejących metaheurystyk. Paper [^1] opisuje że LLM:
- Tworzy **nowe kombinacje operatorów**
- Wykorzystuje **wiedzę o funkcjach benchmarkowych** (mimo black-box)
- Implementuje **hybrydowe strategie** (łączenie faz eksploracji i eksploatacji)

## Analiza przebiegów zbieżności

IOHanalyzer generuje wykresy ECDF (Empirical Cumulative Distribution Function) [^1] — pokazujące dla każdego budżetu ewaluacji, jaka frakcja uruchomień osiągnęła cel.

Na tych wykresach LLaMEA:
- **Szybciej startuje** (szybsza zbieżność w początkowej fazie)
- **Nie utyka** w lokalnych minimach tak często jak DE
- **Dorównuje** CMA-ES w fazie eksploatacji (dokładne zawężanie)

## Co jest imponujące?

1. **Automatyczne wykrywanie struktury** — LLM nie ma bezpośredniego dostępu do funkcji celu, ale "domyśla się" struktury problemu z zachowania w benchmarku
2. **Zero ekspertyzy od człowieka** — cały projekt algorytmu wygenerowany
3. **Reprodukowalność** — te same warunki startowe dają te same wyniki (dzięki IOHprofiler)

## Co wymaga zastrzeżeń?

1. **API cost** — GPT-4 jest drogi, każda iteracja kosztuje
2. **Nie zawsze lepszy** — na niektórych funkcjach CMA-ES tuned nadal wygrywa
3. **Ograniczone wymiary** — 5D to maksimum gdzie LLaMEA konsekwentnie wygrywa
4. **Brak teorii** — brak matematycznych gwarancji zbieżności (typowe dla EC)

## Praktyczne implikacje

Jeśli masz problem optymalizacyjny [^2]:

| Scenariusz | Rekomendacja |
|-----------|------------|
| Problem ciągły, 3-5D, budżet >10K ewaluacji | Wypróbuj LLaMEA |
| Problem wymaga szybkiej zbieżności | CMA-ES nadal solidny |
| Potrzebujesz teoretycznych gwarancji | Żaden z nich |
| Budżet ograniczony, kod musi być prosty | CMA-ES / DE |

## Porównanie z AlphaEvolve (Google DeepMind)

LLaMEA jest opisywane jako **"fully-open alternative to Google DeepMind's AlphaEvolve"** [^3]. AlphaEvolve używa Gemini do ewolucji algorytmów, ale jest zamknięte. LLaMEA jest MIT-licencjonowane i w pełni reprodukowalne.

---

**Następna strona:** [08 — Badania powiązane](pages/08-related-research) — co dzieje się w sąsiednich obszarach
