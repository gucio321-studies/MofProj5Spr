# Cel ćwiczenia

Celem ćwiczenia było rozwiązanie równania Poissona w dwuwymiarowej, uziemionej na brzegach przestrzeni.
W niniejszym cœiczeniu wykorzystano różne metody numeryczne rozwiązania:
- minimalizacji funkcjonału energii,
- optymalizacji gradientowej,
- metody Monte Carlo.

# Aparatura i metodyka wykonania

W ramach eksperymentu (Prove of concept) kod do symulacji i prezentacji wynikóœ wykonano w języku [Go](https://go.dev).
Do prezentacji wykorzystano biblioteke [giu](https://github.com/AllenDang/giu) (framework [Dear ImGui](https://github.com/ocornut/imgui)).

# Wyniki pomiarów

## Minimalizacja bezpośrednia

Najpierw wykonano minimalizację bezpośrednio wartości $S_{loc}$.
W tym celu w każdej iteracji zmieniano wartość $u(i, j)$ o jedną z wartości $\delta \in \left\{0, 0.5, 1, \frac{1}{4}\frac{3 S_1 - 4S_2 + S_3}{S_1 - 2S_2 + S_3}\right\}$ tak,
aby uzyskać jak najmniejszą wartosć $S_i$ (gdzie $S_i = S(\delta_i)$).

Uzyskano następującą zależność wartości $S$ od numeru iteracji:

```{figure} ./01.png
Zależność S od numeru iteracji dla minimalizacji bespośredniej S.
```

Po ostatniej iteracji otrzymano następujący rozkład wartości $u(i, j)$

```{figure} ./02.png
Rozkłąd $u(i, j)$ po minimalizacji bezpośredniej S.
```


## Porównanie wydajności czasowej poszczegulnych metod

| Operacja | Czas wykonania [ms] |
| --- | --- |
| Minimalizacja bezpośrednia funkcjonału S | 1.275s |
| Task 2, $\beta = 0.1$ | 0.4842s |
| Task 2, $\beta = 0.3$ | 0.4812s |
| Task 2, $\beta = 0.4$ | 0.4665s |
| Task 2, $\beta = 0.49$ | 0.5196s |
| Task 2 (total) | 1.952s |
| Task 3 | 0.5409s |

# Obliczenia

# Szacowanie niepewności

# Podsumowanie

# Literatura

- prof. dr hab. inż. Wojciech Łużny - Kurs Mechaniki.
