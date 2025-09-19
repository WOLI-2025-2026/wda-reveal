# BHP na sali, zasady oceniania, wprowadzenie do algorytmów  
<span class="badge">Lekcja 1</span>

--

## Zasady BHP w czasie zajęć

- **Sala komputerowa**  
  - Pracujemy na wyznaczonych stanowiskach.  
  - Utrzymujemy porządek przy stanowisku.  
  - Przewody zasilające **nie mogą** leżeć na przejściach.

- **Jedzenie i picie**  
  - Picie poza stanowiskami roboczymi, jedzenie niewskazane w czasie zajęć.
  - Nic płynnego przy klawiaturze/komputerze.

- **Wyjścia do toalety**  
  - Informujemy prowadzącego, że wychodzimy – *nie pytamy* (krótki komunikat wystarczy).

- **Elektryka**  
  - Uważamy przy **podłączaniu/odłączaniu** urządzeń – grozi porażeniem.  
  - W razie porażenia <span class="danger">nie dotykamy</span> osoby gołymi rękami – używamy **izolatora** (np. drewno/plastik).

</div>

--

## BHP: sytuacje awaryjne
- Pożar/dym/awaria: **najpierw** odłączamy zasilanie _(o ile bezpieczne)_, **alarmujemy** grupę i prowadzącego.  
- Złe samopoczucie, nagłe problemy: **niezwłocznie informujemy** prowadzącego.

--

## Zasady oceniania
- **2 sprawdziany** z części WDA.  
- Możliwe **kartkówki / wejściówki**.  
- **Aktywność** na zajęciach wpływa na ocenę.

--

## Wprowadzenie do algorytmów
1. Definicje.  
2. Metody reprezentacji algorytmów.  
3. Złożoność obliczeniowa i pamięciowa.  
4. Realizacja w języku C++.

--

## Definicja: algorytm
**Algorytm** to _dobrze zdefiniowana, skończona procedura_, która dla danych wejściowych w _ograniczonej liczbie kroków_ wytwarza wynik/rozwiązanie problemu.  
<span class="small muted">Źródło: ujęcia encyklopedyczne (np. Britannica) oraz CLRS.</span>

--

## Metody reprezentacji algorytmów
<div class="grid-cols">
<div class="box">

### 1) Lista kroków
Prosty opis w języku naturalnym, numerowane kroki.

</div>
<div class="box">

### 2) Schemat blokowy
Diagram bloków i przepływu sterowania (strzałki).

</div>
<div class="box">

### 3) Pseudokod
Uproszczony zapis „jak kod”, bez składni konkretnego języka.

</div>
<div class="box">

### 4) Kod źródłowy
Implementacja w języku programowania (np. C++).

</div>
</div>

--

## Zmienne w schematach blokowych

- **Zmienne** to symbole (np. `x`, `n`, `suma`), które przechowują dane wykorzystywane w algorytmie.  
- W schematach blokowych zmienne pojawiają się w:
  - **blokach wejścia/wyjścia** – np. *Wczytaj `n`*, *Wypisz `suma`*,
  - **blokach przetwarzania** – np. *suma = suma + n*, *i = i + 1*,
  - **blokach decyzyjnych** – np. *czy `n > 0`?*.

--

### Zasady użycia zmiennych

- Nadajemy zmiennym **jasne nazwy**, które wskazują ich rolę (np. `max`, `licznik`).  
- W bloku **przetwarzania** zapisujemy operacje arytmetyczne lub przypisania.

--

## Schematy blokowe — podstawowe bloki
<div class="grid-cols">

<div class="box" style="text-align:center">

### Start / Stop  
<svg width="160" height="80">
  <ellipse cx="80" cy="40" rx="70" ry="30" fill="#121317" stroke="#5f6b7a" stroke-width="2"/>
  <text x="80" y="45" text-anchor="middle" fill="#eaeaea" font-size="18" font-family="sans-serif">Start</text>
