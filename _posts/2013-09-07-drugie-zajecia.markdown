---
layout: post
title: Zajęcia 2 - skoki w maszynie RAM
tags: lesson
---

Zajmowaliśmy się Maszyną RAM: dodawaniem listy liczb, skokami, pętlami i
warunkami.

## Nowe zadania
Na themisie pojawiły się nowe zadania (RAMCAT, Komparator, Ósma potęga i Suma liczb -
proponuję robić je w tej kolejności). Pierwsze z zadań robiliśmy na
zajęciach, reszta jest trochę trudniejsza. Żeby rozwiązać Ósmą potęgę
musicie poczytać o dodatkowych komendach maszyny RAM poniżej.

## Nowe komendy Maszyny RAM
* `mult n` - mnoży liczbę w komórce `0` z liczbą w komórce `n` i zapisuje
  wynik w komórce `0`.
* `sub n` - analogicznie jak powyżej, tylko że liczby są odejmowane.
* `div n` - analogicznie jak powyżej, tylko że liczby są dzielone.
* `jump label` - zawsze skacze do linii oznaczonej etykietą `label`.
* `jzero label` - skacze do linii oznaczonej etykietą `label` tylko, gdy
  liczba w komórce o nr `0` jest zerem.
* `jgtz label` - (ang. *jump if greater than zero*) - jak wyżej, ale skacze,
  gdy zawartość komórki `0` jest dodatnia.
* `halt` - zatrzymuje wykonywanie programu.

I kilka dodatkowych, nie omawianych na zajęciach:

* `store n` - skopiuj zawatrość komórki o numerze `0` do komórki o numerze
  `n`.
* `load n` - skopiuj zawartość komórki o numerze `n` do komórki o numerze
  `0`.

Jeżeli do komend `load` podamy jako argument liczbę poprzedzoną znakiem `=`
to *podana liczba zostanie wczytana do komórki o numerze 0 (akumulatora)*.
Dla przykładu:

    load =10
    read 1
    add 1
    write 0

Powyższy program do wczytanej liczby doda 10, po czym wypisze wynik na ekran.
Tak samo możemy zrobić z instrukcjami `add`, `sub` itp. Poniższy program
również doda do wczytanej liczby 10 i wypisze wynik:

    read 0
    add =10
    write 0

*Podpowiedź*: do zrobienia zadania Suma liczb najprawdopodobniej będą Wam potrzebne
komendy `load` i `store`.

## Porównywanie liczb

Spróbujmy napisać program, który wczyta dwie liczby i wypisze 1, jeżeli pierwsza
jest mniejsza od drugiej, a 0 w przeciwnym przypadku. Podczas konkursu, czy choćby
na Themisie zadanie będzie sformułowane podobnie do poniższego:

    Jasiu jest kiepski z matematyki i nie wie która z dwóch liczb zapisanych w jego
    zeszycie jest większa. Pomóż mu!
    
    Dane:
      a, b - dwie liczby naturalne

    Wynik:
      1, jeżeli a < b
      0, w przeciwnym przypadku

W Maszynie RAM nie mamy instrukcji porównującej liczby, ale możemy skorzystać z tego,
że `a < b` wtedy, gdy `0 < b - a` (wystarczy obustronnie odjąć `a` od nierówności).
Czyli możemy odjąć od siebie liczby podane na wejściu, po czym sprawdzić czy wynik
odejmowania jest większy od zera komendą `jgtz`. Kompletny program poniżej:

           read 1
           read 0
           sub 1
           jgtz dalej
           write =0
           halt
    dalej: write =1

Komentarz do programu: liczbę `a` wczytujemy do komórki `1`, liczbę `b` do komórki
`0`. Po komendzie `sub 1` w akumulatorze (komórce o nr `0`) mamy wynik działania
`b - a`. Jeżeli jest on większy od zera (czyli jeżeli `a < b`), to skaczemy do
etykiety `dalej`, po czym program wypisze `1`.

Jeżeli wynik jest mniejszy bądź równy zeru, to wykona się kolejna instrucja: na ekran
(na taśmę wyjściową) zostanie wypisane `0`, po czym program zakończy pracę na instrukcji
`halt`.

Zauważmy, że instrukcja `halt` jest konieczna: bez niej, w przypadku gdy `a >= b` program
wypisałby `0` a później `1`.

## Schematy blokowe
Na zajęciach pokazałem na tablicy kilka przykładów schematów blokowych, które
następnie przepisywaliśmy do Maszyny RAM. Na następnych zajęciach wrócimy
do tematu, a dla zainteresowanych dostępne są [materiały w internecie](http://kasia315.republika.pl/kurs/lekcja2.htm).

## Ciekawostka
Popatrzmy na następujące zadanie:

> Weźmy liczbę `n` większą od 1. Jeżeli jest parzysta, podzielmy ją przez 2.
> Jeżeli jest nieparzysta, to pomnóżmy przez 3 i dodajmy 1. Dla przykładu:

    6 -> 3
    3 -> 10 (= 3 * 3 + 1)

> Proces powtarzamy tak długo, aż osiągniemy 1. Na przykład:

    3 -> 10 -> 5 -> 16 -> 8 -> 4 -> 2 -> 1

Pytanie: czy zawsze otrzymamy na końcu jeden, czy możemy się 'zapętlić'?
Uwaga: Odpowiedź nie jest prosta :)
