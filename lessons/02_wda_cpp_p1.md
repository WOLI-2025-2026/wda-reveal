# „Hello World!" - Procedury wejścia i wyjścia, proste typy zmiennych.

--

## Zmienne

Zmienna to związek trzech składowych: nazwy, zbioru wartości oraz wybranego elementu zbioru wartości. W praktyce zmienna to zarezerwowane miejsce w pamięci dla pewnej danej wykorzystywanej w programie. W języku C++ zbiór wartości zmiennej określamy jako typ. Podstawowymi typami zmiennych są:

* *int –* zmienna całkowitoliczbowa
* *char –* zmienna znakowa
* *float –* zmienna liczbowa zmiennoprzecinkowa
* *double-* zmienna liczbowa podwójnej precyzji (również zmiennoprzecinkowa)

--

Aby utworzyć zmienną w C++ należy podać jej typ oraz nadać jej nazwę: **typ\_zmiennej nazwa\_zmiennej**. Wartość, czyli trzecia składowa zmiennej utworzonej w ten sposób, zostanie wybrana losowo lub wyzerowana (w zależności od miejsca w kodzie, w którym zmienna jest tworzona).

*Przykład (1.0) Tworzenie własnych zmiennych*

```cpp
#include <iostream>
using namespace std;

int main() {	
    int liczba_calkowita;
    char znak;
    float zmiennoprzecinkowa;
    double podwojnej_precyzji;
	
    return 0;
}
```

Program z przykładu (1.0), rezerwuje miejsce dla 4 zmiennych o nazwach *liczba\_calkowita, znak, zmiennoprzecinkowa, podwojnej\_precyzji.*

--

## Funkcja `cout`

Funkcje wejścia i wyjścia to podstawowe elementy, używane w programowaniu do komunikacji programu z użytkownikiem. Pozwalają one wypisywać komunikaty oraz pobierać dane od użytkownika. W języku C++ do wypisywania używamy strumienia wyjścia `std::cout`. Aby wyświetlić tekst na ekranie konsoli, należy wywołać `cout` wraz z operatorem `<<`.

*Przykład (1.1) Wyświetlanie tekstu za pomocą cout*

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello World!";
    return 0;
}
```

*Wynik działania programu:*

> Hello World!

--

Za pomocą `cout` można również wyświetlić wartość zmiennej.

*Przykład (1.2) Wyświetlanie zmiennej za pomocą cout*

```cpp
#include <iostream>
using namespace std;

int main() {	
    int liczba_calkowita = 0;
    cout << "Liczba calkowita: " << liczba_calkowita;
    return 0;
}
```

*Wynik działania programu:*

> Liczba calkowita: 0

--

Możemy również wyświetlić wiele zmiennych:

*Przykład (1.3) Wyświetlanie wielu zmiennych za pomocą cout*

```cpp
#include <iostream>
using namespace std;

int main() {	
    int liczba_calkowita = 0;
    char znak = 'a';
    float zmiennoprzecinkowa = 0.4;
    cout << liczba_calkowita << " " << znak << " " << zmiennoprzecinkowa;
    return 0;
}
```

*Wynik działania programu:*

> 0 a 0.4

--

### Funkcja `cin`

Kolejnym bardzo ważnym elementem jest pobieranie danych od użytkownika. W C++ służy do tego `std::cin`, który działa podobnie jak `scanf`, ale nie wymaga podawania adresów ani kodów formatujących.

*Przykład (1.4) Pobieranie wartości za pomocą cin*

```cpp
#include <iostream>
using namespace std;

int main() {	
    int liczba_calkowita;
    cin >> liczba_calkowita;
    return 0;
}
```

--

Można sprawdzić działanie, dodając komunikaty:

*Przykład (1.5) Pobieranie wartości za pomocą cin - dowód*

```cpp
#include <iostream>
using namespace std;

