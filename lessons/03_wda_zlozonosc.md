# Złożoność algorytmów

--

## Złożonośc algorytmów

- **Złożoność czasowa** – jak liczba operacji (czas wykonania) rośnie wraz ze wzrostem rozmiaru danych wejściowych `n`.  
- **Złożoność pamięciowa** – jak dużo pamięci potrzebuje algorytm w zależności od `n`.

--

### Notacja O(n)

- **Duże O** (np. `O(n)`) opisuje *górne ograniczenie* – czyli jak szybko rośnie czas/pamięć w **najgorszym przypadku**.  
- Przykłady:
  - `O(1)` – czas stały, niezależny od danych,  
  - `O(n)` – czas liniowy, proporcjonalny do rozmiaru danych,  
  - `O(n²)` – czas kwadratowy, rośnie szybko przy dużych `n`.

--

### Przykłady notacji

- `O(1)` – dostęp do elementu tablicy.  
- `O(n)` – przeszukiwanie liniowe.  
- `O(n log n)` – szybkie sortowanie, mergesort.  
- `O(n²)` – sortowanie bąbelkowe, sortowanie przez wstawianie.  
- `O(2^n)` – przeszukiwanie wszystkich podzbiorów.  
- `O(n!)` – pełna permutacja elementów.

--

<img src="media/wykrez-zlozonosc.png" alt="Schemat blokowy" class="small-img">
https://pl.wikipedia.org/wiki/Asymptotyczne_tempo_wzrostu

--


## Analiza złożoności — sortowanie bąbelkowe

Algorytm sortowania bąbelkowego:

1. Powtarzaj `n-1` razy:  
   - Dla każdej pary sąsiednich elementów `A[i]` i `A[i+1]`:  
     - Jeśli są w złej kolejności → zamień.

--

### Krok 1: policzmy liczbę porównań

- **Pętla zewnętrzna**: wykonuje się `n-1` razy.  
- **Pętla wewnętrzna**:  
  - I przebieg: ~`n-1` porównań  
  - II przebieg: ~`n-2` porównań  
  - …  
  - Ostatni: 1 porównanie  

Łącznie:  
$$(n-1) + (n-2) + \dots + 1 = \frac{n(n-1)}{2}$$

--

### Krok 2: porządkujemy wynik

- Suma $\frac{n(n-1)}{2}$ jest **równa** około $\frac{n^2}{2} - \frac{n}{2}$.  
- Przy analizie asymptotycznej pomijamy stałe i składniki niższego rzędu.  

➡️ Otrzymujemy:  
**złożoność czasowa = O(n²)**

--

### Krok 3: policzmy operacje dodatkowe

- Każda zamiana = 3 operacje przypisania.  
- W najgorszym przypadku zamian może być tyle, co porównań.  
- Mimo to **rząd wielkości** nadal jest $O(n^2)$.

--

### Krok 4: złożoność pamięciowa

- Tablica `A` (n elementów) → traktujemy jako dane wejściowe.  
- Algorytm potrzebuje tylko **jednej zmiennej pomocniczej** do zamiany wartości.  

➡️ **złożoność pamięciowa = O(1)**

--

### Podsumowanie (sortowanie bąbelkowe)

- **Złożoność czasowa**: $O(n^2)$ w najgorszym i średnim przypadku, $O(n)$ w najlepszym (już posortowane dane).  
- **Złożoność pamięciowa**: $O(1)$ — działa w miejscu.  
- W praktyce: bardzo nieefektywny dla dużych `n`, wykorzystywany głównie w celach dydaktycznych.



