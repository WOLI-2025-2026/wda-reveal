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


--

# Łańcuchy znaków i ASCII w C++

## ASCII – tabela znaków

Każdy znak w komputerze ma przypisany **kod liczbowy** (ASCII – American Standard Code for Information Interchange).
W uproszczeniu:

* `0–31` → znaki sterujące (np. `\n` – nowa linia, `\t` – tabulator),
* `32` → spacja `' '`,
* `48–57` → cyfry `'0'..'9'`,
* `65–90` → litery wielkie `'A'..'Z'`,
* `97–122` → litery małe `'a'..'z'`.

--

![ASCII](https://e7.pngegg.com/pngimages/250/319/png-clipart-ascii-character-encoding-value-binary-code-miscellaneous-angle.png)

--

**Przykład: wypisywanie znaków ASCII z kodami**

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    for (int i = 32; i < 128; i++) {
        cout << setw(3) << i << " = " << static_cast<char>(i) << '\n';
    }
    return 0;
}
```

--

*Fragment wyniku:*

```
 32 =  
 33 = !
 34 = "
 ...
 65 = A
 66 = B
 ...
 97 = a
 98 = b
 ...
```

--

## Typ `std::string`

W C++ do pracy z tekstem używamy klasy **`std::string`** z biblioteki `<string>`.
To wygodniejsza i bezpieczniejsza reprezentacja łańcucha niż tablice znaków.

--

### Tworzenie i podstawowe operacje

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s1 = "Hello";
    string s2 = "World";

    cout << s1 + " " + s2 << '\n';   // konkatenacja
    cout << s1.size() << '\n';       // długość napisu
    cout << s1[0] << '\n';           // dostęp do pojedynczego znaku
}
```

-- 

### Wczytywanie tekstu

```cpp
string s;
cin >> s;            // czyta jedno słowo (do spacji)
getline(cin, s);     // czyta całą linię
```

--

## Najważniejsze metody `std::string`

| Operacja            | Przykład                 | Wynik                      |
| ------------------- | ------------------------ | -------------------------- |
| Długość             | `s.size()`               | `5` dla `"Hello"`          |
| Konkatenacja        | `s1 + s2`                | `"HelloWorld"`             |
| Dodanie znaku       | `s.push_back('!')`       | `"Hello!"`                 |
| Dostęp do znaku     | `s[1]`                   | `'e'`                      |
| Porównanie          | `if(s1 == s2)`           | true/false                 |
| Wyszukiwanie        | `s.find("lo")`           | 3                          |
| Wycinek (substring) | `s.substr(1, 3)`         | `"ell"`                    |
| Usuwanie            | `s.erase(2, 2)`          | usuwa 2 znaki od indeksu 2 |
| Wstawianie          | `s.insert(1, "ABC")`     | `"HABCello"`               |
| Zamiana fragmentu   | `s.replace(1, 3, "XYZ")` | `"HXYZo"`                  |

--

## Funkcje pomocnicze na znakach (`<cctype>`)

Do pracy z pojedynczymi znakami:

* `isalpha(ch)` – litera?
* `isdigit(ch)` – cyfra?
* `isspace(ch)` – biały znak?
* `toupper(ch)` – zmiana na wielką literę,
* `tolower(ch)` – zmiana na małą literę.


--

*Przykład: zamiana na wielkie litery i liczenie cyfr*

```cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

int main() {
    string s;
    getline(cin, s);

    int digits = 0;
    for (char& ch : s) {
        if (isdigit((unsigned char)ch)) digits++;
        ch = toupper((unsigned char)ch);
    }
    cout << "WIELKIMI: " << s << "\n";
    cout << "Liczba cyfr: " << digits << "\n";
}
```

--

## Zadania do samodzielnego wykonania

1. Wypisz wszystkie znaki ASCII od 32 do 126 wraz z ich kodami.
2. Napisz program, który wczytuje łańcuch i:

   * wypisuje jego długość,
   * wypisuje pierwszy i ostatni znak,
   * sprawdza, czy zawiera cyfrę.
3. Napisz funkcję, która odwraca łańcuch (np. `"Ala"` → `"alA"`).
4. Napisz program, który zamienia wszystkie litery na małe i usuwa spacje.
5. Napisz program, który sprawdza, czy podane słowo jest **palindromem** (czytane od końca daje ten sam napis).
6. Napisz program zliczający liczbę poszczególnych liter w ciągu znaków podanym przez użytkownika. Program wyświetla liczbę wystąpień znaków które przynajmniej raz wystąpiły w podanym tekście.


