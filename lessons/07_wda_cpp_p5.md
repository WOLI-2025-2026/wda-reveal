# Wprowadzenie do wskaźników (C++)

Wskaźnik to **zmienna przechowująca adres pamięci**. Wskaźnik ma **typ**, odpowiadający typowi danych, na które wskazuje. Aby zadeklarować wskaźnik, po typie dodajemy `*`.

*Przykład (12.0) deklaracja zmiennych wskaźnikowych (C++):*

```cpp
int* wsk_int;
char* wsk_char;

// w C++ zamiast 'struct node*' zwykle deklarujemy typ klas/struktur wcześniej:
struct node {};
node* wsk_node;
```

--

## Wskaźniki na zmienne, referencja (adres) i dereferencja

Wskaźnik przypisujemy do istniejącej zmiennej, biorąc **adres** zmiennej operatorem `&` (address-of).
**Dereferencja** (`*wsk`) pozwala odwołać się do wartości „pod adresem”.

--

*Przykład (12.1) stworzenie wskaźnika na zmienną (C++):*

```cpp
#include <iostream>
using namespace std;

int main() {
    int zmienna;
    int* wsk_int = &zmienna;   // adres zmiennej

    // ...lub w dwóch krokach:
    int zmienna2;
    int* wsk2;
    wsk2 = &zmienna2;

    // modyfikacja wartości przez wskaźnik (dereferencja):
    *wsk_int = 42;
    cout << "zmienna = " << zmienna << '\n'; // 42
}
```

--

> Obrazowo: `wsk` przechowuje **adres**, `*wsk` to **wartość** pod tym adresem.
> Wskaźnik w dowolnym momencie wskazuje **dokładnie jedno miejsce**, ale podczas działania programu można mu przypisywać **różne adresy**.

--

## Arytmetyka wskaźników

Na wskaźnikach można wykonywać:

* **odejmowanie dwóch wskaźników tego samego typu** → wynik to odległość (w liczbie elementów danego typu),
* **dodawanie/odejmowanie liczby całkowitej** → przesunięcie wskaźnika o tyle **elementów** (nie bajtów!) danego typu.

To szczególnie przydatne w pracy z tablicami (pamiętaj: nazwa tablicy **degraduje** do wskaźnika na jej **pierwszy element**).

--

*Przykład (12.2.1) iteracja po tablicy wskaźnikiem (C++):*

```cpp
#include <iostream>
using namespace std;

constexpr int ARRAY_SIZE = 6;

int main() {
    int array[ARRAY_SIZE] = {1,2,3,4,5,6};
    int* ptrArray;

    for (ptrArray = array; ptrArray - array < ARRAY_SIZE; ++ptrArray) {
        cout << *ptrArray << ' ';
    }
    cout << '\n';
    return 0;
}
```

--

*Przykład (12.2.2) to samo, z indeksowaniem przez dodawanie do wskaźnika:*

```cpp
#include <iostream>
using namespace std;

constexpr int ARRAY_SIZE = 6;

int main() {
    int array[ARRAY_SIZE] = {1,2,3,4,5,6};
    int* ptrArray = array;

    for (int i = 0; i < ARRAY_SIZE; ++i) {
        cout << *(ptrArray + i) << ' ';
    }
    cout << '\n';
    return 0;
}
```

--

**Jak to działa?**
`ptrArray = array;` – wskaźnik ustawiamy na **pierwszy element**.
`ptrArray - array` – różnica wskaźników (liczba elementów).
`++ptrArray` – przesuwa wskaźnik o **jeden element typu `int`** dalej.
`*ptrArray` – dereferencja, czyli bieżąca wartość tablicy.

--

### Wskaźnik a tablica wielowymiarowa

W pamięci tablice wielowymiarowe leżą **ciągiem** (wiersz po wierszu). Możemy więc przejść po wszystkich elementach jednym wskaźnikiem na typ bazowy.

--

*Przykład (12.3) przejście po tablicy 2D wskaźnikiem (C++):*

```cpp
#include <iostream>
using namespace std;

constexpr int N = 3;

int main() {
    int array[N][N] = {{1,2,3},{4,5,6},{7,8,9}};

    int* ptr  = &array[0][0];
    int* pend = &array[N-1][N-1];

    for (; ptr <= pend; ++ptr) {
        cout << *ptr << ' ';
    }
    cout << '\n';
    return 0;
}
```

--

> Uwaga: kontroluj **granice** – wychodzenie poza zakres tablicy prowadzi do błędów wykonania.

--

## Wskaźnik na wskaźnik

Wskaźnik może wskazywać **inny wskaźnik**. Dodając kolejne `*`, otrzymujemy „poziomy” pośrednie.

