# LLaMEA: Automatyczne Projektowanie Algorytmów Optymalizacyjnych przez LLM

**LLaMEA** (Large Language Model Evolutionary Algorithm) to framework, który łączy dwa potężne paradygmaty: ewolucyjne obliczenia optymalizacyjne i duże modele językowe (LLM). Zasadniczo — zamiast eksperta od metaheurystyk, który ręcznie projektuje algorytm optymalizacyjny, LLaMEA wykorzystuje GPT-4 do automatycznego generowania, mutowania i selekcjonowania takich algorytmów [[1]]([[1]]).

## TL;DR — Co to właściwie robi?

Wyobraź sobie, że masz złożony problem optymalizacyjny (np. zoptymalizować kształt skrzydła samolotu, harmonogram logistyczny albo parametry sieci neuronowej). Tradycyjnie potrzebujesz eksperta, który zna dziesiątki algorytmów metaheurystycznych i wie, który jak zastosować. LLaMEA **automatyzuje ten proces eksperckiego projektowania** — podajesz opis problemu, a system iteracyjnie ewoluuje algorytmy, testuje je na benchmarkach i zostawia te, które działają najlepiej [[2]]([[2]]).

## Dlaczego to istotne?

1. **Ekspertyza jest ograniczona** — istnieje >500 metaheurystyk w literaturze, ale większość to niewielkie warianty istniejących metod [[1]]([[1]]). LLaMEA nie jest ograniczone do istniejących modułów — LLM może wygenerować zupełnie nową strukturę algorytmu.
2. **Automatyczna optymalizacja hiperparametrów na sterydach** — zamiast dostrajać istniejący algorytm, LLaMEA generuje całą jego architekturę.
3. **Wyniki mówią same za siebie** — wygenerowane algorytmy **przewyższają** CMA-ES (Covariance Matrix Adaptation Evolution Strategy) i Differential Evolution na benchmarku BBOB w 5 wymiarach, mimo że nie widziały tych instancji podczas treningu [[1]]([[1]]).

## Kluczowy pomysł w jednym zdaniu

> LLaMEA zamyka pętlę ewolucyjną (generacja → ewaluacja → selekcja → mutacja) gdzie **LLM jest generatorem** nowych wariantów algorytmu, a **automatyczny benchmark** dostarcza informację zwrotną o jakości [[1]]([[1]])[[2]]([[2]]).

## Struktura wiki

Ta wiki jest zorganizowana dla studenta magisterskiego z podstawową wiedzą o ML:

1. [[01-optimization-foundations|**01**]] — Fundamenty optymalizacji (gradient, bezgradientowa, box-constrained)
2. [[02-evolutionary-computation|**02**]] — Obliczenia ewolucyjne (inspiracja biologiczna, portfolio algorytmów)
3. [[03-metaheuristics-explained|**03**]] — Metaheurystyki (exploracja vs. eksploatacja, >500 metod)
4. [[04-llamea-core-loop|**04**]] — **Rdzeń LLaMEA** — jak LLM wchodzi do pętli ewolucyjnej
5. [[05-architecture|**05**]] — Architektura systemu i integracja modułów
6. [[06-bbob-benchmark|**06**]] — Benchmark BBOB i rola IOHprofiler
7. [[07-experimental-results|**07**]] — Wyniki eksperymentalne i co oznaczają
8. [[08-related-research|**08**]] — Powiązane badania (benchmarki automatyczne, reasoning LLM)
9. [[09-getting-started|**09**]] — Instalacja i pierwszy eksperyment

## Odpowiedź na pytanie "po co mi to?"

Jeśli prowadzisz badania w ML/AI — LLaMEA pokazuje nowy paradygmat: **LLM jako komponent algorytmiczny w pętli optymalizacyjnej**. To nie jest chatbot; to automatyczny projektant algorytmów.

Jeśli interesuje cię inżynieria — wyobraź sobie, że zamiast wybierać między PSO, GA, CMA-ES czy DE, system generuje dla twojego konkretnego problemu **coś lepszego niż wszystkie te opcje**.

Jeśli chcesz zbudować coś podobnego — [[09-getting-started|strona 09]] pokazuje jak uruchomić LLaMEA w 5 minut.

---

**Referencje:**

[[1]] van Stein & Bäck, *LLaMEA: A Large Language Model Evolutionary Algorithm for Automatically Generating Metaheuristics*, arXiv:2405.20132, 2024

[[2]] Niki van Stein, *LLaMEA: Combining the Power of Evolution and Large Language Models*, blog post, 2024

[[3]] LIACS XAI Group, *LLaMEA — Natural Computing Group*, https://naco.liacs.nl/projects/2024-llamea/
