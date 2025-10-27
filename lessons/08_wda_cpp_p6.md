# 💻 Lekcja: Dynamiczne alokowanie pamięci w C++

--

## 🎯 Cele lekcji
Po tej lekcji będziesz potrafić:
- wyjaśnić, czym jest dynamiczna alokacja pamięci,
- tworzyć i usuwać zmienne oraz tablice dynamiczne,
- wykorzystywać wskaźniki w zarządzaniu pamięcią,
- korzystać z kontenera `std::vector` do dynamicznego przechowywania danych.

--

## 🧩 1. Pamięć statyczna a dynamiczna

### 📘 Statyczna alokacja
Zmienna istnieje tylko w zakresie, w którym została zdefiniowana.
```cpp
int x = 10;  // statyczna alokacja
```

### 📘 Dynamiczna alokacja
Tworzy zmienne w czasie działania programu.
```cpp
int *p = new int;  // dynamiczna alokacja
*p = 42;
delete p;          // zwolnienie pamięci
```

--

### 🧠 Zadanie 1
Utwórz program, który:
- dynamicznie tworzy zmienną `double`,
- wczytuje wartość od użytkownika,
- wyświetla jej kwadrat,
- zwalnia pamięć po zakończeniu działania.

--

## ⚙️ 2. Dynamiczne tablice

### 📗 Przykład
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Podaj rozmiar tablicy: ";
    cin >> n;

    int *tab = new int[n];

    for (int i = 0; i < n; i++) tab[i] = i * i;

    for (int i = 0; i < n; i++) cout << tab[i] << " ";
    cout << endl;

    delete[] tab;  // zwolnienie pamięci
}
```

### 💡 Wyjaśnienie
`new int[n]` przydziela tablicę o rozmiarze `n`.  
`delete[] tab` zwalnia całą tablicę.

--

### 🧠 Zadanie 2
Napisz program, który:
- tworzy tablicę `n` liczb całkowitych,
- wczytuje wartości od użytkownika,
- oblicza średnią,
- wyświetla liczby większe od średniej,
- zwalnia pamięć po zakończeniu.

--

## ⚙️ 3. Wskaźniki i dynamiczna pamięć

### 📗 Przykład
```cpp
int *p = new int(10);
cout << "Adres: " << p << ", wartość: " << *p << endl;
delete p;
```

### 💡 Uwaga
Nie wolno odwoływać się do wskaźników po `delete`!
```cpp
int *p = new int(5);
int *q = p;
delete p;
cout << *q; // ❌ niezdefiniowane zachowanie
```

--

### 🧠 Zadanie 3
1. Utwórz dynamiczną tablicę 10 elementów.  
2. Utwórz wskaźnik wskazujący na środkowy element.  
3. Wyświetl jego wartość i adres.  
4. Zwalnij pamięć po zakończeniu.

--

## ⚙️ 4. Kontener `std::vector` — dynamiczna tablica

### 📗 Przykład użycia
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<int> liczby = {5, 2, 9, 1};

    liczby.push_back(7);  // dodanie
    sort(liczby.begin(), liczby.end());

    for (int x : liczby) cout << x << " ";
    cout << endl;

    liczby.pop_back();    // usunięcie ostatniego elementu
}
```

### 💡 Wektory automatycznie zarządzają pamięcią!
Nie musisz używać `new` ani `delete`.

--

### 🧠 Zadanie 4
1. Napisz program, który:
   - tworzy wektor `int`,  
   - pozwala dodać nową liczbę,  
   - usuwa element o wybranym indeksie,  
   - sortuje i wyświetla zawartość.

--

## 🧾 Podsumowanie

| Pojęcie | Opis |
|----------|------|
| `new` / `delete` | dynamiczna alokacja / zwalnianie pamięci |
| `new[]` / `delete[]` | dynamiczne tablice |
| Wskaźnik (`*`) | dostęp do danych w pamięci |
| `std::vector` | automatyczna dynamiczna struktura danych |

--

## 🧩 Zadanie końcowe
Stwórz program, który:
- wczytuje dowolną liczbę ocen uczniów do `std::vector<double>`,
- umożliwia dodawanie i usuwanie ocen,
- oblicza średnią i sortuje oceny,
- kończy działanie po wpisaniu `exit`.