*Przykład (12.4) wskaźnik na wskaźnik (i dalej) w C++:*

```cpp
#include <iostream>
using namespace std;

int main() {
    int  liczba = 20;
    int* wsk_int = &liczba;
    int** wsk_wsk_int = &wsk_int;
    int*** wsk_wsk_wsk_int = &wsk_wsk_int;

    cout << " liczba= " << liczba
         << " ; *wsk_int= " << *wsk_int
         << " ; **wsk_wsk_int= " << **wsk_wsk_int
         << " ; ***wsk_wsk_wsk_int= " << ***wsk_wsk_wsk_int << '\n';

    ++liczba;

    cout << " liczba= " << liczba
         << " ; *wsk_int= " << *wsk_int
         << " ; **wsk_wsk_int= " << **wsk_wsk_int
         << " ; ***wsk_wsk_wsk_int= " << ***wsk_wsk_wsk_int << '\n';

    // Adresy wypisujemy jako wskaźniki na void* (czytelnie i przenośnie):
    cout << "&liczba= " << static_cast<const void*>(&liczba)
         << " ;  wsk_int= " << static_cast<const void*>(wsk_int)
         << " ; *wsk_wsk_int= " << static_cast<const void*>(*wsk_wsk_int)
         << " ; **wsk_wsk_wsk_int= " << static_cast<const void*>(**wsk_wsk_wsk_int) << '\n';

    cout << " &wsk_int= " << static_cast<const void*>(&wsk_int)
         << " ; wsk_wsk_int= " << static_cast<const void*>(wsk_wsk_int)
         << " ; *wsk_wsk_wsk_int= " << static_cast<const void*>(*wsk_wsk_wsk_int) << '\n';

    cout << " &wsk_wsk_int= " << static_cast<const void*>(&wsk_wsk_int)
         << " ; wsk_wsk_wsk_int= " << static_cast<const void*>(wsk_wsk_wsk_int) << '\n';
    return 0;
}
```

--

Program pokazuje: wartości zmiennych, dereferencje na kolejnych poziomach oraz **adresy** (w C++ wypisujemy je bezpiecznie jako `const void*`).

> W praktyce wskaźniki wielokrotne (`T**`, `T***`) spotkasz np. przy dynamicznych tablicach wielowymiarowych lub interfejsach C-API.

--

## Zadania do samodzielnego wykonania

1. **Pierwsze kroki ze wskaźnikiem**

   * zadeklaruj zmienną `int` oraz wskaźnik `int*`;
   * zainicjalizuj zmienną dowolną wartością i przypisz wskaźnikowi **adres** tej zmiennej;
   * wypisz kolejno: wartość zmiennej, jej **adres**, potem **adres przechowywany** we wskaźniku;
   * zmień wartość zmiennej zwykłym przypisaniem i ponownie wypisz stan;
   * zmień wartość **przez wskaźnik** (np. `*p = ...`) i ponownie wypisz stan.

2. **Wskaźnik i tablica**

   * zadeklaruj i zainicjalizuj tablicę `int a[10]` oraz wskaźnik `int* p = a;`
   * wypisz wszystkie elementy tablicy **przez wskaźnik** (inkrementuj `p` lub użyj `*(p+i)`),
   * zmień dwa wybrane elementy tablicy **przez wskaźnik** i wypisz wynik.

--

# Własne funkcje (C++)

Rozdział rozszerza temat funkcji o **przekazywanie parametrów przez wartość, wskaźnik i referencję**.

## Przekazywanie argumentu funkcji przez wartość

Przekazanie **przez wartość** kopiuje argument do parametru funkcji. Oryginalna zmienna **nie ulega zmianie**.

--

*Przykład (13.1) funkcja z parametrem przekazywanym przez wartość (C++):*

```cpp
#include <iostream>
using namespace std;

int dodaj5(int liczba)
{
    liczba += 5;    // modyfikujemy kopię
    return liczba;
}

int main()
{
    int licz = 5;
    int wynik = dodaj5(licz);

    cout << "licz = " << licz << " ; wynik = " << wynik << '\n';
    return 0;
}
```

--

## Przekazywanie argumentu funkcji przez wskaźnik

Tu formalnie **przekazujemy wskaźnik** (adres). Funkcja może zmienić wartość znajdującą się **pod adresem** (dereferencja `*`), więc wpływa na zmienną wywołującego.

--

*Przykład (13.2.1) parametr jako wskaźnik:*

