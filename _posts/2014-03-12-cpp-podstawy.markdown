---
layout: post
title: Podstawy C++ - zmienne, warunki, wejście/wyjście
tags: lesson
---

Do pisania programów w C++ używamy narzędzia Dev-C++ ([ściągnij Dev-C++](http://prdownloads.sourceforge.net/dev-cpp/devcpp-4.9.9.2_setup.exe)).
Programy zapisujemy jako pliki z rozszerzeniem `cpp`, na przykład `program.cpp`.
Po zapisaniu pliku klawiszem `F9` uruchamiamy program. Jeżeli wystąpią błędy
kompilacji dowiemy się o tym w okienku u dołu ekranu.

## Szablon programu

Póki co, jak amen w pacierzu, nasze programy zaczynamy następująco:

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    // Tu będzie kod

    return 0;
}
{% endhighlight %}

(Podpowiedź: jeżeli linia zaczyna się od znaków `//`, to jest to komentarz i
cały tekst do końca linii zostanie zignorowany - w ten sposób możemy robić
notatki w kodzie).

## Zmienne

W C++ zanim będziemy używać jakiejś zmiennej musimy ją najpierw zadeklarować,
czyli powiedzieć kompilatorowi, że będziemy jej używać. Na przykład:

{% highlight cpp %}
int x;
x = 10;
{% endhighlight %}

W pierwszej linii mówimy "drogi kompilatorze, będę potrzebował pamiętać jedną
liczbę; niech ona nazywa się `x`". W kolejnej linii wykonujemy przypisanie.
W dalszej części programu pod nazwą `x` będziemy mieć dostęp do wartości `10`.

Możemy też użyć komputer do przechowania napisu. W tym przypadku mówimy, że zmienna
jest typu `string` zamiast `int`. Przykład:

{% highlight cpp %}
string imie;
imie = "Ala";
{% endhighlight %}

## Wejście/wyjście

Jeżeli zmienialibyśmy zmienne tylko w pamięci komputera to nie byłoby to bardzo
użyteczne. Musimy umieć zapytać użytkownika o liczbę i wypisać mu wynik.

Do wczytywania służy konstrukcja `cin`. Najlepiej zobaczyć to na przykładzie:

{% highlight cpp %}
int x, y; // Możemy zadeklarować dwie zmienne w jednej linii
cin >> x >> y; // Wczytujemy z klawiatury kolejno liczby x i y
{% endhighlight %}

Wypisywanie wygląda podobnie - zamiast `cin` mamy `cout` i strzałki prowadzą w
drugą stronę. Kierunek strzałek można zapamiętać tak, że z `cin` wyciągamy
liczby a do `cout` wkładamy.

{% highlight cpp %}
int x;
x = 10;
cout << x;
{% endhighlight %}

Możemy wypisywać również napisy (podajemy je w cudzysłowach) i nowe linie (używając
`endl`). Poniżej znajduje się pełny program, który należy skopiować do Dev-C++ i uruchomić na
swoim komputerze.

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;
int main() {
    int x, y, z;
    x = 10;
    y = 20;
    cout << "Liczba x to " << x << " a y to " << y << endl;

    cout << "Podaj liczbe: ";
    cin >> z;

    cout << "Wpisales " << z << endl;

    return 0;
}
{% endhighlight %}

## Działania na liczbach

Liczby w języku C++ możemy dodawać, odejmować i mnożyć używając znaków `+`, `-` i `*`.
Dla przykładu:

{% highlight cpp %}
int x, y, z;
x = 10;
y = 20;
z = (y - x + 2) * 5; // teraz w z jest liczba 60
{% endhighlight %}

Dzielenie (oznaczane znakiem `/`) zachowuje się inaczej niż to znane wam z zajęć
matematyki: `5 / 2 = 2`. Wynik dzielenia jest zaokrąglany w dół. Dzielenie przez
`0` jest błędem i spowoduje ono zakończenie działania programu.

Mamy do dyspozycji jeszcze operację reszty z dzielenia (inaczej modulo) oznaczaną
przez `%`.

Mając to wszystko do dyspozycji możemy napisać prosty kalkulator:

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    int x, y;

    cout << "Podaj dwie liczby: ";
    cin >> x >> y;

    cout << "x + y = " << x + y << endl;
    cout << "x - y = " << x - y << endl;
    cout << "x * y = " << x * y << endl;

    // Jeżeli y będzie równe 0, to program w tym miejscu zakończy się błędem
    cout << "x / y = " << x / y << endl;
    cout << "x % y = " << x % y << endl;

    return 0;
}
{% endhighlight %}

Zachęcam do wpisywania różnych liczb w kalkulator i zobaczenia jak komputer
radzi sobie z rachunkami.

A tu mała wprawka: zastanów się co wypisze poniższy program zanim go uruchomisz!

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    int x, y, z;

    x = 2;
    y = 3;
    z = 10;
    cout << x + y + z << endl;

    x = x * 2;
    cout << x + y + z << endl;

    z = z - y;
    cout << z - x + 2 * y << endl;

    x = 1;
    cout << x * y * z << endl;

    x = y;
    y = z;

    cout << "x = " << x << endl;
    cout << "y = " << y << endl;
    cout << "z = " << z << endl;

    return 0;
}
{% endhighlight %}

## Wyrażenia warunkowe

W powyższym programie nie chcielibyśmy wykonywać dzielenia ani modulo, jeżeli
jako drugą liczbę użytkownik podał 0. Jak to zrobić?