int main() {	
    int liczba_calkowita = 0;
    cout << "Liczba calkowita przed cin: " << liczba_calkowita << endl;
    cout << "Podaj liczbe calkowita: ";
    cin >> liczba_calkowita;
    cout << "Liczba calkowita po cin: " << liczba_calkowita;
    return 0;
}
```

--

Można też pobrać kilka zmiennych naraz:

*Przykład (1.6) Pobranie wielu wartości za pomocą cin*

```cpp
#include <iostream>
using namespace std;

int main() {	
    int liczba_calkowita;
    char znak;
    float zmiennoprzecinkowa;
    cin >> liczba_calkowita >> znak >> zmiennoprzecinkowa;
    return 0;
}
```

--

## Formatowanie wyświetlanego tekstu

W języku C++ do formatowania używamy manipulatorów z nagłówka `<iomanip>`, np. `setw`, `setprecision`, `fixed`.

*Przykład (1.7) Formatowanie wyświetlania liczb całkowitych*

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {	
    int a=101;
    int b=13;
    int c=4;
    cout << setw(3) << a << endl;
    cout << setw(3) << b << endl;
    cout << setw(3) << c << endl;
    return 0;
}
```

--

*Przykład (1.8) Formatowanie wyświetlania liczb zmiennoprzecinkowych*

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {	
    float a = 4.440441444;
    cout << a << endl;
    cout << fixed << setprecision(2) << a << endl;
    return 0;
}
```

--

### Przykłady do analizy:

*Przykład (1.9) wczytanie zmiennych typu int i float*

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() { 
   int age; 
   float height; 
   cout << "Age and height: "; 
   cin >> age >> height; 
   cout << "Your age: " << age << endl 
        << "Your height: " << fixed << setprecision(2) << height;
   return 0; 
} 
```

--

*Przykład (1.10) Formatowanie wyświetlania zmiennych typu float*

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() { 
   float PI = 3.14159265359;
   cout << fixed << setprecision(2) << " .2f = " << setw(7) << PI << endl;
   cout << fixed << setprecision(3) << " .3f = " << setw(7) << PI << endl;
   cout << fixed << setprecision(5) << " .5f = " << setw(7) << PI << endl;
   return 0;
} 
```

--

### Zadania do samodzielnego wykonania:

1. Napisz program, który przywita się z użytkownikiem, zapyta, ile ma lat (zmienna całkowitoliczbowa) i wyświetli komunikat, jaki wiek podał użytkownik.

2. Napisz program, który wczyta jedną liczbę zmiennoprzecinkową i wyświetli ją z dokładnością do 1, 3, 5 miejsc po przecinku. Wczytywanie poprzedź odpowiednim komunikatem.

--

# Operatory arytmetyczne (C++)

## Operator przypisania

Operatory arytmetyczne służą do wykonywania operacji matematycznych na zmiennych. Pierwszym z nich jest użyty już wcześniej **operator przypisania**. Jego symbolem jest znak `=`. Zapisuje on wartość wyrażenia podanego **po prawej** stronie (P-wyrażenie) do wyrażenia **po lewej** stronie (L-wyrażenie).

* L-wyrażeniem w praktyce będzie u nas **zmienna**, do której można zapisać wartość.
* P-wyrażeniem może być dowolne wyrażenie dające wynik: zmienna, stała, działanie arytmetyczne, wynik funkcji, a także ich kombinacje.

--

W C++ (tak jak w C) istnieją także **złożone operatory przypisania** (np. `+=`, `-=`, …), które od razu wykonują działanie i zapisują wynik do tej samej zmiennej. Operator przypisania ma **wiążenie prawostronne** (right-associative): najpierw obliczane jest wyrażenie po prawej stronie, a dopiero potem wykonywane jest przypisanie.

--

*Przykład (2.0) Wykonanie przypisania (C++):*

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    char c, d;

    // przypisanie konkretnych wartości
    a = 3;
    b = 4;
    c = 'A';
    d = 'a';
    cout << "a:" << a << " b:" << b << " c:" << c << " d:" << d << '\n';

    // przypisanie za pomocą innych zmiennych
    a = b;
    c = d;
    cout << "a:" << a << " b:" << b << " c:" << c << " d:" << d << '\n';
    return 0;
}
```

