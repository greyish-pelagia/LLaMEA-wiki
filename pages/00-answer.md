# LLaMEA: Automatyczne Projektowanie Algorytmów Optymalizacyjnych przez LLM

**LLaMEA** (Large Language Model Evolutionary Algorithm) to framework, który łączy dwa potężne paradygmaty: ewolucyjne obliczenia optymalizacyjne i duże modele językowe (LLM). Zasadniczo — zamiast eksperta od metaheurystyk, który ręcznie projektuje algorytm optymalizacyjny, LLaMEA wykorzystuje GPT-4 do automatycznego generowania, mutowania i selekcjonowania takich algorytmów [^1].

## TL;DR — Co to właściwie robi?

Wyobraź sobie, że masz złożony problem optymalizacyjny (np. zoptymalizować kształt skrzydła samolotu, harmonogram logistyczny albo parametry sieci neuronowej). Tradycyjnie potrzebujesz eksperta, który zna dziesiątki algorytmów metaheurystycznych i wie, który jak zastosować. LLaMEA **automatyzuje ten proces eksperckiego projektowania** — podajesz opis problemu, a system iteracyjnie ewoluuje algorytmy, testuje je na benchmarkach i zostawia te, które działają najlepiej [^2].

## Dlaczego to istotne?

1. **Ekspertyza jest ograniczona** — istnieje >500 metaheurystyk w literaturze, ale większość to niewielkie warianty istniejących metod [^1]. LLaMEA nie jest ograniczone do istniejących modułów — LLM może wygenerować zupełnie nową strukturę algorytmu.
2. **Automatyczna optymalizacja hiperparametrów na sterydach** — zamiast dostrajać istniejący algorytm, LLaMEA generuje całą jego architekturę.
3. **Wyniki mówią same za siebie** — wygenerowane algorytmy **przewyższają** CMA-ES (Covariance Matrix Adaptation Evolution Strategy) i Differential Evolution na benchmarku BBOB w 5 wymiarach, mimo że nie widziały tych instancji podczas treningu [^1].

## Kluczowy pomysł w jednym zdaniu

> LLaMEA zamyka pętlę ewolucyjną (generacja → ewaluacja → selekcja → mutacja) gdzie **LLM jest generatorem** nowych wariantów algorytmu, a **automatyczny benchmark** dostarcza informację zwrotną o jakości [^1][^2].

## Struktura wiki

Ta wiki jest zorganizowana dla studenta magisterskiego z podstawową wiedzą o ML:

1. [01 — Fundamenty optymalizacji](pages/01-optimization-foundations) — gradient, bezgradientowa, box-constrained
2. [02 — Obliczenia ewolucyjne](pages/02-evolutionary-computation) — inspiracja biologiczna, portfolio algorytmów
3. [03 — Metaheurystyki](pages/03-metaheuristics-explained) — eksploracja vs. eksploatacja, >500 metod
4. [04 — Rdzeń LLaMEA](pages/04-llamea-core-loop) — jak LLM wchodzi do pętli ewolucyjnej
5. [05 — Architektura systemu](pages/05-architecture) — integracja modułów
6. [06 — Benchmark BBOB](pages/06-bbob-benchmark) — IOHprofiler
7. [07 — Wyniki eksperymentalne](pages/07-experimental-results) — co oznaczają
8. [08 — Badania powiązane](pages/08-related-research) — benchmarki automatyczne, reasoning LLM
9. [09 — Pierwsze kroki](pages/09-getting-started) — instalacja i pierwszy eksperyment

## Odpowiedź na pytanie "po co mi to?"

Jeśli prowadzisz badania w ML/AI — LLaMEA pokazuje nowy paradygmat: **LLM jako komponent algorytmiczny w pętli optymalizacyjnej**. To nie jest chatbot; to automatyczny projektant algorytmów.

Jeśli interesuje cię inżynieria — wyobraź sobie, że zamiast wybierać między PSO, GA, CMA-ES czy DE, system generuje dla twojego konkretnego problemu **coś lepszego niż wszystkie te opcje**.

Jeśli chcesz zbudować coś podobnego — [strona 09](pages/09-getting-started) pokazuje jak uruchomić LLaMEA w 5 minut.

---

**Referencje:**

[^1]: van Stein & Bäck, *LLaMEA: A Large Language Model Evolutionary Algorithm for Automatically Generating Metaheuristics*, arXiv:2405.20132, 2024

[^2]: Niki van Stein, *LLaMEA: Combining the Power of Evolution and Large Language Models*, blog post, 2024

[^3]: LIACS XAI Group, *LLaMEA — Natural Computing Group*, https://naco.liacs.nl/projects/2024-llamea/
