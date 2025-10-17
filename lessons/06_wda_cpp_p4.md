# Tablice wielowymiarowe – statyczne (C++)

Tablica wielowymiarowa, podobnie jak jednowymiarowa, jest strukturą danych przechowującą wiele elementów **tego samego typu**.
W odróżnieniu od tablicy jednowymiarowej, każdy element tablicy wielowymiarowej ma **więcej niż jeden indeks** — odpowiada to współrzędnym w układzie przestrzennym.

--

## Wymiary tablic

Pojęcie wymiaru tablicy można łatwo porównać z wymiarem układu współrzędnych.
Dla przykładu:

* Tablica jednowymiarowa (`a[5]`) to linia (wektor),
* Tablica dwuwymiarowa (`a[3][3]`) to prostokąt (macierz),
* Tablica trójwymiarowa (`a[2][3][4]`) można sobie wyobrazić jako „kostkę” złożoną z bloków wartości.

Nie ma ograniczenia co do liczby wymiarów, choć w praktyce operuje się najczęściej na 2D lub 3D.

--

## Deklaracja tablicy wielowymiarowej

Deklaracja wygląda podobnie jak w przypadku tablic jednowymiarowych — po typie zmiennej i nazwie podajemy w nawiasach kwadratowych rozmiary kolejnych wymiarów.

```cpp
int a[5][5];      // tablica dwuwymiarowa 5x5
int b[2][4][2];   // tablica trójwymiarowa 2x4x2
```

Aby odwołać się do konkretnego elementu, podajemy **wszystkie indeksy**:

```cpp
a[0][0] = 1;
a[2][3] = 5;
```

--

## Reprezentacja w pamięci

Tablice wielowymiarowe są w pamięci zapisywane **ciągiem**, podobnie jak jednowymiarowe.
Dla przykładu, tablica `int a[4][5];` zostanie umieszczona w pamięci jako 20 kolejnych wartości:

```
a[0][0], a[0][1], ... a[0][4], a[1][0], ..., a[3][4]
```

Dlatego odwoływanie się do elementów spoza granic tablicy (np. `a[4][0]` przy tablicy 4x5) może prowadzić do błędów (tzw. *segmentation fault*).

--

## Przykład (10.1) – wczytywanie i wypisywanie elementów tablicy dwuwymiarowej

```cpp
#include <iostream>
using namespace std;

int main() {
    int tablica[3][3];

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << "Podaj tablica[" << i << "][" << j << "]: ";
            cin >> tablica[i][j];
        }
    }

    cout << "\nZawartosc tablicy:\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << "tablica[" << i << "][" << j << "] = " << tablica[i][j] << '\n';
        }
    }

    return 0;
}
```

--

## Tworzenie funkcji obsługujących tablice wielowymiarowe

Analogicznie do tablic jednowymiarowych, można napisać własne funkcje do **wczytywania i wyświetlania** tablic 2D.
W C++ przekazujemy tablicę do funkcji, podając wszystkie jej wymiary poza pierwszym.

--

*Przykład (10.2)*

```cpp
#include <iostream>
using namespace std;

void printArray2D(int array[][3], unsigned rows, unsigned cols);
void scanArray2D(int array[][3], unsigned rows, unsigned cols);

int main() {
    int tablica[3][3];

    scanArray2D(tablica, 3, 3);
    printArray2D(tablica, 3, 3);

    return 0;
}

void printArray2D(int array[][3], unsigned rows, unsigned cols) {
    for (unsigned i = 0; i < rows; i++) {
        for (unsigned j = 0; j < cols; j++) {
            cout << "tablica[" << i << "][" << j << "] = " << array[i][j] << '\n';
        }
    }
}

void scanArray2D(int array[][3], unsigned rows, unsigned cols) {
    for (unsigned i = 0; i < rows; i++) {
        for (unsigned j = 0; j < cols; j++) {
            cout << "Podaj tablica[" << i << "][" << j << "]: ";
            cin >> array[i][j];
        }
    }
}
```

--

> W C++17+ można też używać `std::array<std::array<int, N>, M>` lub `std::vector<std::vector<int>>`,
> ale na razie pozostajemy przy tablicach statycznych, aby zrozumieć podstawy.

--

## Wizualizacja i wypisywanie tabelaryczne

Jeśli chcemy wypisać macierz w formie **tabeli**, można użyć `std::setw()` z `<iomanip>`:

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    int tab[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << setw(4) << tab[i][j];
        }
        cout << '\n';
    }
}
```

--


## Zadania do samodzielnego rozwiązania

1. **Macierz 4×4:**
   Wczytaj wartości do tablicy 4×4, a następnie wypisz je w formie tabeli (użyj `setw()`).

2. **Sortowanie wierszy:**
   Rozwiń program z pkt 1 tak, aby każdy wiersz był posortowany od najmniejszej do największej wartości.
   (Wskazówka: można użyć `std::sort(tab[i], tab[i] + 4)` z `<algorithm>`.)

3. **Tablica trójwymiarowa:**
   Wylosuj liczby całkowite 0–9 do tablicy `int tab[10][10][10]`.
   Następnie wypisz ją warstwami (czyli po jednej wartości z trzeciego wymiaru).
   Użyj `rand()` i `setw(2)`.

--

4. **Macierz 6×6 – wczytywanie i wypisywanie:**
   Stwórz funkcje `readMatrix(int a[][6], int n)` oraz `printMatrix(int a[][6], int n)`, które wczytują i wyświetlają macierz n×n.

5. **Mnożenie macierzy:**
   Napisz funkcję `multiplyMatrices()` wykonującą mnożenie macierzy A×B → C.
   Jeśli rozmiary są niezgodne, funkcja powinna zwracać `false`.
   W przeciwnym wypadku oblicz macierz wynikową.

6. **Eksperyment z wyższym wymiarem:**
   Utwórz tablicę 5-wymiarową o rozmiarach `3x3x3x3x3` i napisz prosty program, który pozwoli odczytać oraz zmieniać dowolny element, pytając użytkownika o kolejne współrzędne.

--

## Podsumowanie

* Tablice wielowymiarowe pozwalają przechowywać dane w formie **macierzy, siatek, kostek**.
* Dostęp do elementu wymaga podania wszystkich indeksów.
* W pamięci są przechowywane liniowo, ale logicznie reprezentują przestrzeń o wielu wymiarach.
* Najczęściej używana jest tablica **dwuwymiarowa** – macierz.
* W C++ można korzystać z funkcji `std::sort`, `std::setw`, a także pisać własne funkcje operujące na macierzach.