*Wynik działania programu:*

> a:3 b:4 c\:A d\:a
> a:4 b:4 c\:a d\:a

--

## Operatory arytmetyczne

Operatory arytmetyczne w C++ odpowiadają za dodawanie, odejmowanie, mnożenie, dzielenie i resztę z dzielenia. Używa się ich intuicyjnie, jak w matematyce.

*Przykład (2.1) Operacje arytmetyczne (C++):*

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 5;
    int suma = a + b;        // dodawanie
    int roznica = a - b;     // odejmowanie
    int iloczyn = a * b;     // mnożenie
    int iloraz = a / b;      // dzielenie całkowite (bo int)
    int modulo = a % b;      // reszta z dzielenia

    cout << "a+b=" << suma << '\n'
         << "a-b=" << roznica << '\n'
         << "a*b=" << iloczyn << '\n'
         << "a/b=" << iloraz << '\n'
         << "a%b=" << modulo << '\n';
    return 0;
}
```

*Wynik działania programu:*

> a+b=15
> a-b=5
> a\*b=50
> a/b=2
> a%b=0

--

Aby wykonać działanie arytmetyczne, umieszczamy je po prawej stronie `=`. W jednym wyrażeniu można mieć kilka operatorów — **priorytet** i **wiążenie lewostronne** (dla `+ - * / %`) decydują o kolejności, a **nawiasy** pozwalają tę kolejność zmienić.

*Przykład (2.2) Operacje wieloargumentowe i nawiasy (C++):*

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 4, b = 5, c = 3, wynik;

    cout << "a=" << a << " b=" << b << " c=" << c << '\n';

    wynik = a + b * c;      // mnożenie ma wyższy priorytet
    cout << "a+b*c = " << wynik << '\n';

    wynik = (a + b) * c;    // nawiasy zmieniają kolejność
    cout << "(a+b)*c = " << wynik << '\n';

    wynik = (a + b) * 2;    // mieszanie zmiennych i stałych
    cout << "(a+b)*2 = " << wynik << '\n';

    return 0;
}
```

*Wynik działania programu:*

> a=4 b=5 c=3
> a+b\*c = 19
> (a+b)\*c = 27
> (a+b)\*2 = 18

--

## Dzielenie całkowite a dzielenie zmiennoprzecinkowe

Szczególną uwagę trzeba zwrócić na **dzielenie**. Gdy wszystkie argumenty i zmienna-wynik są typu całkowitego (`int`), wykonywane jest **dzielenie całkowite** (część ułamkowa jest obcinana). Jeśli chcemy uzyskać część ułamkową, przynajmniej jeden operand i/lub zmienna docelowa muszą być typu zmiennoprzecinkowego (`float`/`double`).

*Przykład (2.3) Różnica dzielenia:*

```cpp
// Dzielenie całkowite
#include <iostream>
using namespace std;

int main() {
    int a = 10, b = 4;
    int c = a / b;      // 2 (część ułamkowa obcięta)
    cout << a << "/" << b << "=" << c << '\n';
    return 0;
}
```

*Wynik:*

> 10/4=2

--

```cpp
// Dzielenie zmiennoprzecinkowe
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    float a = 10, b = 4;
    float c = a / b;    // 2.5
    cout << fixed << setprecision(1)
         << a << "/" << b << "=" << c << '\n';
    return 0;
}
```

*Wynik:*

> 10/4=2.5

--

## Konwersja typów

**Konwersja typów** jest potrzebna, gdy chcemy tymczasowo potraktować wartość jak innego typu. W C++ polecamy korzystać z rzutowań w stylu C++: `static_cast<T>(wyrazenie)`.

* **Konwersja jawna** — sami wskazujemy typ.
* **Konwersja niejawna** — kompilator dobierze typ pośredni tak, aby nie tracić informacji (np. w wyrażeniu mieszanym `int` i `float` wartości całkowite zostaną rozszerzone do `float`).