</svg>

</div>

<div class="box" style="text-align:center">

### Wejście / Wyjście  
<svg width="160" height="80">
  <polygon points="20,20 140,20 120,60 0,60" fill="#121317" stroke="#5f6b7a" stroke-width="2"/>
  <text x="80" y="45" text-anchor="middle" fill="#eaeaea" font-size="16" font-family="sans-serif">Dane</text>
</svg>

</div>

<div class="box" style="text-align:center">

### Przetwarzanie  
<svg width="160" height="80">
  <rect x="20" y="20" width="120" height="40" rx="6" ry="6" fill="#121317" stroke="#5f6b7a" stroke-width="2"/>
  <text x="80" y="45" text-anchor="middle" fill="#eaeaea" font-size="16" font-family="sans-serif">Oblicz</text>
</svg>

</div>

<div class="box" style="text-align:center">

### Decyzja  
<svg width="160" height="80">
  <polygon points="80,10 150,40 80,70 10,40" fill="#121317" stroke="#5f6b7a" stroke-width="2"/>
  <text x="80" y="45" text-anchor="middle" fill="#eaeaea" font-size="16" font-family="sans-serif">Tak/Nie?</text>
</svg>

</div>

</div>


--

## Przykład: parzystość liczby
<div class="grid-cols">
<div class="box">

### Lista kroków
1. Wczytaj liczbę `n`.  
2. Jeśli `n % 2 == 0` → powiększ o 1 i wypisz „parzysta”.  
3. W przeciwnym pomniejsz o 1 razie wypisz „nieparzysta”.  
4. Zakończ.

</div>
<div class="box">

### Schemat blokowy (SVG)
![Schemat blokowy](media/schemat1.png)


--

## Zadanie 1
Narysuj schemat blokowy, który:
 - wczytuje dwie liczby,
 - oblicza ich sumę i różnicę,
 - wypisuje wyniki. 

--

## Zadanie 2
Narysuj schemat blokowy, który:
 - wczytuje dwie liczby,
 - wyświetla więszką z nich.

--

## Zadanie 2.1
Narysuj schemat blokowy, który:
 - wczytuje trzy liczby,
 - wyświetla największą z nich.

--

## Zadanie 2.2
Narysuj schemat blokowy, który:
 - wczytuje `n` liczb,
 - wyświetla największą z nich.

--

## Zadanie 3

Narysuj schemat blokowy, który:
- wczytuje `n` liczb,  
- wyświetla największą z nich.

https://pl.wikipedia.org/wiki/Ci%C4%85g_Fibonacciego

--

## Zmienne tablicowe (tablice) w schematach blokowych

- **Tablica** to zmienna złożona, która przechowuje wiele wartości tego samego typu.  
- Dostęp do elementu tablicy następuje przez **indeks**:  
  - np. `A[0]`, `A[1]`, …, `A[n-1]`.  
- W schematach blokowych tablice pojawiają się głównie w:
  - **blokach wejścia** – np. *Wczytaj A[ i ]* w pętli,  
  - **blokach przetwarzania** – np. *suma = suma + A[ i ]*,  
  - **blokach decyzyjnych** – np. *czy A[ i ] > max ?*.

--

## Zadanie 4

Narysuj schemat blokowy, który:
- wczytuje `n` liczb,  
- liczy średnią arytmetyczną podanych liczb.

--

## Zadanie 4.1

Narysuj schemat blokowy, który:
- wczytuje `n` liczb,  
- liczy średnią arytmetyczną podanych liczb.

UWAGA ! Nie bez korzystania z tablicy.

--

## Zadanie 5

Narysuj schemat blokowy, który:
- wczytuje `n` liczb i zapisuje je w tablicy,
- sortuje tablicę zgodnie algorytmem sortowania bąbelkowego.

https://pl.wikipedia.org/wiki/Sortowanie_b%C4%85belkowe




