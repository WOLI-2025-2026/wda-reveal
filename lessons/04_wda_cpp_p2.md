# Instrukcja wyboru switch case.

--

## Menu wyboru _switch-case-break_

Instrukcja wyboru w programowaniu umożliwia wybór instrukcji do wykonania spośród wielu dostępnych opcji. Bardzo dobrze sprawdza się przy tworzeniu menu. W języku C składa się ona z instrukcji switch(argument)oraz opcji wyboru case wartość\_argumentu:_._ W praktyce najczęściej wykorzystywaną opcją jest używanie instrukcji wyboru za pomocą instrukcji switch case break.Takie użycie jest bardzo intuicyjne i porównywalne z użyciem instrukcji warunkowej sprawdzającej równość, a default staje się odpowiednikiem frazy else.

_Schemat (5.0) instrukcja wielokrotnego wyboru swich case break_

![Schemat1](https://user-images.githubusercontent.com/71324202/143785129-e9cbc369-dca7-419a-9da7-f4261d58f843.png)

--

_Przykład (5.0) Menu wyboru zbudowane za pomocą switch case break._

```
#include <stdio.h>
#include <stdlib.h>

int main() {
	
	int wybor;
	for(;;)/* pętla for bez wyrażeń – nieskończona */
	{
		printf("\nMENU\n");
		printf("1. Powiedz czesc!\n");
		printf("2. Opowiedz zart.\n");
		printf("3. Pozegnaj sie.\n");
		printf("Wybierz opcje: ");
		fflush(stdin); /* czyszczenie bufora stdin */
		scanf(" %d",&wybor);
		switch(wybor)
		{
		  case 1:
			{
			  printf("Czesc!\n");
			}break;
		  case 2:
			{
			  printf("-Czym rozni sie doswiadczony informatyk od poczatkujacego?\n");
			  printf("-Poczatkujacy uwaza, ze 1KB to 1000B, a doswoadczony jest pewnien");
			  printf(", ze 1km to 1024m.\n");
			}break;
		  case 3:
			{
			  printf("Do zobaczenia!\n");
			  exit(0); /* Zakończenie działania programu */
			}break;
		  default: 
			{
			  printf("Nie ma takiej opcji\n");
			}break;
		}	
	}

	return 0;
}


```

--

## Więcej o switch-case

Instrukcji switch case można jedna używać bez instrukcji przerwania. Wtedy jej działanie przełącza program do odpowiedniego miejsca w kodzie i następnie wykonuje już wszystkie poniższe instrukcje nie zwracając uwagi, w którym przypadku (_case_) się znajduje. Najłatwiej to zrozumieć poprzez analizę schematów (5.1 i 5.2) znajdujących się poniżej.

--

_Schemat (5.1) konstrukcja switch case bez break_

![Schemat2](https://user-images.githubusercontent.com/71324202/143785138-5385ce36-9450-410b-b754-6cc07647195e.png)


--

_Schemat (5.2) bardziej zaawansowane użycie instrukcji switch case z break i bez._

![Schemat3](https://user-images.githubusercontent.com/71324202/143785139-24267703-57fc-40fd-9b2d-063517766286.png)


--

Na początku zaleca się jednak korzystać z instrukcji _switch case break_, ale niedokładnością w omówieniu tematu byłoby nieporuszenie potencjału jaki kryje w sobie instrukcja wielokrotnego wyboru.

--

## Zadania do samodzielnego wykonania:

1. Stwórz kalkulator, w którym użytkownik podaje 2 liczby, następnie podaje znak działania jakie chce wykonać (+, -, \*, /, %). Wykorzystaj instrukcję _switch case_. Program wykonuje działanie i wyświetla wynik.
2. Stwórz kalkulator 2 liczb z menu. W opcjach menu zawrzyj: zmianę pierwszej liczby, zmianę drugiej liczby, wybór działania do wykonania (+, -, \*, /, %) oraz zakończenie programu. Po każdorazowej zmianie danych program oblicza zadane działanie i wyświetla je powyżej menu, oraz daje możliwość dalszego korzystania z programu.

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

Zmienna stała jest zmienną, której wartość nie może ulec zmianie. Jest to przydatne w momentach gdy kiedy chcemy mieć pewność, że żadne działanie nie zmodyfikuje nam wartości zmiennej. Aby stworzyć zmienną stałą należy użyć słowa kluczowego `const` przed typem (modyfikatorem) zmiennej.

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

# Pierwsze własne funkcje i rekurencja

--

## **Podejście proceduralne**
Wszystkie zagadnienia poruszone we wcześniejszych rozdziałach były omawiane przy użyciu programów napisanych w podejściu strukturalnym. Podejście to polega na stworzeniu całego programu wewnątrz funkcji głównej `main`. W praktyce, tego podejścia nie używa się praktycznie wcale. Dużo prościej i przejrzyściej tworzy się kod korzystają z podejścia proceduralnego. Polega ono na tworzeniu własnych procedur i funkcji obsługujących poszczególne problemy, a funkcja `main` służy jedynie do złożenia wszystkich funkcji w działający program, spełniający swoje założenia działania.

--

*Schemat (7.0) podejście strukturalne a podejście proceduralne* ([Karol Kuczmarski „Od zera do gierkodera”](http://www.cs.put.poznan.pl/arybarczyk/Kurs%20C++.pdf))

![Schemat0](https://user-images.githubusercontent.com/71324202/143834923-c328668b-ffa6-484f-84f1-89ecfd7e974a.png)

--

## **Deklaracja i tworzenie własnych funkcji**
Aby zadeklarować funkcję należy najpierw podać typ wartości jaką funkcja będzie zwracać. Typy wartości są identyczne jak typy wartości zmiennych (`int`, `char`, `float`, `double`). Warto jeszcze wspomnieć tutaj o typie używanym często jako typ funkcji `void`, który nie zwraca żadnej wartości. Funkcja typu `void` nazywana jest procedurą. Drugą składową potrzebną do stworzenia funkcji jest jej nazwa (identyfikator). Również jak w przypadku zmiennych, nazwę funkcji nadaje programista. Po identyfikatorze funkcji konieczne jest wystąpienie nawiasów, wewnątrz których, opcjonalnym jest zadeklarowanie parametrów funkcji. Parametry funkcji to zmienne, podawane funkcji od których zależy wynik działania funkcji. Ostatnim elementem składowym funkcji jest, blok kodu źródłowego funkcji. Należy pamiętać, że każda funkcja określona typem różnym niż `void` musi zwracać wartość za pośrednictwem operatora *return,* odpowiadającą typowi funkcji. 

--

```
typ nazwa_funkcji(typ_zmiennej nazwy_parametrów,…) 
{
/* kod źródłowy funkcji */
/* jeżeli typ funkcji to void to return nie występuje */
	return wartość_zgodna_z_typem_funkcji; 
/* można użyć zmiennej  jako wartości zwracanej*/
}

```

--

Deklaracji funkcji można dokonać powyżej lub poniżej funkcji `main`. W pierwszym przypadku stosujemy pełen zapis funkcji wraz z jej kodem źródłowym powyżej funkcji `main` dzięki czemu wewnątrz `main` możemy swobodnie wywoływać działanie naszej funkcji. Taki sposób jednak powoduje pewne problemy, kiedy tworzymy więcej niż jedną własną funkcję, a one odwołują się do siebie nawzajem. Dlatego preferowaną deklaracją użycia kodu, jest deklaracja funkcji poniżej funkcji `main`. W takim przypadku powyżej funkcji `main`, deklarujemy w sposób skrócony istnienie funkcji poprzez podanie jej typu, nazwy oraz typów parametrów. Takie zadeklarowanie funkcji, nazywa się prototypem i daje sygnał kompilatorowi „ta funkcja istnieje, ale jej kod jest podany w innym miejscu”, dzięki czemu unikamy problemów z wywoływaniem funkcji przez siebie nawzajem. Ciało takiej funkcji umieszczamy wtedy poniżej funkcji `main`.

--

*Przykład (7.0) deklaracja funkcji przed `main`*

```
#include <stdio.h>
#include <stdlib.h>

double kwadrat_liczby(double liczba)
{
	return liczba*liczba;
}

int main() 
{
	/* kod main */
	return 0;
}


```

--

*Przykład (7.1) definicja funkcji po `main`*

```
#include <stdio.h>
#include <stdlib.h>

double kwadrat_liczby(double);

int main()
{
	/* kod main */
	return 0;
}

double kwadrat_liczby(double liczba)
{
	return liczba*liczba;
}

```

--

## **Wywołanie funkcji**
Aby wywołać funkcję, należy podać jej identyfikator, wraz z nawiasem, wewnątrz którego podamy argumenty odpowiadające kolejnym parametrom funkcji. Działanie funkcji spowoduje, że miejsce, w którym zostanie wywołana zostanie zastąpione zwracaną wartością. Można taką funkcję wywołać wewnątrz operacji arytmetycznej (o ile typ funkcji jest odpowiedni), przy operacji przypisania (jako argument, który ma zostać przypisany, nie można przypisać wartości do funkcji, ponieważ nie jest tzw. L-wartością), lub jako argument innej funkcji, instrukcji warunkowej, w której typ zwracanej wartości jest dopuszczony. Innymi słowy funkcji można użyć wszędzie tam, gdzie ma być użyta wartość, którą zwraca dana funkcja. Funkcję typu `void`, która nie zwraca wartości wywołuje się po prostu wypisując jej nazwę i argumenty.

--

*Przykład (7.2) wywołanie funkcji w różnych sytuacjach*

```
#include <stdio.h>
#include <stdlib.h>

double kwadrat_liczby(double);
int max(int,int);

int main()
{
	double a = kwadrat_liczby(4);
	double b = a + kwadrat_liczby(5);
	int c = max(23,10);
	printf("a=%4.0lf \nb=%4.0lf \nc=%4d",a,b,c);
	return 0;
}

double kwadrat_liczby(double liczba)
{
	return liczba*liczba;
}

int max(int a, int b)
{
	return (a>b)? a : b;
}

```

--


## **Przekazywanie argumentów do funkcji oraz klasa pamięci `static`** 
Argumenty przekazywane są do funkcji, w miejscu deklaracji parametrów. Aby ułatwić rozróżnienie parametru i argumentu posłużę się przykładem (7.2). Funkcja `int max(int a, int b)` ma dwa parametry a i b, natomiast w funkcji `main` w wywołaniu funkcji `max(23,10);` za argument podane jest 23 i 10. Jako argument funkcji możemy podać wartość stałą, lub zmienną. Należy pamiętać jednak, że wartość argumentu nie jest przekazywana do funkcji w oryginale, a jedynie kopiowana do parametru, przez co działanie funkcji nie wpłynie na zmienne podane w argumencie. Do sprawdzenia tego posłuży nam przykład (7.3). Jest tam również przestawiona zmienna funkcji kasy `static`. Jej działanie jest o tyle różne, od działania zwykłej zmiennej lokalnej, że obszar pamięci zarezerwowany przez tą zmienną, jest zarezerwowany przez cały czas działania programu, a ona sama deklarowana jest tylko raz. Więc linijka `static int i=1;` wykona się tyko podczas pierwszego wywołania funkcji, a w każdym kolejnym zostanie ona pominięta. Trochę tak, jakby zmienna typu `static` zachowywała się jak zmienna globalna, jednak z ograniczonym dostępem. Zmodyfikowanie zmiennej tej w dowolnym momencie, zostanie zapamiętane i zmienna ta przyjmie inną wartość również w kolejnym wywołaniu tej funkcji. 

--

*Przykład (7.3) wartości zmiennych wewnątrz funkcji i poza nią oraz zmienna lokalna funkcji klasy `static`*

```
#include <stdio.h>
#include <stdlib.h>

void parametry(int a, int b)
{
	static int i=1;
	a=a+1;
	b=b+3;
	printf("\nWEWNATRZ FUNCKJI wywolanie %d\n", i) ;
	printf("a=%d b=%d",a,b);
	i++;
}

int main() {
	int a=3,b=5;
	printf("\nPRZED WYWOLANIEM\n") ;
	printf("a=%d b=%d",a,b);
	
	parametry(a,b);
	
	printf("\nPO WYWOLANIU 1\n") ;
	printf("a=%d b=%d",a,b);
	
	parametry(a,b);
	
	printf("\nPO WYWOLANIU 2\n") ;
	printf("a=%d b=%d",a,b);
	return 0;
}

```

--

## **Funkcje rekurencyjne**
Funkcje rekurencyjne to takie funkcje, które odwołują się do samej siebie. Słynne przysłowie o rekurencji mówi, że aby zrozumieć rekurencję, najpierw należy zrozumieć rekurencję. Brzmi skomplikowanie, ale wcale takie nie jest. Najłatwiej jest rekurencję wytłumaczyć na przykładzie, co stanie się zaraz. Bardzo istotą rzeczą w funkcjach rekurencyjnych jest warunek stopu i krok rekurencyjny. Jak już było wspomniane funkcja rekurencyjna musi wywoływać samą siebie, ale nie może tego wykonywać w nieskończoność. Dlatego wewnątrz funkcji rekurencyjnej jest potrzebny warunek stopu, czyli definicja wartości funkcji dla znanego argumentu. Krok rekurencyjny to kolejna bardzo ważna rzecz, jest to nic innego jak odpowiednie wywołanie funkcji rekurencyjnej wewnątrz niej z odpowiednią zmianą parametru, tak aby funkcja dążyła zawsze do warunku stopu. Jako funkcję rekurencyjną, można zdefiniować funkcję silnia

![Rysunek1](https://user-images.githubusercontent.com/71324202/143834929-27f96821-8526-40fe-afee-24855d57a9fb.png)

--

Gdzie przypadek, kiedy n=1 jest warunkiem stopu, a wszelkie inne wartości są warunkiem ogólnym. f(n-1) jest krokiem rekurencyjnym w kierunku warunku stopu, zakładając, że n jest podana jako nieujemna liczba całkowita. Taką funkcję reprezentuje program z przykładu (7.4).

--

*Przykład (7.4) funkcja silnia rekurencyjnie*

```
#include <stdio.h>
#include <stdlib.h>

unsigned silnia (unsigned);

int main() 
{
	printf("%d", silnia(3));
	return 0;
}

unsigned silnia (unsigned n)
{
/* obsłużenie wyjątku n=0 */
	if(n==0)
		return 0;
/* warunek stopu ------ 1 dla n=1 */
	if(n==1)
		return 1;
/* warunek ogólny ------ n*f(n-1)  */
	return n*silnia(n-1);
}

```

*Wynik działania programu:*

>6

--

Przykład przedstawiający problem blokowo znajduje się poniżej – schemat (7.1). W jego pierwszej części zatytułowanej jako *Wywołanie kolejnych funkcji silnia – rekurencyjnie* , mamy pokazane wywołanie wszystkich funkcji aż do uzyskania warunku stopu. W warunku stopu wartość funkcji jest znana, więc kolejna część *Obliczanie kolejnych argumentów…* pokazuje nam kolejne wykonania instrukcji `return` w postaci strzałek powrotnych. W ten sposób wartości kolejnych wywołań funkcji stają się znane, aż do momentu w którym uzyskamy wynik dla interesującego nas argumentu. 

--

*Schemat (7.1) działanie funkcji silnia z przykładu 7.4, dla argumentu n=4.*

![Schemat1](https://user-images.githubusercontent.com/71324202/143834927-11d727cf-d571-40df-a0d4-c460214ff30d.png)

--

## **Zadania do samodzielnego wykonania**
1. Stwórz funkcje max(a,b) i min(a,b), które będą zwracać większą\mniejszą z podanych liczb.
2. Stwórz funkcję silnia(a), która będzie iteracyjnie (przy pomocy pętli) liczyć wartość silni z podanej liczby.
3. Stwórz funkcję `potega(liczba, wykladnik)`, która będzie iteracyjnie liczyć wartość potęgi o podanych parametrach.
4. Stwórz funkcję `potega(liczba, wykladnik)`, która będzie rekurencyjnie liczyć wartość potęgi o podanych parametrach.

--

5. Korzystając z własnych funkcji stwórz kalkulator z menu dający możliwość wykonania obliczeń podanych poniżej. Każda z operacji powinna być wykonywana przez osobną funkcję/procedurę.
	1. dodawanie n liczb;
	2. odejmowanie od liczby aż do momentu podania '0';
	3. mnożenie dwóch liczb;
	4. dzielenie liczby;
	5. potęgowanie;
	6. kwadrat liczby;
	7. silnia;

--

6. Stwórz funkcję liczącą wartość n-tego wyrazu [Ciągu Fibonacciego](https://pl.wikipedia.org/wiki/Ci%C4%85g_Fibonacciego)
7. Stwórz funkcję liczącą sumę wszystkich wyrazów [Ciągu Fibonacciego](https://pl.wikipedia.org/wiki/Ci%C4%85g_Fibonacciego) kończąc na n-tym wyrazie.
8. Stwórz funkcję liczącą wartość n-tego wyrazu ciągu określonego wzorem:

![image](https://user-images.githubusercontent.com/71324202/143841510-fa248fbc-8e7d-4395-af52-66133199df04.png)

9. Napisz funkcje ceiling, floor i round, odzwierciedlające funkcje matematyczne sufit i podłoga oraz zaokrąglenie matematyczne (skorzystaj z jawnej konwersji typów).

 