```cpp
#include <iostream>
using namespace std;

int dodaj5(int* liczba)
{
    *liczba += 5;   // zmieniamy oryginał przez dereferencję
    return *liczba;
}

int main()
{
    int licz = 5;
    int wynik = dodaj5(&licz); // przekazujemy adres

    cout << "licz = " << licz << " ; wynik = " << wynik << '\n';
    return 0;
}
```

--

*Przykład (13.2.2) identycznie, ale z osobnym wskaźnikiem:*

```cpp
#include <iostream>
using namespace std;

int dodaj5(int* liczba)
{
    *liczba += 5;
    return *liczba;
}

int main()
{
    int licz = 5;
    int* wsk = &licz;

    int wynik = dodaj5(wsk);

    cout << "licz = " << licz << " ; wynik = " << wynik << '\n';
    return 0;
}
```

--

## Przekazywanie tablicy jako argumentu funkcji

Przekazanie tablicy do funkcji sprowadza się do przekazania **wskaźnika na jej pierwszy element**. Dlatego modyfikacje w funkcji widać na oryginale.

--

*Przykład (13.3) obsługa tablicy przez arytmetykę wskaźników:*

```cpp
#include <iostream>
using namespace std;

void printArrayOfInt(int* array, int size)
{
    for (int* p = array; p - array < size; ++p)
        cout << *p << ' ';
    cout << '\n';
}

int main()
{
    int array[6] = {1,2,3,4,5,6};
    printArrayOfInt(array, 6);
    return 0;
}
```

--

**Tablica wielowymiarowa.** W pamięci leży „ciągiem” (wierszami), więc można przejść po niej wskaźnikiem do **pojedynczego elementu**.

--

*Przykład (13.4) drukowanie 2D przez wskaźnik:*

```cpp
#include <iostream>
using namespace std;

void printArray2DimOfInt(int* array, int size_x, int size_y)
{
    int last = size_x * size_y - 1;
    int* p = array;
    for (int i = 0; p <= &array[last]; ++p, ++i) {
        if (i % size_y == 0) cout << '\n';
        cout << ' ' << *p;
    }
    cout << '\n';
}

int main()
{
    int array[3][3] = {{1,2,3},{4,5,6},{7,8,9}};
    // decay do int* (pierwszy element)
    printArray2DimOfInt(&array[0][0], 3, 3);
    return 0;
}

--

> Uwaga: w C++ można też pisać funkcje z nagłówkiem `void f(int a[][3])` dla znanego drugiego wymiaru, albo używać `std::array`/`std::vector`. Tu zostajemy przy surowych tablicach, by skupić się na sposobach przekazywania parametrów.

--

## Przekazywanie argumentu funkcji przez referencję (C++)

**Referencja** (`T&`) to alias oryginalnej zmiennej. Działa podobnie do wskaźnika, ale jest **bezpieczniejsza i wygodniejsza** (nie trzeba dereferencjonować).

--

*Przykład (13.5) parametr przez referencję:*

```cpp
#include <iostream>
using namespace std;

int dodaj5(int& liczba)  // alias na oryginał
{
    liczba += 5;         // modyfikujemy oryginał
    return liczba;
}

int main()
{
    int licz = 5;
    int wynik = dodaj5(licz);

    cout << "licz = " << licz << " ; wynik = " << wynik << '\n';
    return 0;
}
```

--

> Kiedy używać?
>
> * **Wartość** – gdy chcesz kopii i brak efektów ubocznych.
> * **Referencja (`T&`)** – gdy chcesz modyfikować oryginał (lub uniknąć kopii dużych obiektów).
> * **Wskaźnik (`T*`)** – gdy naturalnie operujesz na adresach, przekazanie może być `nullptr`, iterujesz po buforach itp.

--

## Zadania do samodzielnego wykonania

1. Napisz funkcję, która **zwraca adres większej** z dwóch liczb przekazywanych przez wskaźniki:
   `int* max_ptr(int* a, int* b);`

2. Napisz funkcję, która **porównuje dwie liczby**, a **mniejszą** nadpisuje **sumą obu**. Zmienne są zadeklarowane i zainicjalizowane przed wywołaniem.
   Użyj wskaźników jako parametrów wejściowych, **funkcja nie zwraca wartości**.

3. Wykonaj następujące kroki:

   * zadeklaruj i zainicjalizuj tablicę `int a[10]` oraz wskaźnik na tę tablicę `int* p = a;`
   * napisz i wywołaj funkcję wyświetlania tablicy,
   * napisz i wywołaj funkcję ponownego wprowadzania elementów tablicy,
   * napisz i wywołaj funkcje zliczające: **sumę**, **średnią**, **wartość największą**, **wartość najmniejszą**,
   * zaimplementuj **menu wyboru** pozwalające uruchamiać powyższe operacje.

--