--

*Przykład (2.4) Konwersja jawna:*

```cpp
#include <iostream>
using namespace std;

int main() {
    int a = 5, b = 10;
    float c;

    c = a / b; // dzielenie int/int -> najpierw 0, potem konwersja do float
    cout << c << '\n'; // 0

    c = static_cast<float>(a) / b; // a rzutowane na float -> dzielenie float
    cout << c << '\n'; // 0.5
    return 0;
}
```

*Wynik:*

> 0
> 0.5

W powyższym przykładzie pierwsze przypisanie to także **konwersja niejawna** (z `int` na `float`) — ale dopiero po wykonaniu dzielenia całkowitego. Drugie używa jawnego rzutowania, przez co całe dzielenie staje się zmiennoprzecinkowe. Dodatkowo, gdy jeden operand jest `float`, **drugi też zostanie niejawnie rozszerzony** do `float` przed wykonaniem operacji.

Uwaga: rzutowanie w dół, np. z `float` do `int`, **ucina część ułamkową**.

--

## Podsumowanie operatorów (C++)

### Operatory arytmetyczne

| znak | funkcja                                                  |
| :--: | :------------------------------------- |
|  `+` | Dodawanie                                                |
|  `-` | Odejmowanie                                              |
|  `*` | Mnożenie                                                 |
|  `/` | Dzielenie                                                |
|  `%` | Modulo (reszta z dzielenia, tylko dla typów całkowitych) |

--

### Operatory przypisania

| znak | funkcja                        | przykład | zapis równoważny |
| :--: | :-------------------- | :----: | :----------: |
|  `=` | Zwykłe przypisanie             |  `x = 2` |         —        |
| `+=` | Przypisanie sumy               | `x += 2` |    `x = x + 2`   |
| `-=` | Przypisanie różnicy            | `x -= 2` |    `x = x - 2`   |
| `*=` | Przypisanie iloczynu           | `x *= 2` |    `x = x * 2`   |
| `/=` | Przypisanie ilorazu            | `x /= 2` |    `x = x / 2`   |
| `%=` | Przypisanie reszty z dzielenia | `x %= 2` |    `x = x % 2`   |

> Przypomnienie: `=` jest **prawostronnie wiążący** (right-associative), a `+ - * / %` są **lewostronnie wiążące** (left-associative). Priorytet: `* / %` > `+ -`. Używaj nawiasów, gdy chcesz to nadpisać.

--

## Operator inkrementacji i dekrementacji

W C++ mamy **inkrementację** (`++`) i **dekrementację** (`--`), które zwiększają/zmniejszają wartość zmiennej całkowitej o 1. Mogą wystąpić **przed** zmienną (pre-) lub **po** (post-).

* **Preinkrementacja** `++a` — najpierw zwiększa `a`, potem zwraca nową wartość.
* **Postinkrementacja** `a++` — zwraca starą wartość `a`, a dopiero potem ją zwiększa.

Analogicznie działa `--a` i `a--`.

--

*Przykład (2.6) Pre- vs post-inkrementacja:*

```cpp
// Preinkrementacja
#include <iostream>
using namespace std;

int main() {
    int a = 2;
    int b = ++a; // a staje się 3, b otrzymuje 3
    cout << "a=" << a << '\n' << "b=" << b << '\n';
    return 0;
}
```

*Wynik:*

> a=3
> b=3

--

```cpp
// Postinkrementacja
#include <iostream>
using namespace std;

int main() {
    int a = 2;
    int b = a++; // b otrzymuje 2, a dopiero potem staje się 3
    cout << "a=" << a << '\n' << "b=" << b << '\n';
    return 0;
}
```

*Wynik:*

> a=3
> b=2

--

## Przykłady do analizy

*Przykład (2.7) Suma dwóch liczb (wzór z obliczeniem wewnątrz `cout`):*

