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

## Minimalizacja gradientowa

Można również dokonać minimalizacji S poprzez wyliczenie wartości gradientu.
Dzięki temu zamiast czterokrotnie liczyć wartości S można to zrobić tylko 2 razy.
Przyjmuje się wartość $d = 0.001$ i wylicza się wartość S dla $u(i, j) = u(i, j) \pm d$.
Nastęþnie wyznacza się wartość $\nabla S = \frac{S_+ - S_-}{2d}$ i zmniejsza się wartość $u(i, j)$ o $\beta \nabla S$.
Obliczenia wykonano dla 4 różnych wartości współczynnika $\beta \in \left\{0.1, 0.2, 0.3, 0.4, 0.49\right\}$.

Na poniższym wykresie zestawiono zależności S od numeru iteracji dla różnych wartości $\beta$ oraz minimalizacji bezpośredniej.

```{figure} ./03.png
Zależność S od numeru iteracji dla minimalizacji bezpośredniej oraz gradientowej dla różnych wartości $\beta$ oraz dla minimalizacji bezpośredniej.
```

Dla $\beta \to 0.5$ operacja jest szybciej zbierzna.
Można zaobserwować, że pomimo, żę $\beta = 0.49$ teoretycznie jest zbiega się wolniej, wartość $S$ będzie ostatecznie mniejsza niż dla $\beta=0.4$.

Poniżej przedstawiono rozkłąd $u(i, j)$ dla $\beta = 0.1$ oraz $\beta = 0.49$. Nie zamieszczono pozostałych rozkładów, ponieważ są one praktycznie identyczne jak $\beta = 0.49$.

```{figure} ./04.png
Rozkłąd $u(i, j) dla $\beta = 0.1
```

```{figure} ./05.png
Rozkłąd $u(i, j) dla $\beta = 0.49
```

Pozostałe rozkłądy mogą zostać odtworzone poprzez uruchemienie symulacji we własnym zakresie - patrz [literatura](#literatura).

## Losowa minimalizacja.

Wykonano również minimalizację losową.
W tym celu, dla wartości $r=0.1$ losowano pewną wartość liczbową z zakresu $u_0 \in \left<-r,r\right>$ następnie sprawdzano, czy wartość S
przed zmianą była większa niż po zmainie. Jeżeli tak, aplikowano zmianę.

Poniższy wykres przedstawia zależność wartośći S od numeru iteracji.

```{figure} ./06.png
Zależność wartośći S od numeru iteracji
```

## Porównanie wydajności czasowej poszczegulnych metod

| Operacja | Czas wykonania [ms] |
| --- | --- |
| Minimalizacja bezpośrednia funkcjonału S | 1.275s |
| Minimalizacja gradientowa, $\beta = 0.1$ | 0.4842s |
| Minimalizacja gradientowa, $\beta = 0.3$ | 0.4812s |
| Minimalizacja gradientowa, $\beta = 0.4$ | 0.4665s |
| Minimalizacja gradientowa, $\beta = 0.49$ | 0.5196s |
| Minimalizacja gradientowa (total) | 1.952s |
| Task 3 | 0.5409s |

# Obliczenia

# Szacowanie niepewności

# Podsumowanie

# Literatura

- MOF5 - Program symulacyjny - https://github.com/gucio321-studies/MOFProj5 rewizja 9b6f174c695dc013162dd1fa2969e6a0e9532da3
