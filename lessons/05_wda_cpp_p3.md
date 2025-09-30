# Tablice jednowymiarowe – statyczne (C++)

Tablica to struktura danych pozwalająca przechować wiele elementów określonego typu. W praktyce można też ją zdefiniować jako zbiór **indeksowanych** zmiennych tego samego typu. Tablicę w C++ deklaruje się przez podanie typu, nazwy i rozmiaru:

`typ_zmiennej nazwa_zmiennej[rozmiar_tablicy];`

np.

```cpp
int a[5]; // 5-elementowa tablica liczb całkowitych
```

--

Taki zapis tworzy tablicę typu `int` o rozmiarze 5, czyli pięć kolejnych w pamięci elementów, do których można się dostać za pomocą `a[0]`, `a[1]`, `a[2]`, `a[3]`, `a[4]`. Warto zauważyć, że ostatni element n-elementowej tablicy ma indeks `n-1`, ponieważ indeksowanie zaczyna się od 0.

| `a[0]` | `a[1]` | `a[2]` | `a[3]` | `a[4]` |
| :----: | :----: | :----: | :----: | :----: |

--

**Ważne (C++):** rozmiar **statycznej** tablicy musi być **stałą wyrażalną w czasie kompilacji** (*constant expression*). W C++ możesz użyć np.:

```cpp
constexpr int N = 5; // albo: const int N = 5;
int a[N];            // OK w C++
```

Natomiast **zwykła zmienna** ustalana w trakcie działania programu nie może być rozmiarem tablicy statycznej.

--

Aby odwołać się do elementu tablicy, podajemy jej indeks (typu całkowitego). Na elementach tablicy można wykonywać te same operacje co na zwykłych zmiennych:

```cpp
a[0] = 0;               // do pierwszego elementu tablicy
int i = 4;
a[i] = 3;               // do i-tego (tu: piątego) elementu tablicy
```

--

Szczególnie wygodne jest łączenie tablic z pętlami – zmienna sterująca pętli może służyć jako indeks.

*Przykład (8.0) Wczytanie i wypisanie wartości do tablicy za pomocą pętli (C++):*

```cpp
#include <iostream>
using namespace std;

int main() {
    int tablica[5];

    for (int i = 0; i < 5; i++) {
        cout << "Podaj element tablicy o indeksie " << i << ": ";
        cin >> tablica[i];
    }
    for (int i = 0; i < 5; i++) {
        cout << "tablica[" << i << "] = " << tablica[i] << '\n';
    }
    return 0;
}
```

--

--

## Sposoby przypisania do tablicy wartości początkowych

Deklarując tablicę można zainicjować jej początkowe wartości, podając je w nawiasach klamrowych po operatorze `=`. Elementy pominięte zostaną **wyzerowane**.

--

**(8.1)** Wszystkie wartości podane jawnie:

```cpp
int a[5] = { 0, 1, 5, 8, 0 };
// |0|1|5|8|0|
```

--

**(8.2)** Wybrane pozycje – w C++ robimy to dwuetapowo:

```cpp
int a[10] = {0}; // wyzeruj całą tablicę
a[3] = 4;
a[4] = 1;
a[5] = 5;
a[9] = 3;
// |0|0|0|4|1|5|0|0|0|3|
```

--

**(8.3)** Szybkie wyzerowanie całej tablicy:

```cpp
int a[10] = {0}; // wszystkie elementy = 0
// |0|0|0|0|0|0|0|0|0|0|
```

--

**(8.4)** Pominięcie rozmiaru – rozmiar zostanie wywnioskowany z liczby elementów:

```cpp
int a[] = {1, 5, 8, 0};
// |1|5|8|0|
```

--

## Tworzenie funkcji obsługujących tablice

(Wyjaśnienie „dlaczego to działa” – wskaźniki, przekazywanie tablic i pamięć – będzie w dalszych rozdziałach. Tu skupiamy się na praktyce.)

Aby funkcja operowała na tablicy, w parametrach podajemy **tablicę** (która w nagłówku funkcji „degraduje” do wskaźnika) **oraz jej rozmiar** – to zabezpiecza przed wyjściem poza zakres. Zmiany na takim parametrze tablicowym **wpływają na oryginalną tablicę**.

--

*Przykład (8.5) funkcje operujące na tablicy (C++):*

```cpp
#include <iostream>
using namespace std;

void print_array(const int array[], int size);
void scan_array(int array[], int size);

int main() {
    int tab[5];
    scan_array(tab, 5);
    print_array(tab, 5);
    return 0;
}

void print_array(const int array[], int size) {
    if (size > 0) {
        for (int i = 0; i < size; i++) {
            cout << "tablica[" << i << "] = " << array[i] << '\n';
        }
    }
}

void scan_array(int array[], int size) {
    if (size > 0) {
        for (int i = 0; i < size; i++) {
            cout << "Podaj element tablicy o indeksie " << i << ": ";
            cin >> array[i];
        }
    }
}
```

--

*Wynik działania programu (identyczny jak w przykładzie 8.0):*

```
Podaj element tablicy o indeksie 0:1
Podaj element tablicy o indeksie 1:2
Podaj element tablicy o indeksie 2:3
Podaj element tablicy o indeksie 3:4
Podaj element tablicy o indeksie 4:5
tablica[0] = 1
tablica[1] = 2
tablica[2] = 3
tablica[3] = 4
tablica[4] = 5
```

--

## Zadania do samodzielnego wykonania

1. Zadeklaruj tablicę jednowymiarową wybranymi wartościami (w kodzie). Następnie **wyświetl** zawartość tej tablicy za pomocą pętli `for`, `while` i `do…while`, tworząc odpowiednie funkcje:

   * od początku do końca,
   * od końca do początku.
2. Napisz program, który wczytuje do tablicy 10 liczb podanych przez użytkownika, a następnie – dzieląc program na funkcje – realizuje:

   * podanie średniej arytmetycznej,
   * wypisanie wszystkich liczb większych od średniej,
   * wypisanie najmniejszej oraz największej liczby,
   * sumę wszystkich elementów o wartościach **nieparzystych**,
   * wypisanie tablicy od ostatniego elementu.

--

3. Napisz program, który będzie na **tablicy statycznej** obsługiwał działanie kolejki:

   * FIFO,
   * LIFO.
4. Napisz program, który wczyta od użytkownika tablicę 10-elementową, a następnie posortuje ją algorytmem [sortowania bąbelkowego](https://pl.wikipedia.org/wiki/Sortowanie_b%C4%85belkowe). Stwórz funkcję `bubble_sort()`.

--

5. Napisz program, który wczyta od użytkownika tablicę 10-elementową, a następnie posortuje ją algorytmem [merge sort](https://pl.wikipedia.org/wiki/Sortowanie_przez_scalanie). Stwórz funkcję `merge_sort()`.
6. Napisz program, który wczyta od użytkownika tablicę 10-elementową, a następnie posortuje ją algorytmem [quick sort](https://pl.m.wikipedia.org/wiki/Sortowanie_szybkie). Stwórz funkcję `quick_sort()`.