```cpp
#include <iostream>
using namespace std;

int main() { 
    int x, y; 
    cout << "Podaj x i y: "; 
    cin >> x >> y;
    // kompilator najpierw obliczy x + y, potem wypisze wynik
    cout << "Suma x+y = " << (x + y) << '\n'; 
    return 0; 
}
```

--

*Przykład (2.8) Iloczyn i formatowanie wyświetlania:*

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() { 
    cout << "Inches: "; 
    float inches; 
    cin >> inches;
    cout << "Centimetres: " << fixed << setprecision(2) << (inches * 2.54f) << '\n';
    return 0; 
}
```

--

## Zadania do samodzielnego wykonania

1. Napisz program, który pobierze od użytkownika 3 liczby całkowite, a następnie wyświetli wartości:

   1. sumy trzech,
   2. różnicy pierwszych dwóch,
   3. iloczynu pierwszej i trzeciej,
   4. ilorazu trzeciej i drugiej (pamiętaj o doborze typu przy dzieleniu).

2. Napisz program, który wylicza średnią dla 5 ocen (użyj typu zmiennoprzecinkowego i wypisz wynik z np. 2 miejscami po przecinku).

--

# Instrukcje warunkowe i operatory logiczne (C++)

--

## Instrukcja warunkowa

Instrukcja warunkowa jest elementem języka programowania, który pozwala wykonać różne instrukcje zależnie od warunku podanego wewnątrz nawiasów.

*Schemat (3.0) Instrukcja warunkowa*

![schemat 3 0](https://user-images.githubusercontent.com/71324202/139920911-2c98e385-d3ac-4569-9ae7-670a65c7edf7.png)

--

W języku C++ instrukcja warunkowa występuje w postaci instrukcji **if** (jeżeli) oraz **else** (w przeciwnym przypadku). Schemat:

```cpp
if(warunek) { 
    // Kod do wykonania przy spełnieniu warunku
}
else { 
    // Kod do wykonania, jeżeli warunek się nie spełni
}
```

W miejscu oznaczonym jako *warunek* podajemy wyrażenie logiczne lub zmienną. Blok w `{}` zostanie wykonany, jeśli wyrażenie zwróci wartość **różną od 0** (czyli logiczne „prawda”). Do budowy warunków używa się operatorów relacji i operatorów logicznych.

--

## Operatory relacji i operatory logiczne

### Operatory relacji

| Oznaczenie | Działanie          | Przykład użycia                        |
| :------: | :------------ | :------------------------- |
|    `==`    | Równe              | `if(a == b) // jeżeli a równe b`       |
|    `!=`    | Różne              | `if(a != b) // jeżeli a różne od b`    |
|     `<`    | Mniejsze           | `if(a < b)  // jeżeli a mniejsze od b` |
|     `>`    | Większe            | `if(a > b)  // jeżeli a większe od b`  |
|    `<=`    | Mniejsze lub równe | `if(a <= b) // jeżeli a ≤ b`           |
|    `>=`    | Większe lub równe  | `if(a >= b) // jeżeli a ≥ b`           |

--

### Operatory logiczne

| Oznaczenie | Działanie        | Przykład użycia                                  |                  |            |   |                                |
| :------: | :---------- | :-------------------------------- | ----------- | ------- | - | -------------------- |
|    `&&`    | Koniunkcja (AND) | `if(a == b && b < 10) // jeżeli a==b oraz b<10`  |                  |            |   |                                |
|     \|\|   | Alternatywa (OR) | `if(a > b \|\| a < 0) // jeżeli a>b lub a<0` |
|     `!`    | Negacja (NOT)    | `if(!(a < b)) // jeżeli nie jest prawdą, że a<b` |                  |            |   |                                |

Wynikiem każdej operacji logicznej jest wartość: **różna od 0**, gdy warunek spełniony, lub **0**, gdy niespełniony.

--

## Przykład użycia instrukcji warunkowej

