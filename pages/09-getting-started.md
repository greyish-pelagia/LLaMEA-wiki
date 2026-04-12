# Pierwsze Kroki: Instalacja i Uruchomienie LLaMEA

Ta strona pokazuje jak w 5 minut uruchomić LLaMEA na własnym komputerze. Zakładam że masz Pythona 3.9+ i API key do OpenAI (lub kompatybilny endpoint).

## Wymagania wstępne

1. **Python 3.9+**
2. **API key OpenAI** (lub inny LLM provider przez OpenAI-compatible API)
3. **IOHprofiler** (do ewaluacji na BBOB)
4. **~10 GB** miejsca na dane benchmarkowe

## Instalacja

### Opcja 1: z PyPI (najszybsza)

```bash
pip install llamda
```

To zainstaluje główny pakiet. Uwaga: IOHprofiler może wymagać osobnej instalacji [[1]]([[1]]).

### Opcja 2: ze źródeł (pełna kontrola)

```bash
git clone https://github.com/XAI-liacs/LLaMEA
cd LLaMEA
pip install -e .
```

Wersja ze źródeł daje dostęp do przykładów w `examples/`.

## Konfiguracja API key

```bash
export OPENAI_API_KEY="sk-..."
```

Lub w kodzie:

```python
import os
os.environ["OPENAI_API_KEY"] = "sk-..."
```

## Minimalny przykład

```python
from llamdea import LLaMEA
from llamdea.llm import OpenAI_LLM
from llamdea.problems import BBOBProblem

# 1. Inicjalizacja LLM
llm = OpenAI_LLM(model="gpt-4")

# 2. Definicja problemu
problem = BBOBProblem(function_id=1, dimension=5)

# 3. Inicjalizacja LLaMEA
optimizer = LLaMEA(
    llm=llm,
    problem=problem,
    max_iterations=50,
    population_size=10
)

# 4. Uruchomienie
best_solution = optimizer.run()

# 5. Wynik
print(f"Najlepszy algorytm: {best_solution.code}")
print(f"Wartość fitness: {best_solution.fitness}")
```

## Struktura kodu — co gdzie jest

```
llamea/
├── __init__.py           # Główny eksport: LLaMEA
├── llamdea.py            # Core loop (generacja → ewaluacja → selekcja)
├── llm.py                # Abstrakcja LLM (OpenAI, Azure, local)
├── solution.py           # Reprezentacja osobnika (algorytm + fitness)
├── problems/             # Definicje problemów
│   ├── __init__.py
│   └── bbob.py           # BBOB wrapper
└── utils/
    └── logging.py        # Śledzenie ewolucji
```

## Typowe problemy i rozwiązania

### Problem: "ModuleNotFoundError: No module named 'llamda'"

Rozwiązanie: Upewnij się że installacja przebiegła poprawnie:
```bash
pip install --force-reinstall llamda
```

### Problem: "Invalid API key" lub "Rate limit exceeded"

Rozwiązanie: Sprawdź swój API key i ewentualnie ustaw billing na OpenAI. Dla produkcji rozważ local LLM (via Ollama) lub Azure OpenAI.

### Problem: "IOHprofiler not found"

Rozwiązanie: IOHprofiler wymaga osobnej instalacji:
```bash
pip install IOHexperimenter
```

### Problem: "Generated code has syntax error"

To **normalne** — LLM czasem generuje kod który nie działa. LLaMEA ma wbudowaną walidację i retries. Jeśli problem się powtarza, spróbuj prostszego promptu.

## Konfiguracja zaawansowana

```python
optimizer = LLaMEA(
    llm=llm,
    problem=problem,
    
    # Evolutionary parameters
    max_iterations=100,      # Liczba pokoleń
    population_size=20,       # Rozmiar populacji
    elite_size=3,             # Elita (najlepsze bez zmian)
    mutation_rate=0.3,        # Prawdopodobieństwo mutacji
    
    # LLM parameters  
    temperature=0.7,         # Kreatywność LLM
    max_retries=3,           # Retry przy błędzie kodu
    
    # Budget
    max_evaluations=10000,   # Maksymalna liczba ewaluacji
    
    # Callback
    logger=my_logger         # Śledzenie postępu
)
```

## Przydatne zasoby

| Zasób | URL |
|-------|-----|
| GitHub (XAI-liacs) | https://github.com/XAI-liacs/LLaMEA |
| GitHub (nikivanstein) | https://github.com/nikivanstein/LLaMEA |
| Dokumentacja | https://xai-liacs.github.io/LLaMEA/ |
| PyPI | https://pypi.org/project/llamea/ |
| ArXiv Paper | https://arxiv.org/abs/2405.20132 |
| Niki's Blog | https://www.nikivanstein.nl/posts/2024/07/llamea/ |

## Następne kroki

1. Uruchom przykład z `examples/basic_bbob.py` w repozytorium
2. Spróbuj różnych modeli LLM (GPT-4 vs GPT-3.5 vs lokalne)
3. Eksperymentuj z parametrami populacji i selekcji
4. Spróbuj własnego problemu optymalizacyjnego (dziedzicz `Problem` class)

## Disclaimer

Koszt GPT-4 API może być znaczący przy wielu iteracjach. Pilnuj limitów i rozważ modele lokalne (Ollama + Llama 3) dla eksperymentów developmentowych.
