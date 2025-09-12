# WDA — start zajęć
BHP na sali, zasady oceniania, wprowadzenie do algorytmów  
<span class="badge">Lekcja 1</span>

---

## Zasady BHP w czasie zajęć
<div class="grid-cols">
<div class="box">

### Sala komputerowa
- Pracujemy **na wyznaczonych stanowiskach**.  
- Utrzymujemy porządek przy stanowisku.  
- Przewody zasilające <span class="warn">nie mogą</span> leżeć na przejściach.

</div>
<div class="box">

### Jedzenie i picie
- **Poza stanowiskami roboczymi** – napoje i jedzenie w wyznaczonym miejscu.  
- Nic płynnego przy klawiaturze/komputerze.

</div>
<div class="box">

### Wyjścia do toalety
- **Informujemy** prowadzącego, że wychodzimy – _nie pytamy_ (krótki komunikat wystarczy).

</div>
<div class="box">

### Elektryka
- Uważamy przy **podłączaniu/odłączaniu** urządzeń – grozi porażeniem.  
- W razie porażenia <span class="danger">nie dotykamy</span> osoby gołymi rękami – używamy **izolatora** (np. drewno/plastik).

</div>
</div>

---

## BHP: sytuacje awaryjne
- Pożar/dym/awaria: **najpierw** odłączamy zasilanie _(o ile bezpieczne)_, **alarmujemy** grupę i prowadzącego.  
- Złe samopoczucie, nagłe problemy: **niezwłocznie informujemy** prowadzącego.

---

## Zasady oceniania
- **2 sprawdziany** z części WDA.  
- Możliwe **kartkówki / wejściówki**.  
- **Aktywność** na zajęciach wpływa na ocenę.

---

## Wprowadzenie do algorytmów
1. Definicje.  
2. Metody reprezentacji algorytmów.  
3. Złożoność obliczeniowa i pamięciowa.  
4. Realizacja w języku C++.

---

## Definicja: algorytm
**Algorytm** to _dobrze zdefiniowana, skończona procedura_, która dla danych wejściowych w _ograniczonej liczbie kroków_ wytwarza wynik/rozwiązanie problemu.  
<span class="small muted">Źródło: ujęcia encyklopedyczne (np. Britannica) oraz CLRS.</span>

---

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

---

## Schematy blokowe — podstawowe bloki
<div class="grid-cols">
<div class="box">

- **Start/Stop** — owal.  
- **Wejście/Wyjście** — równoległobok.  
- **Przetwarzanie** — prostokąt.  
- **Decyzja** — romb (tak/nie).

</div>
<div class="box">

- **Łącznik** — małe kółko/znacznik.  
- **Proces wstępnie zdef.** — podproces.  
- **Dokument** — wygięty prostokąt.  
- **Strzałki** — kierunek przepływu.

</div>
</div>

---

## Przykład: parzystość liczby
<div class="grid-cols">
<div class="box">

### Lista kroków
1. Wczytaj liczbę `n`.  
2. Jeśli `n % 2 == 0` → wypisz „parzysta”.  
3. W przeciwnym razie wypisz „nieparzysta”.  
4. Zakończ.

</div>
<div class="box">

### Schemat blokowy (SVG)
<!-- surowe HTML jest dozwolone w Markdown Reveal -->
<svg class="flow" viewBox="0 0 820 520" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Schemat blokowy: sprawdzanie parzystości">
  <defs>
    <style>
      .blk{ fill:#121317; stroke:#5f6b7a; stroke-width:2; rx:16; ry:16 }
      .txt{ fill:#eaeaea; font-family: Inter, Arial, sans-serif; font-size:20px }
      .edge{ stroke:#8aa3bf; stroke-width:2; fill:none; marker-end:url(#arr) }
      .par{ font-weight:700; fill:#abf7b1 }
      .nie{ font-weight:700; fill:#ffb3b3 }
    </style>
    <marker id="arr" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="8" markerHeight="8" orient="auto-start-reverse">
      <path d="M 0 0 L 10 5 L 0 10 z" fill="#8aa3bf"/>
    </marker>
  </defs>
  <ellipse cx="410" cy="50" rx="90" ry="30" stroke="#5f6b7a" stroke-width="2" fill="#121317"/>
  <text x="410" y="55" text-anchor="middle" class="txt">Start</text>
  <polygon points="300,120 520,120 560,160 260,160" stroke="#5f6b7a" stroke-width="2" fill="#121317"/>
  <text x="410" y="148" text-anchor="middle" class="txt">Wczytaj n</text>
  <polygon points="410,200 540,260 410,320 280,260" stroke="#5f6b7a" stroke-width="2" fill="#121317"/>
  <text x="410" y="265" text-anchor="middle" class="txt">n % 2 == 0?</text>
  <rect x="90" y="380" width="260" height="60" class="blk"/>
  <text x="220" y="415" text-anchor="middle" class="txt par">Wypisz: parzysta</text>
  <rect x="470" y="380" width="260" height="60" class="blk"/>
  <text x="600" y="415" text-anchor="middle" class="txt nie">Wypisz: nieparzysta</text>
  <ellipse cx="410" cy="490" rx="90" ry="30" stroke="#5f6b7a" stroke-width="2" fill="#121317"/>
  <text x="410" y="495" text-anchor="middle" class="txt">Stop</text>
  <path d="M410,80 L410,120" class="edge"/>
  <path d="M410,160 L410,200" class="edge"/>
  <path d="M280,260 C240,260 220,300 220,380" class="edge"/>
  <path d="M540,260 C580,260 600,300 600,380" class="edge"/>
  <path d="M220,440 C220,470 320,490 410,490" class="edge"/>
  <path d="M600,440 C600,470 500,490 410,490" class="edge"/>
</svg>

</div>
</div>

---

## Złożoność algorytmów
<div class="grid-cols">
<div class="box">

### Czas (Big-O)
- `O(1)` — stały.  
- `O(log n)` — logarytmiczny.  
- `O(n)` — liniowy.  
- `O(n log n)` — np. sortowania szybkie/merge.  
- `O(n²)`, `O(2^n)` — kosztowne.

</div>
<div class="box">

### Pamięć
- Dodatkowa pamięć (np. tablice pomocnicze).  
- Rekurencja → stos wywołań.  
- W praktyce: kompromis czas ⟷ pamięć.

</div>
</div>

---

## Realizacja w języku C++
```cpp
#include <iostream>
using namespace std;

int main(){
  long long n; cout << "Podaj n: ";
  if(!(cin >> n)) return 0;
  if(n % 2 == 0) cout << "parzysta\n";
  else           cout << "nieparzysta\n";
  return 0;
}