W języku C++ mamy instrukcję `if` (po polsku "if" znaczy "jeżeli"). Schemat
jej użycia:

{% highlight cpp %}
if([warunek logiczny]) {
    // Fragment kodu, który wykona się tylko wtedy,
    // gdy warunek jest prawdziwy.
} else {
    // Fragment kodu, który wykona się tylko wtedy,
    // gdy warunek *NIE* jest prawdziwy.
}
{% endhighlight %}

Jeżeli w przypadku, gdy warunek jest fałszywy nie chcemy nic robić, to możemy
pominąć instrukcję `else`:

{% highlight cpp %}
if([warunek logiczny]) {
    // Fragment kodu, który wykona się tylko wtedy,
    // gdy warunek jest prawdziwy.
}
// Gdy warunek jest fałszywy, to kod "pod if'em" się nie
// wykona i zaczniemy od razu wykonywać ten fragment.
{% endhighlight %}

Jakie mamy do dyspozycji warunki logiczne? Możemy sprawdzić, czy:

- dwie liczby są równe, np. `x == y`, lub bardziej złożone `x == 25 * y + 2`,
- dwie liczby są różne, np. `x != y`, lub bardziej złożone `x != 25 * y + 2`,
- jedna liczba jest większa od drugiej: `x > y`, lub bardziej złożone `x + 10 > 2 * y`;
  podobnie dla `>`, `<=` i `>=`.

Przykładowo, tak wygląda poprawiona wersja kalkulatora:
{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    int x, y;

    cout << "Podaj dwie liczby: ";
    cin >> x >> y;

    cout << "x + y = " << x + y << endl;
    cout << "x - y = " << x - y << endl;
    cout << "x * y = " << x * y << endl;

    if(y != 0) {
        cout << "x / y = " << x / y << endl;
        cout << "x % y = " << x % y << endl;
    }

    return 0;
}
{% endhighlight %}

Teraz napiszemy program, który:

- poprosi użytkownika o wpisanie temperatury na dworze (w stopniach Celsiusza),
- wypisze mu, czy jest odpowiednia temperatura do gry w piłkę.

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    int temperatura;

    cout << "Podaj temperature: ";
    cin >> temperatura;

    if(temperatura > 10 && temperatura < 30) {
        cout << "Mozna grac" << endl;
    } else {
        cout << "Nie radze grac" << endl
    }

    return 0;
}
{% endhighlight %}

Pojawiła się tu nowa rzecz: w warunku chcieliśmy powiedzieć, że temperatura jest
większa od 10 stopni *i* mniejsza od 30 stopni. Możemy to zrobić posługując się
operatorem `&&`. Jeżeli chcemy powiedzieć *lub* piszemy `||`. Poniższy program
działa tak samo jak poprzedni (sprawdź!):

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    int temperatura;

    cout << "Podaj temperature: ";
    cin >> temperatura;

    if(temperatura <= 10 || temperatura >= 30) {
        cout << "Nie radze grac" << endl
    } else {
        cout << "Mozna grac" << endl;
    }

    return 0;
}
{% endhighlight %}

## Bardziej skomplikowane wyrażenia warunkowe

Kolejny przykład to program wczytujący dwie liczby i:

- wypisujący "WIEKSZA", jeżeli pierwsza jest większa od drugiej,
- wypisujący "ROWNE", jeżeli liczby są równe,
- wypisujący "MNIEJSZA", jeżeli pierwsza liczba jest mniejsza od drugiej.

Pierwsze podejście mogłoby wyglądać tak:

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    int x, y;

    // Od teraz już nie wypisujemy prośby "wpisz liczby": użytkownik
    // domyśli się, że musi to zrobić, a na themisie NIE WOLNO wypisywać
    // takich próśb.
    cin >> x >> y;

    if(x < y) {
        cout << "MNIEJSZA" << endl;
    } else {
        if(x == y) {
            cout << "ROWNE" << endl;
        } else {
            // Dlaczego nie potrzebuję napisać tu
            // if(x > y) { ... } ?
            cout << "WIEKSZA" << endl;
        }
    }

    return 0;
}
{% endhighlight %}

Jeżeli zdarzy nam się tak, że w `else` od razu zaczynamy kolejnym `if`em i
nie robimy tam nic więcej, to możemy to skrócić w następujący sposób:

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    int x, y;

    cin >> x >> y;

    if(x < y) {
        cout << "MNIEJSZA" << endl;
    } else if(x == y) {
        cout << "ROWNE" << endl;
    } else {
        cout << "WIEKSZA" << endl;
    }

    return 0;
}
{% endhighlight %}

## Więcej przykładów

Rozwiązanie zadania "Kwadrat sumy" z themisa:

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    int x, y, wynik;

    cin >> x >> y;
    wynik = (x + y) * (x + y);
    cout << wynik << endl;

    // Można zamienić poprzednią linię na:
    // cout << (x + y) * (x + y) << endl;

    return 0;
}
{% endhighlight %}

Rozwiązanie zadania "RAMMOD" bez korzystania z operatora `%`:

{% highlight cpp %}
#include <iostream>
#include <string>

using namespace std;

int main() {
    int x, y, z, m;

    cin >> x >> y;
    z = x / y;
    m = x - z * y;

    cout << m << endl;

    return 0;
}
{% endhighlight %}

## Co dalej?

W następnym odcinku opowiemy sobie o pętlach w języku C++.
