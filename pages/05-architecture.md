# Architektura Systemu: Moduły i Przepływ Danych

LLaMEA to nie jedna klasa Pythona — to **zintegrowany system** z kilkoma kluczowymi komponentami. Poznanie architektury pomoże ci zarówno zrozumieć jak działa, jak i jak je rozszerzać.

## Architektura wysokiego poziomu

```
┌──────────────────────────────────────────────────────────────┐
│                      LLaMEA Framework                        │
│                                                              │
│  ┌─────────────┐     ┌─────────────┐     ┌──────────────┐   │
│  │ LLM Module  │────▶│   Core EA   │────▶│  Evaluator   │   │
│  │ (GPT-4/     │     │  Loop       │     │  (IOHexp.)   │   │
│  │  OpenAI)    │     │             │     │              │   │
│  └─────────────┘     └─────────────┘     └──────────────┘   │
│         ▲                  │                     │           │
│         │                  │                     ▼           │
│         │                  │            ┌──────────────┐   │
│         └──────────────────┘            │   BBOB        │   │
│              feedback loop             │   Benchmark    │   │
│                                       └──────────────┘   │
└──────────────────────────────────────────────────────────────┘
```

## Komponent 1: Moduł LLM

**Interfejs:** `llamea/llm.py`

Obsługuje komunikację z LLM (GPT-4, GPT-3.5-turbo, lub modele lokalne przez OpenAI-compatible API) [[1]]([[1]])[[2]]([[2]]).

Funkcje:
- Wysyłanie promptów z opisem problemu
- Parsowanie wygenerowanego kodu Python
- Obsługa błędów (gdy LLM generuje nieprawidłowy kod)
- Zarządzanie kosztami API

```python
# Uproszczony interfejs z dokumentacji [[3]]([[3]])
from llamdea import LLaMEA, OpenAI_LLM

llm = OpenAI_LLM(model="gpt-4")
optimizer = LLaMEA(llm=llm, problem=problem)
best_algorithm = optimizer.run()
```

## Komponent 2: Rdzeń EA (Evolutionary Algorithm)

**Interfejs:** `llamea/llamea.py` + `llamea/solution.py`

Implementuje standardową pętlę ewolucyjną [[1]]([[1]]):
- Reprezentacja osobnika: kod algorytmu (string) + metryki fitness
- Selekcja: elitarny wybór najlepszych
- Mutacja: LLM generuje warianty
- Historia: śledzenie najlepszych osobników

## Komponent 3: Evaluator (IOHexperimenter)

**Interfejs:** `benchmarks/ma_bbob/run_mabbob.py`

Automatyczne uruchamianie algorytmów na benchmarku BBOB [[1]]([[1]])[[4]]([[4]]):
- Łączy się z IOHprofiler
- Uruchamia algorytm na 24 funkcjach testowych
- Zbiera metryki: przebieg zbieżności, wartości końcowe
- Generuje statystyki porównawcze (vs CMA-ES, DE)

## Komponent 4: Solution Management

**Interfejs:** `llamea/solution.py`

Zarządza osobnikami w populacji:
- Przechowywanie kodu wygenerowanego algorytmu
- Metryki fitness (z IOHexperimenter)
- Metadane: timestamp, numer generacji, parent ID

## Przepływ danych w jednej iteracji

```
1. LLM.generate(prompt, context)
         ↓ (wygenerowany kod Pythona)
2. Validate(code) → syntax check
         ↓ (jeśli OK)
3. IOHexperimenter.run(code, problem)
         ↓ (metryki fitness)
4. Solution.create(code, fitness, generation)
         ↓
5. EA.selection(solutions) → best + mutation candidates
         ↓
6. LLM.mutate(best_candidates) → goto 1
```

## Struktura katalogów projektu

```
LLaMEA/
├── LlamEA/              # Główny pakiet Pythona
│   ├── __init__.py
│   ├── llamdea.py       # Core EA loop
│   ├── llm.py           # LLM interface
│   ├── solution.py      # Solution representation
│   └── ...
├── benchmarks/
│   └── ma_bbob/
│       └── run_mabbob.py  # BBOB runner
├── tests/               # Testy jednostkowe
├── README.md
└── requirements.txt
```

Według [[3]]([[3]]) projekt jest w pełni open-source (MIT License).

## Konfiguracja eksperymentu

LLaMEA pozwala na konfigurację [[1]]([[1]])[[3]]([[3]]):
- **LLM provider:** OpenAI (GPT-4), Azure, lub lokalny przez OpenAI-compatible API
- **Budget:** maksymalna liczba ewaluacji / pokoleń
- **Population size:** rozmiar populacji algorytmów
- **Selection mechanism:** jaki algorytm selekcji (elitarny, tournament)
- **Mutation rate:** jak często LLM generuje warianty vs. losowe nowe

---

**Następna strona:** [[06-bbob-benchmark]] — jak mierzymy jakość algorytmu