*Przykład (3.0) Wykorzystanie instrukcji warunkowej (C++):*

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    cout << "Podaj dwie liczby: ";
    cin >> a >> b;

    if(a == b)
        cout << "Liczby sa rowne!" << endl;
    else
        cout << "Liczby sa rozne!" << endl;

    return 0;
}
```

*Wynik działania programu, dla dwóch zmiennych różnych:*

```
Podaj dwie liczby: 3 2
Liczby sa rozne!
```

*Wynik działania programu, dla dwóch zmiennych równych:*

```
Podaj dwie liczby: 3 3
Liczby sa rowne!
```

--

## Operator trójargumentowy `?:`

Jeśli efekt działania instrukcji warunkowej różni się tylko jedną linią, można użyć operatora trójargumentowego `?:`.

*Przykład (3.1) użycie operatora `?:` zamiast prostego if-else (C++):*

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    cout << "Podaj dwie liczby: ";
    cin >> a >> b;

    (a == b) ? cout << "Liczby sa rowne!" : cout << "Liczby sa rozne!";
    return 0;
}
```

*Wynik działania programu:*

```
Podaj dwie liczby: 3 2
Liczby sa rozne!
```

lub:

```
Podaj dwie liczby: 3 3
Liczby sa rowne!
```

--

Wyrażenie trójargumentowe składa się z trzech części:

1. wyrażenie logiczne,
2. wyrażenie wykonywane, gdy warunek jest prawdziwy,
3. wyrażenie wykonywane, gdy warunek jest fałszywy.

Schemat:

```cpp
warunek ? wyrazenie1 : wyrazenie2;
```

