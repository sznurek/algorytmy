---
layout: post
title: Zajęcia 1 - podstawy Maszyny RAM
tags: lesson
---

Na pierwszych zajęciach poznaliśmy ciąg Fibonacciego, nauczyliśmy
się pisać proste programy w maszynie RAM oraz dowiedzieliśmy się
czegoś o grach "w 21" i "w trzy stosy".

## Ciąg Fibonacciego
Ciąg Fibonacciego to ciąg liczb naturalnych (czyli większych lub równych zero,
bez części ułamkowej). Zaczyna się od liczb 1 i 1, a każdy kolejny element
jest sumą dwóch poprzednich. Początkowy fragment ciągu to `1 1 2 3 5 8 13 21
34 55 89 ...`

Można to sprawdzić samemu:

    2 = 1 + 1
    3 = 2 + 1
    5 = 3 + 2
    8 = 5 + 3
    (...)

## Maszyna RAM
Pierwsze programy pisaliśmy w Maszynie RAM. Można ją pobrać ze strony
autora: [Maszyna RAM](http://www.szkup.com/download/RamMachineNet20.zip).

Przypomnę zestaw instrukcji:

* `read n` - wczytaj liczbę z taśmy wejściowej do komórki pamięci o numerze `n`,
* `write n` - wypisz zawartość komórki o numerze `n` na taśmę wyjściową,
* `add n` - dodaj liczbę z `n`-tej komórki pamięci do komórki o numerze `0` i
  zapisz wynik działania w komórce `0`.

Przykładowy program w maszynie RAM: wczytanie dwóch liczb z wejścia i wypisanie
ich w odwrotnej kolejności:

    read 0
    read 1
    write 1
    wrtie 0

## Gra "w 21"
Jaś i Małgosia grają w prostą grę: zaczynając od liczby 21 na przemian odejmują
od niej 1, 2, 3 lub 4. Grają tak długo, aż dojdą do liczby 0. Nie mogą odjąć od
liczby za dużo - nie można wejść w liczby ujemne! To znaczy, że gdy w trakcie
rozgrywki natrafimy na liczbę 3, to nie możemy wykonać ruchu "minus 4". Przegrywa osoba,
która wykona ostatni ruch. Rownoważnie, wygrywa osoba, która jako pierwsza
zastanie liczbę 0.

Jaś pozwala Małgosi zaczynać każdą grę (ponieważ Jasiu jest prawdziwym dżentelmenem).
Prześledźmy przykładową rozgrywkę:

    21 - Małgosia odejmuje 3
    18 - Jaś odejmuje 2
    16 - Małgosia odejmuje 1
    15 - Jaś odejmuje 4
    11 - Małgosia odejmuje 2
    9  - Jaś odejmuje 3
    6  - Małgosia odejmuje 3
    3  - Jaś odejmuje 2
    1  - Małgosia musi odjąć 1, przegrywa :(

Podczas zajęć doszliśmy do wniosku, że Małgosia (jako osoba, która wykonuje drugi
ruch) nie ma szans na zwycięstwo, o ile Jaś nie popełni żadnego błędu.

Czy Małgosia może wygrać grę "w 24"? A grę "w 27"?

## Gra "w trzy stosy"
Drugą grą którą poznaliśmy to gra o roboczej nazwie "w trzy stosy". Grają Jaś i
Małgosia. Układają przed sobą trzy stosy monet: na pierwszym jest `a` monet,
na drugim `b` monet, na trzecim `c` monet. Na przykład mogą ułożyć stosy
po 2, 7 i 4 monety (`a = 2; b = 7; c = 4`). Na rysunku:

      *
      *
      *
      * *
      * *
    * * *
    * * *
    2 7 4

Ruch polega na wybraniu dowolnego ze stosów i zabraniu z niego dowolnej liczby
monet. Jaś i Małgosia wykonują ruchy na przemian. Oczywiście zaczyna Małgosia
i ściąga z środkowego stosu jedną monetę:
  
      *
      *
      * *
      * *
    * * *
    * * *
    2 6 4

Jaś odpowiada zabraniem całego stosu trzeciego:

      *
      *
      *
      *
    * *
    * *
    2 6

Małgosia zabiera cztery monety ze stosu drugiego:

    * *
    * *
    2 2

Jaś zabiera jedną monetę ze stosu pierwszego:

      *
    * *
    1 2

Jaś widzi już, że w tym momencie przegrał. Czy widzisz dlaczego?

Tym razem w lepszej sytuacji jest Małgosia - wykonując odpowiednie
ruchy (i dobierając początkową liczbę monet) może zawsze wygrać
i upokorzyć Jasia. Mówimy, że Małgosia ma *strategię wygrywającą*.
Dlaczego tak jest dowiemy się na następnych zajęciach.

## Ciekawostka

Po każdych zajęciach postaram umieścić się jedną ciekawostkę wraz
z pytaniem. Nie jest to żadne obowiązkowe zadanie domowe, tylko
"pożywienie" dla osób lubiących łamigłówki. O rozwiązanie można
mnie wypytać na następnych zajęciach. Oto ciekawostka:

> W przedziale pociągu jedzie 6 osób. Jeżeli każde dwie osoby znają
> się nawzajem lub nie znają w ogóle (tzn. nie ma sytuacji, że Jaś
> zna Małgosię a Małgosia nie zna Jasia), to zawsze będzie w takim
> przedziale trójka przyjaciół (każdy zna każdego) lub trójka
> nieznajomych (nikt nie zna nikogo).
> Czy wiesz czemu tak jest?
