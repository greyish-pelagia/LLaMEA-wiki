# Badania Powiązane: Automatyczne Generowanie Benchmarków i Samokontrola LLM

LLaMEA nie jest izolowanym projektem — wpisuje się w szerszy trend **automatyzacji projektowania algorytmów i systemów LLM**. Ta strona pokazuje kontekst i pokrewne prace.

## Obszar 1: Automatyczne generowanie benchmarków optymalizacyjnych

### ArXiv 2601.12723: Evolutionary Framework for Automatic Optimization Benchmark Generation via LLMs

Praca Ono, Harada, Miura (2026) [^1] — bardzo bliska tematycznie do LLaMEA:

> Systematycznie pokazuje jak LLM może nie tylko generować algorytmy, ale też **generować nowe funkcje benchmarkowe**.

To drugi kierunek automatyzacji — jeśli LLaMEA automatyzuje projektowanie algorytmów, to ta praca automatyzuje projektowanie **problemów testowych**.

### ArXiv 2604.06973: Block-Bench

Ye, Neumann, Bäck, van Stein (2026) [^2]:

> Framework do **kontrolowanego i transparentnego benchmarkowania optymalizacji dyskretnej**.

Block-Bench to metologia benchmarkowania — nie generuje benchmarków LLM-em, ale dostarcza **struktury** do systematycznego porównywania algorytmów na problemach kombinatorycznych.

## Obszar 2: Reasoning i weryfikacja w LLM Agents

### ArXiv 2604.08401: Verify Before You Commit

Yuan et al. (2026) [^3] — ważne dla zrozumienia **ograniczeń LLM**:

> LLM agents często propagują **niewiarygodne przekonania pośrednie** przez długie sekwencje decyzyjne.

Problem: w pętli LLaMEA, LLM generuje kod algorytmu. Czy można mu **ufać** że kod będzie poprawny? Verify Before You Commit pokazuje techniki **self-auditing** — LLM sprawdza własne rezonowanie zanim wykona akcję.

Dla LLaMEA to bezpośrednio istotne: jeśli LLM źle zinterpretuje feedback z benchmarku, może mutować w złym kierunku.

## Obszar 3: Fine-tuning LLM dla reasoning agents

Źródła [^4] opisują podejście:

> Fine-tuning mniejszych modeli (LLaMA 3.2-3B) na reasoning-specific datasets dla zadań matematycznych i kodowych.

To potencjalnie relevantne dla LLaMEA — czy zamiast GPT-4, można użyć fine-tuned model specjalizującego się w generowaniu kodu optymalizacyjnego?

## Obszar 4: Modularne frameworki automated design

Tradycyjne (przed-LLM) podejścia do automatycznego projektowania [^1]:
- Modularny CMA-ES (millions of module combinations)
- Modularny DE
- Modularny PSO

Wszystkie wymagają **eksperta** do zdefiniowania przestrzeni modułów. LLaMEA eliminuje to przez generowanie zupełnie nowego kodu.

## AlphaEvolve (Google DeepMind)

LLaMEA jest świadomie porównywane z AlphaEvolve [^5]:

| Cecha | AlphaEvolve | LLaMEA |
|-------|------------|--------|
| LLM | Gemini | GPT-4 |
| Kod | Zamknięty | MIT Open Source |
| Aplikacja | Matematyka, materiały | Metaheurystyki |
| Benchmark | Niestandardowy | BBOB (standard) |

LLaMEA jest **alternatywą open-source** z standardowym benchmarkiem.

## Przyszłe kierunki

Według paperu [^1]:
1. **Różne LLM** — przetestować GPT-4o, Claude, Gemini zamiast GPT-4
2. **Różne selekcje** — tournament selection, multi-objective selection
3. **Różne populacje** — większe populacje, island model
4. **Inne domeny** — nie tylko metaheurystyki, ale dowolne algorytmy
5. **Kombinatoryka** — rozszerzenie poza ciągłą optymalizację

## Dlaczego to wszystko jest spójne?

Wspólny motyw: **automatyzacja ekspertyzy algorytmicznej**. Zamiast:
- Człowieka który zna 500 metaheurystyk → LLM który je zna i generuje nowe
- Człowieka który projektuje benchmark → LLM który generuje nowe problemy
- Człowieka który weryfikuje reasoning → LLM który sam siebie sprawdza

To fundamentalna zmiana w paradygmacie: **od ekspertyzy ręcznej do ekspertyzy emergującej z LLMs**.

---

**Następna strona:** [09 — Pierwsze kroki](pages/09-getting-started) — jak uruchomić LLaMEA samodzielnie