![operator trojargumentowy](https://user-images.githubusercontent.com/71324202/139921157-50821243-6470-4736-a401-7a9349081b2b.png)

--

*Przykład (3.2) wykonanie funkcji `max(a, b)` przy pomocy operatora `?:`:*

```cpp
#include <iostream>
using namespace std;

int main() {
    int a, b;
    cout << "Podaj dwie liczby: ";
    cin >> a >> b;

    int c = (a > b) ? a : b;  // wybiera większą z dwóch liczb
    cout << "Wieksza liczba to: " << c;
    return 0;
}
```

--

## Zadania do samodzielnego wykonania

1. Stwórz program, który wczytuje od użytkownika 2 liczby całkowite i wyświetla:

   * większą,
   * mniejszą,
   * relację jaka występuje pomiędzy pierwszą a drugą (np. `3<4`, `5=5`, `5>1`).

2. Napisz prosty kalkulator, w którym użytkownik podaje 2 liczby, następnie znak działania (`+`, `-`, `*`, `/`, `%`). Program wykonuje działanie i wyświetla wynik.

3. Napisz program, który pobiera 2 liczby od użytkownika, a następnie stwierdza, czy pierwsza jest podzielna przez drugą.

4. Napisz program, który oblicza średnią dla 5 ocen, oraz wyświetla, ile było ocen niedostatecznych.


--

# Pętle (C++)

## Wprowadzenie

Pętle pozwalają **wielokrotnie wykonywać ten sam fragment kodu** bez konieczności powielania go ręcznie. Dzięki nim możemy zrealizować np. sumowanie elementów, powtarzanie obliczeń, odczytywanie wielu danych od użytkownika.

W C++ mamy trzy podstawowe konstrukcje pętli:

* `while`
* `do … while`
* `for`

Każda z nich działa nieco inaczej i jest stosowana w innych sytuacjach.

--

## Pętla `while`

Pętla `while` powtarza fragment kodu **tak długo, jak spełniony jest warunek** zapisany w jej nagłówku.

*Schemat:*

```cpp
while(warunek) {
    // kod wykonywany dopóki warunek jest prawdziwy
}
```

Najpierw sprawdzany jest warunek, a dopiero później wykonywane jest ciało pętli.

--

*Przykład (4.0) Pętla while w C++:*

```cpp
#include <iostream>
using namespace std;

int main() {
    int i = 0;
    while(i < 5) {
        cout << "i = " << i << endl;
        i++; // zwiększamy i, aby pętla się zakończyła
    }
    return 0;
}
```

*Wynik działania programu:*

```
i = 0
i = 1
i = 2
i = 3
i = 4
```

--

## Pętla `do … while`

Pętla `do … while` działa podobnie jak `while`, ale **najpierw wykonuje ciało pętli, a dopiero potem sprawdza warunek**. Dzięki temu jest gwarancja, że kod w pętli wykona się co najmniej raz.

*Schemat:*

```cpp
do {
    // kod wykonywany co najmniej raz
} while(warunek);
```

*Przykład (4.1) Pętla do … while w C++:*

```cpp
#include <iostream>
using namespace std;

int main() {
    int liczba;
    do {
        cout << "Podaj liczbe dodatnia: ";
        cin >> liczba;
    } while(liczba <= 0);

    cout << "Podales liczbe " << liczba << endl;
    return 0;
}
```

Tutaj pętla powtarza się, dopóki użytkownik nie poda liczby dodatniej.

--

## Pętla `for`

Pętla `for` jest bardzo wygodna, gdy znamy z góry liczbę powtórzeń. Jej nagłówek składa się z trzech elementów:

```cpp
for(inicjalizacja; warunek; modyfikacja) {
    // kod powtarzany dopóki warunek jest prawdziwy
}
```

* **inicjalizacja** – ustawienie wartości początkowej zmiennej sterującej,
* **warunek** – warunek kontynuacji pętli,
* **modyfikacja** – zmiana zmiennej sterującej po każdej iteracji.

--

*Przykład (4.2) Pętla for w C++:*

```cpp
#include <iostream>
using namespace std;

int main() {
    for(int i = 0; i < 5; i++) {
        cout << "i = " << i << endl;
    }
    return 0;
}
```

*Wynik działania programu:*

```
i = 0
i = 1
i = 2
i = 3
i = 4
```

--

## Instrukcje sterujące w pętlach

### Instrukcja `break`

Instrukcja `break` pozwala **przerwać działanie pętli** niezależnie od warunku.

*Przykład (4.3) Użycie break w C++:*

```cpp
#include <iostream>
using namespace std;

int main() {
    for(int i = 0; i < 10; i++) {
        if(i == 5) break; // przerwij pętlę, gdy i==5
        cout << i << " ";
    }
    return 0;
}
```

*Wynik działania programu:*

```
0 1 2 3 4
```

--

### Instrukcja `continue`

Instrukcja `continue` **pomija bieżącą iterację** i przechodzi do kolejnej.

*Przykład (4.4) Użycie continue w C++:*

```cpp
#include <iostream>
using namespace std;

int main() {
    for(int i = 0; i < 10; i++) {
        if(i % 2 == 0) continue; // pomiń liczby parzyste
        cout << i << " ";
    }
    return 0;
}
```

*Wynik działania programu:*

```
1 3 5 7 9
```

--

## Zagnieżdżanie pętli

W C++ można umieszczać pętle wewnątrz innych pętli.

*Przykład (4.5) Zagnieżdżone pętle w C++:*

```cpp
#include <iostream>
using namespace std;

int main() {
    for(int i = 1; i <= 3; i++) {
        for(int j = 1; j <= 3; j++) {
            cout << "(" << i << "," << j << ") ";
        }
        cout << endl;
    }
    return 0;
}
```

*Wynik działania programu:*

```
(1,1) (1,2) (1,3) 
(2,1) (2,2) (2,3) 
(3,1) (3,2) (3,3) 
```

--

## Zadania do samodzielnego wykonania

1. Napisz program, który wypisuje liczby od 1 do 100.
2. Napisz program, który oblicza sumę liczb od 1 do n (n podaje użytkownik).
3. Napisz program, który wyświetla tabliczkę mnożenia (10×10).
4. Napisz program, który zlicza, ile cyfr ma podana liczba całkowita.
5. Napisz program, który pobiera od użytkownika 5 ocen, a następnie liczy ich średnią.



