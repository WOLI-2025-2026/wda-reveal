--

# Instrukcja wyboru `switch-case` (C++)

--

## Menu wyboru `switch-case-break`

Instrukcja wyboru w programowaniu umożliwia wybór jednej z wielu ścieżek działania. Świetnie sprawdza się np. w tworzeniu **menu**.
W C++ składa się z instrukcji:

```cpp
switch(argument) {
    case wartosc1:
        // kod do wykonania
        break;
    case wartosc2:
        // kod do wykonania
        break;
    default:
        // kod, gdy żadna opcja nie pasuje
        break;
}
```

Instrukcja `default` jest odpowiednikiem `else` z instrukcji warunkowej.

--

*Schemat (5.0) instrukcja wielokrotnego wyboru switch-case-break:*

![Schemat1](https://user-images.githubusercontent.com/71324202/143785129-e9cbc369-dca7-419a-9da7-f4261d58f843.png)

--

*Przykład (5.0) Menu wyboru zbudowane za pomocą switch-case-break (C++):*

```cpp
#include <iostream>
#include <cstdlib> // dla exit()
using namespace std;

int main() {
    int wybor;

    for(;;) { // pętla nieskończona
        cout << "\nMENU\n";
        cout << "1. Powiedz czesc!\n";
        cout << "2. Opowiedz zart.\n";
        cout << "3. Pozegnaj sie.\n";
        cout << "Wybierz opcje: ";
        cin >> wybor;

        switch(wybor) {
            case 1:
                cout << "Czesc!\n";
                break;
            case 2:
                cout << "-Czym rozni sie doswiadczony informatyk od poczatkujacego?\n";
                cout << "-Poczatkujacy uwaza, ze 1KB to 1000B, a doswiadczony jest pewien,\n";
                cout << "  ze 1km to 1024m.\n";
                break;
            case 3:
                cout << "Do zobaczenia!\n";
                exit(0); // zakończenie programu
            default:
                cout << "Nie ma takiej opcji\n";
                break;
        }
    }
    return 0;
}
```

--

## Więcej o `switch-case`

Instrukcję `switch` można pisać także **bez użycia `break`**. Wtedy po dopasowaniu jednego `case` program **kontynuuje wykonanie kolejnych opcji** aż do napotkania `break` lub końca instrukcji. Nazywa się to **„przechodzeniem dalej” (fall-through)**.

--

*Schemat (5.1) konstrukcja switch-case bez break:*

![Schemat2](https://user-images.githubusercontent.com/71324202/143785138-5385ce36-9450-410b-b754-6cc07647195e.png)

--

*Schemat (5.2) bardziej zaawansowane użycie instrukcji switch-case z break i bez:*

![Schemat3](https://user-images.githubusercontent.com/71324202/143785139-24267703-57fc-40fd-9b2d-063517766286.png)

--

Na początek najlepiej korzystać ze schematu `switch-case-break`, ale znajomość mechanizmu **fall-through** pozwala czasami uprościć kod.

--

## Zadania do samodzielnego wykonania

1. **Kalkulator prosty:**
   Napisz program, w którym użytkownik podaje 2 liczby, następnie znak działania (`+`, `-`, `*`, `/`, `%`). Program wykorzystuje instrukcję `switch-case` do wybrania działania i wypisania wyniku.

2. **Kalkulator z menu:**
   Stwórz kalkulator 2 liczb z **menu wyboru**. W opcjach umieść:

   * zmianę pierwszej liczby,
   * zmianę drugiej liczby,
   * wybór działania do wykonania (`+`, `-`, `*`, `/`, `%`),
   * zakończenie programu.


--

# Więcej o typach zmiennych i nie tylko

--

## **Zasięg zmiennej**
W języku C istnieją dwa rodzaje zasięgów zmiennych. Zmienna globalna i zmienna lokalna. We wszystkich przykładach użytych wcześniej, spotkaliśmy się z deklaracją zmiennych lokalnych, gdyż bardzo rzadko używa się zmiennych globalnych. Zmienną globalną zazwyczaj deklaruje się poniżej dyrektywy preprocesora `#include`. Jest ona wtedy dostępna w całym kodzie i dla każdej funkcji (o funkcjach mowa będzie w kolejnym rozdziale). Jednak każdy kod da się zapisać bez używania zmiennych globalnych i zazwyczaj unika się ich używania (chociaż czasem są przydatne). W zamian za zmienne globalne używa się zmiennych lokalnych. Zmienna lokalna to taka zmienna, do której mamy dostęp tylko w bloku kodu, w którym została zadeklarowana. Blok kodu to kod zawarty pomiędzy nawiasami klamrowymi np. w funkcjach, pętli for, czy instrukcji warunkowej. Do takiej zmiennej nie uda nam się odwołać poza tym blokiem.

--

*Przykład (6.0) zasięg zmiennej*
```
#include <stdio.h>
#include <stdlib.h>
int zmienna_globalna=0;
int main() {
	int zmienna_lokalna_main=1;
	
	if(zmienna_lokalna_main==1)
	{
		int zmienna_lokalna_if=2;
 		printf("%d ",zmienna_globalna); /* dostęp OK */
 		printf("%d ",zmienna_lokalna_main); /* dostęp OK */
 		printf("%d ",zmienna_lokalna_if); /* dostęp OK */
	}
}
```

--

```
 /* ---------------- teraz kod z błędem ---------------------- */
#include <stdio.h>
#include <stdlib.h>
int zmienna_globalna=0;
int main() {
	int zmienna_lokalna_main=1;
	
	if(zmienna_lokalna_main==1)
	{
		int zmienna_lokalna_if=2;
	} /* poza tym nawiasem klamrowym już zmienna_lokalna_if nie jest już widoczna*/
		printf("%d ",zmienna_globalna); /* dostęp OK */
 		printf("%d ",zmienna_lokalna_main); /* dostęp OK */
 		printf("%d ",zmienna_lokalna_if); /* BŁĄD !!!*/

}

```

--

W zmiennych lokalnych istotnym elementem jest przysłanianie zmiennych. Jest to zadeklarowanie zmiennej o tej samej nazwie w innym bloku kodu. Zmienna taka przysłoni zmienną z bloku zewnętrznego, czyli wewnątrz tego bloku stracimy do niej dostęp. Zmienna lokalna może też przysłonić zmienną globalną.

--

*Przykład (6.1) przysłonięcie zmiennej*
```
#include <stdio.h>
#include <stdlib.h>
int zmienna_globalna=0;
int main() {
	int zmienna_lokalna=1;
	
	if(zmienna_lokalna==1)
	{
		int zmienna_lokalna=2; /* przysłania zmienną z main */
 		printf("%d ",zmienna_globalna);
 		printf("%d \n",zmienna_lokalna);
	}
	printf("%d ",zmienna_globalna);
 	printf("%d ",zmienna_lokalna);
}

```

*Wynik działania programu*

>0 2
>
>0 1

--

## **Modyfikatory typów zmiennych oraz stałe**
Modyfikatory typów dają nam większą kontrolę nad rozmiarem pamięci zajmowanym przez zmienną oraz, typem przechowywania wartości. W języku C występują 4 modyfikatory:

- `short` - krótka
- `long` - długa
- `signed` – ze znakiem (+ lub -)
- `unsigned` – bez znaku (tylko +)

--

Dwa pierwsze (`short` i `long`) odpowiadają za rozmiar pamięci zajmowany przez zmienną i można ich używać ze wszystkimi podstawowymi zmiennymi. Kolejne dwa (`signed` i `unsigned`) są odpowiedzialne za typ zapisu danych. W ten sposób zmodyfikujemy zbiór wartości do jakiego może należeć zmienna. Modyfikatorów `signed` i `unsigned` nie można używać z typem zmiennej zmiennoprzecinkowej (`float` i `double`). Każdy z modyfikatorów można użyć samodzielnie – bez deklarowania typu zmiennej. Tak zadeklarowana zmienna, stanie się domyślnie zmienną całkowitą (zapis  `short`  i `short int` są równoznaczne).  

--

|Typ|Liczba bitów N|Zakres wartości : -2^N-1… 2^N-1-1|Kod formatujący|
| - | - | - | - |
|`char`|8 |-128 … 127|%c|
|`short`|16|-32 768 … 32 767|%hd |
|`int` |16|-32 768 … 32 767|%d|
|`int` |32|-2 147 483 648 … 2 147 483 647|%d|
|`long`|32|-2 147 483 648 … 2 147 483 647|%ld |
|`long long`|64|−9 223 372 036 854 775 808 …9 223 372 036 854 775 807|%lld |

--

|Typ|Liczba bitów N|Zakres wartości : -2^N-1… 2^N-1-1|Kod formatujący|
| - | - | - | - |
|`unsigned char`|8|0 … 255|%c|
|`unsigned short`|16|0 … 65 535|%hu |
|`unsigned` (`unsigned int`)|16|0 … 65 535|%u |
|`unsigned` (`unsigned int`)|32|0 … 4294 967 295|%u|
|`unsigned long`|32|0 … 4294 967 295|%ul |

--

W zależności od architektury komputera i kompilatora, zmnienia się rozmiar oraz wartości min i max przedziałów zmiennych typu `int` oraz `unsigned`. 
Zmienna typu `long long` istnieje tylko w nowych kompilatorach.

--

|Typ|Liczba bitów|Liczba cyfr znaczących|Zakres wartości  |Kod formatujący|
| - | - | - | - | - |
|`float` |32|7|3.4 ∙10-38… 3.4 ∙1038|%f|
|`double`|64|15|1.7 ∙10-308…1.7 ∙10308|%lf|
|`long double`|80|19|3.4 ∙10-4932… 1.1 ∙104932|%Lf|

--

Zmienna stała jest zmienną, której wartość nie może ulec zmianie. Jest to przydatne w momentach gdy kiedy chcemy mieć pewność, że żadne działanie nie zmodyfikuje nam wartości zmiennej. Aby stworzyć zmienną stałą należy użyć słowa kluczowego const przed typem (modyfikatorem) zmiennej.

*Przykład (6.2) Deklaracja stałej*
```
const flaot PI=3.14159265359;
/* mamy pewność że zmiennej PI nic nie zmodyfikuje – unikniemy błędów w obliczeniach*/
```

--

W języku C można też stworzyć *stałą symboliczną*. Używa się do tego dyrektywy preprocesora #define. Definicja takiej stałej symbolicznej różni się od zmiennej. Zmienna jest zapisywana do pamięci, natomiast stała symboliczna, jest wykrywana przez kompilator, a jej oznaczenie jest zastępowane odpowiednią frazą w chwili kompilwania (nie jest zapisywana w pamięci). W przykładzie 6.3, wpisując w dowolnym miejscu w kodzie `ARRAY_SIZE` kompilator potraktuje jakby było wpisane 6.

--

*Przykład (6.3) Deklaracja stałej symbolicznej*

`#define ARRAY_SIZE 6`

Poniżej zaimplementowany jest przykład w formie żartu, co można zrobić ze stałą symboliczną. Program działa, ale nie polecam w ten sposób programować.


*Przykład (6.4) Nadużycie stałych symbolicznych*
```
#include <stdio.h>
#include <stdlib.h>
#define e int
#define ee main
#define eee (
#define eeee )
#define eeeee {
#define eeeeee printf
#define eeeeeeeeee \n
#define eeeeeeeeeee ;
#define eeeeeeeeeeee return
#define eeeeeeeeeeeee 0
#define eeeeeeeeeeeeee }

e ee eee eeee
eeeee
	eeeeee eee "Hello World!\n" eeee eeeeeeeeeee
	eeeeeeeeeeee eeeeeeeeeeeee  eeeeeeeeeee
eeeeeeeeeeeeee

```
*Wynik działania programu*

>Hello World!

--

# Pierwsze własne funkcje i rekurencja (C++)

--

## **Podejście proceduralne**

Wszystkie zagadnienia poruszone we wcześniejszych rozdziałach były omawiane przy użyciu programów napisanych w podejściu strukturalnym. Podejście to polega na stworzeniu całego programu wewnątrz funkcji głównej `main`. W praktyce, tego podejścia nie używa się praktycznie wcale. Dużo prościej i przejrzyściej tworzy się kod, korzystając z **podejścia proceduralnego**. Polega ono na tworzeniu własnych **procedur i funkcji** obsługujących poszczególne problemy, a funkcja `main` służy jedynie do złożenia wszystkich funkcji w działający program, spełniający swoje założenia działania.

--

*Schemat (7.0) podejście strukturalne a podejście proceduralne* ([Karol Kuczmarski „Od zera do gierkodera”](http://www.cs.put.poznan.pl/arybarczyk/Kurs%20C++.pdf))

![Schemat0](https://user-images.githubusercontent.com/71324202/143834923-c328668b-ffa6-484f-84f1-89ecfd7e974a.png)

--

## **Deklaracja i tworzenie własnych funkcji**

Aby zadeklarować funkcję należy najpierw podać **typ wartości**, jaką funkcja będzie zwracać. Typy są identyczne jak typy zmiennych (`int`, `char`, `float`, `double`). Warto wspomnieć o typie `void` — funkcja takiego typu **nie zwraca** żadnej wartości (tzw. procedura).

--

Kolejno podajemy **nazwę funkcji** (identyfikator) oraz listę **parametrów** w nawiasach (opcjonalnie). Parametry to zmienne, od których zależy wynik działania funkcji. Ostatnim elementem jest **blok kodu** funkcji. Każda funkcja o typie różnym od `void` musi zwracać wartość poprzez `return`, zgodną z zadeklarowanym typem.


```
typ nazwa_funkcji(typ_zmiennej nazwy_parametrów, …) 
{
    // kod źródłowy funkcji
    // jeżeli typ funkcji to void – return nie występuje
    return wartość_zgodna_z_typem_funkcji; 
    // można też zwrócić zmienną
}
```

--

**Gdzie umieszczać definicje?**
Można zdefiniować funkcję **powyżej** `main` (pełna definicja), albo **poniżej** `main`, a wyżej umieścić **prototyp** (tylko nagłówek: typ, nazwa, lista typów parametrów). Prototyp mówi kompilatorowi: „ta funkcja istnieje – definicja będzie później”. To ułatwia sytuacje, gdy funkcje wywołują się wzajemnie.

--

*Przykład (7.0) deklaracja funkcji przed `main` (C++):*

```cpp
#include <iostream>
using namespace std;

double kwadrat_liczby(double liczba)
{
    return liczba * liczba;
}

int main() 
{
    /* kod main */
    return 0;
}
```

--

*Przykład (7.1) definicja funkcji po `main` (C++):*

```cpp
#include <iostream>
using namespace std;

double kwadrat_liczby(double); // prototyp

int main()
{
    /* kod main */
    return 0;
}

double kwadrat_liczby(double liczba)
{
    return liczba * liczba;
}
```

--

## **Wywołanie funkcji**

Aby **wywołać** funkcję, podajemy jej nazwę i argumenty w nawiasach. Miejsce wywołania zostaje zastąpione **zwróconą wartością**. Dzięki temu funkcję można:

* użyć w wyrażeniu arytmetycznym,
* przypisać do zmiennej,
* przekazać jako **argument** innej funkcji,
* użyć w warunku instrukcji sterującej.

Funkcję typu `void` wywołujemy po prostu przez zapis `nazwa(argumenty);`.

--

*Przykład (7.2) wywołanie funkcji w różnych sytuacjach (C++):*

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

double kwadrat_liczby(double);
int max(int, int);

int main()
{
    double a = kwadrat_liczby(4);
    double b = a + kwadrat_liczby(5);
    int c = max(23, 10);

    cout << fixed << setprecision(0);
    cout << "a=" << setw(4) << a << '\n'
         << "b=" << setw(4) << b << '\n'
         << "c=" << setw(4) << c;
    return 0;
}

double kwadrat_liczby(double liczba)
{
    return liczba * liczba;
}

int max(int a, int b)
{
    return (a > b) ? a : b;
}
```

--

## **Przekazywanie argumentów do funkcji oraz klasa pamięci `static`**

Argumenty przekazywane są do funkcji na podstawie **deklaracji parametrów**. Dla rozróżnienia: w `int max(int a, int b)` – `a` i `b` są **parametrami**, natomiast w wywołaniu `max(23, 10)` wartości `23` i `10` to **argumenty**.

Domyślnie (tak jak w C) w tym przykładzie odbywa się **przekazywanie przez wartość** – do funkcji trafiają **kopie** wartości. Zmiany w parametrach nie wpływają na zmienne przekazane w argumentach.

W przykładzie pokażemy też **lokalną zmienną statyczną** (`static`). Taka zmienna **zachowuje swoją wartość** pomiędzy kolejnymi wywołaniami funkcji (inicjalizacja wykonuje się tylko raz).

--

*Przykład (7.3) wartości zmiennych wewnątrz funkcji i poza nią oraz zmienna lokalna klasy `static` (C++):*

```cpp
#include <iostream>
using namespace std;

void parametry(int a, int b)
{
    static int i = 1;  // inicjalizacja tylko raz
    a = a + 1;
    b = b + 3;
    cout << "\nWEWNATRZ FUNKCJI wywolanie " << i << '\n';
    cout << "a=" << a << " b=" << b;
    i++;
}

int main() {
    int a = 3, b = 5;
    cout << "\nPRZED WYWOLANIEM\n";
    cout << "a=" << a << " b=" << b;

    parametry(a, b);

    cout << "\nPO WYWOLANIU 1\n";
    cout << "a=" << a << " b=" << b;

    parametry(a, b);

    cout << "\nPO WYWOLANIU 2\n";
    cout << "a=" << a << " b=" << b;
    return 0;
}
```

--

*Wynik działania programu:*

```
PRZED WYWOLANIEM
a=3 b=5
WEWNATRZ FUNKCJI wywolanie 1
a=4 b=8
PO WYWOLANIU 1
a=3 b=5
WEWNATRZ FUNKCJI wywolanie 2
a=4 b=8
PO WYWOLANIU 2
a=3 b=5
```

--

To wszystkie informacje potrzebne, aby z powodzeniem stworzyć swoje pierwsze funkcje i zmienić podejście do budowania kodu. Temat ten kryje jednak zdecydowanie więcej możliwości (o wskaźnikach i innych technikach będzie później).

--

## **Funkcje rekurencyjne**

Funkcje rekurencyjne to takie funkcje, które **wywołują same siebie**. Kluczowe pojęcia:

* **warunek stopu** – przypadek, dla którego znamy wynik i **kończymy** rekurencję,
* **krok rekurencyjny** – wywołanie funkcji z „bliższym” argumentem prowadzącym do warunku stopu.

--

Klasyczny przykład: **silnia**.

![Rysunek1](https://user-images.githubusercontent.com/71324202/143834929-27f96821-8526-40fe-afee-24855d57a9fb.png)

Dla `n=1` (oraz standardowo także `n=0`) wynik jest znany. Dla pozostałych `n` mamy zależność `n * f(n-1)`.

--

*Przykład (7.4) funkcja silnia rekurencyjnie (C++):*

```cpp
#include <iostream>
using namespace std;

unsigned long long silnia(unsigned n);

int main() 
{
    cout << silnia(3);
    return 0;
}

unsigned long long silnia(unsigned n)
{
    // obsłużenie przypadku n=0: 0! = 1
    if(n == 0) return 1ULL;

    // warunek stopu: 1! = 1
    if(n == 1) return 1ULL;

    // krok rekurencyjny: n * (n-1)!
    return n * silnia(n - 1);
}
```

--

Poniżej schemat obrazuje najpierw kolejne **zstępowania** do warunku stopu, a potem **powroty** z obliczeniami.

*Schemat (7.1) działanie funkcji silnia z przykładu 7.4, dla argumentu n=4.*

![Schemat1](https://user-images.githubusercontent.com/71324202/143834927-11d727cf-d571-40df-a0d4-c460214ff30d.png)

--

## **Zadania do samodzielnego wykonania**

1. Stwórz funkcje `max(a,b)` i `min(a,b)`, które będą zwracać odpowiednio większą i mniejszą z podanych liczb.
2. Stwórz funkcję `silnia(a)`, która **iteracyjnie** (pętlą) liczy wartość silni z podanej liczby.
3. Stwórz funkcję `potega(liczba, wykladnik)`, która będzie **iteracyjnie** liczyć wartość potęgi o podanych parametrach.
4. Stwórz funkcję `potega(liczba, wykladnik)`, która będzie **rekurencyjnie** liczyć wartość potęgi o podanych parametrach.

--

5. Korzystając z własnych funkcji stwórz **kalkulator z menu** dający możliwość wykonania obliczeń podanych poniżej. Każda operacja powinna być realizowana przez **osobną** funkcję/procedurę:

   1. dodawanie *n* liczb;
   2. odejmowanie od liczby aż do momentu podania `0`;
   3. mnożenie dwóch liczb;
   4. dzielenie liczby;
   5. potęgowanie;
   6. kwadrat liczby;
   7. silnia;

--

6. Stwórz funkcję liczącą wartość *n*-tego wyrazu [Ciągu Fibonacciego](https://pl.wikipedia.org/wiki/Ci%C4%85g_Fibonacciego).
7. Stwórz funkcję liczącą **sumę** wszystkich wyrazów [Ciągu Fibonacciego](https://pl.wikipedia.org/wiki/Ci%C4%85g_Fibonacciego) kończąc na *n*-tym wyrazie.
8. Stwórz funkcję liczącą wartość *n*-tego wyrazu ciągu określonego wzorem:

![image](https://user-images.githubusercontent.com/71324202/143841510-fa248fbc-8e7d-4395-af52-66133199df04.png)

9. Napisz funkcje `ceiling`, `floor` i `round`, odzwierciedlające funkcje matematyczne sufit/podłoga/zaokrąglenie (skorzystaj z **jawnej konwersji** typów).

--


 