# Maszyna S+7

Mechaniczne narzędzie do przekształcania tekstu polskiego metodą oulipijską **S+7**,
opracowaną przez Jeana Lescure'a na czwartym zebraniu grupy Oulipo, 13 lutego 1961 roku.

Każdy rzeczownik zostaje zastąpiony siódmym kolejnym rzeczownikiem ze słownika.
Ta wersja rozszerza regułę na **czasowniki, przymiotniki i przysłówki**, a podstawione
słowo odmienia tak, jak odmienione było słowo pierwotne.

François Le Lionnais, współzałożyciel Oulipo, uogólnił metodę Lescure'a do wzoru
**m±n**: dowolna część mowy, dowolna liczba całkowita, w przód albo wstecz.
Maszyna idzie za tym uogólnieniem — krok ustawia się **osobno dla każdej z trzech
części mowy**, może być ujemny, a zero znaczy „nie ruszaj".

## Jak to działa

1. **Analiza** — każde słowo tekstu zostaje rozpoznane: jaką jest częścią mowy,
   od jakiego lematu (formy hasłowej) pochodzi i w jakiej stoi formie gramatycznej.
2. **Liczenie** — maszyna odnajduje lemat na alfabetycznej liście haseł danej części
   mowy i przechodzi N pozycji dalej. Liczy w **polskim porządku alfabetycznym**
   (a ą b c ć d e ę …), a nie w kolejności kodów Unicode.
3. **Odmiana** — nowy lemat zostaje odmieniony tak, by pasował do formy oryginału:
   ten sam przypadek, liczba, osoba, rodzaj. Gdy hasło nie ma dokładnie takiej formy,
   maszyna wybiera najbliższą i wyraźnie to oznacza.
4. **Rejestr** — dla każdego słowa widać całą drogę przez słownik: wszystkie kroki
   pośrednie, które maszyna pokonała.

## Rozstrzyganie wieloznaczności

Wiele polskich form pasuje do kilku haseł naraz. „Była" to zarówno forma czasownika
*być*, jak i rzadki rzeczownik; „dzień" pasuje do hasła *dzień*, ale też do rzadkiego
*dzienia*. Maszyna wybiera odczyt najczęstszy, opierając się na liście frekwencyjnej,
i premiuje odczyt, w którym słowo jest formą hasłową.

Słowa funkcyjne — zaimki, przyimki, spójniki, partykuły — zostają nietknięte, chyba
że mają wyraźny i częsty odczyt treściowy. Dzięki temu „tak", „mi" czy „się" przechodzą
przez maszynę bez zmian.

**Nazwy własne** są pominięte na listach haseł — słowniki języka polskiego ich nie
notują, więc ich brak czyni maszynę wierniejszą metodzie. Jednocześnie są chronione
przed zamianą: gdyby ich nie sprawdzać osobno, maszyna widziałaby „Polska" wyłącznie
jako formę żeńską przymiotnika *polski* i podmieniałaby nazwę kraju. Rozstrzyga
wielka litera — „Polska kultura" zostaje nietknięta, „polska kuchnia" nie.

**Zaimki przymiotne** (ten, który, każdy, mój, żaden, sam…) zostają nietknięte.
Morfologik klasyfikuje je jako przymiotniki, bo tak się odmieniają, ale to klasa
zamknięta słów funkcyjnych i metoda nie powinna ich ruszać. Świadomie **nie**
chronimy słów „inny" i „pewien", które bywają zwykłymi przymiotnikami.

## Przysłówki

Przysłówki są nieodmienne — jedyne, co robią, to stopniowanie: *szybko, szybciej,
najszybciej*. Maszyna zachowuje stopień, także przy formach nieregularnych
(*dobrze → lepiej → najlepiej*).

Lista obejmuje **wyłącznie przysłówki stopniowalne**, czyli 1398 haseł zamiast
25 907. Powód jest praktyczny: prawie połowa pełnej listy to formy utworzone od nazw
miejscowych (*mielecko, mieroszowsko, dziwnowsko*), których nie da się odfiltrować po
wielkiej literze, bo pisze się je małą. Stopniowanie okazało się skutecznym sitem —
nazwy miejscowe się nie stopniują.

Cena tego wyboru: przysłówki niestopniowalne, jak *dzisiaj* czy *wczoraj*, zostają
nietknięte.

## Odsłowniki

Odsłowniki (*gaszenie*, *dolewanie*, *narzekanie*) to rzeczowniki utworzone od
czasowników. Morfologik lematyzuje je do bezokolicznika, więc traktuje jak formy
czasownika — a odmieniają się i zachowują jak rzeczowniki nijakie.

Maszyna wprowadza je jako **hasła rzeczownikowe**: lematem jest ich własny mianownik,
a znaczniki przepisane są z `ger:…` na `subst:…`. Bez tego 27 377 odsłowników nie
istniałoby dla maszyny w ogóle — tylko 2136 z nich ma w Morfologiku osobne hasło
rzeczownikowe.

## Nazwy własne — przełącznik

Domyślnie nazwy własne są wyłączone z gry w obie strony. Można to odwrócić jednym
polem wyboru: wtedy lista rzeczowników rośnie ze 171 388 do 204 772 haseł, a nazwy
stoją na niej na równi z wyrazami pospolitymi. *Warszawa* przechodzi w *Warszawiankę*,
*Chrystusa* w *Chryzarobinę*, a zwykły rzeczownik może wylądować na nazwie miejscowej.

Pełna lista doczytuje się dopiero przy pierwszym włączeniu, żeby nie obciążać
startu. Uwaga: przy włączonym przełączniku **wszystkie skoki wypadają gdzie indziej**,
bo zmienia się długość listy — te same ustawienia dadzą inne wyniki niż przy wyłączonym.

## Zgoda przymiotnika z rzeczownikiem

Rodzaj jest w polszczyźnie wpisany w hasło, więc skok potrafi przenieść rzeczownik
z męskiego na żeński albo z pojedynczej na mnogą. Stojące obok przymiotniki i zaimki
zostają wtedy przy dawnej formie i wychodzi „dobrego eoceńskość".

Maszyna robi z tego powodu **drugi przebieg**: po zamianie wraca do określeń
sąsiadujących z rzeczownikiem i odmienia je na nowo, według rodzaju i liczby nowego
hasła, zachowując przypadek. Szuka w obie strony, bo polski przymiotnik bywa i przed
rzeczownikiem („młody człowiek"), i po nim („znak osobowy"), oraz przechodzi przez
spójniki („znak osobowy i żywy").

Uzgadnianie zatrzymuje się na interpunkcji i nie przekracza granicy frazy: w „dobrego
dzionka i smacznej kawusi" przymiotnik *smacznej* należy do *kawusi*, nie do *dzionka*.
Wyrazy uzgodnione, ale niezamienione, są w wyniku podkreślone cienką linią.

## Przypadek gramatyczny

Jedna polska forma pasuje często do wielu przypadków naraz. „Normalności" to
jednocześnie dopełniacz, celownik, miejscownik i wołacz liczby pojedynczej oraz
mianownik, biernik, dopełniacz i wołacz liczby mnogiej — osiem odczytów.

Maszyna rozstrzyga to **przyimkiem stojącym przed wyrazem**. „Do" wymaga
dopełniacza, „przy" miejscownika, „przez" biernika. Przyimki wieloznaczne
(w, na, o, po, za, nad, pod, przed, z) nie rozstrzygają, ale zawężają pole wyboru,
co zwykle wystarcza. Przyimek przechodzi przez przymiotniki do rzeczownika, więc
„do wielkiej normalności" działa tak samo jak „do normalności".

Gdy po zawężeniu zostaje więcej niż jeden odczyt, maszyna wybiera najbardziej
prawdopodobny (liczba pojedyncza przed mnogą), ale **oznacza go znakiem zapytania**
w rejestrze, zamiast udawać pewność. Bez analizy składniowej nie da się rozstrzygnąć
wszystkiego i lepiej to pokazać, niż ukryć.

## Pliki

```
index.html        cała aplikacja
dane/             słownik (ok. 4,5 MB spakowane)
```

Aplikacja działa w całości w przeglądarce. Nic nie jest wysyłane na serwer.
Wymaga przeglądarki obsługującej `DecompressionStream`: Firefox 113+, Chrome 80+,
Safari 16.4+.

## Źródła danych

- **PoliMorfologik 2.1** — słownik morfosyntaktyczny języka polskiego,
  Marcin Miłkowski i in., IPI PAN / sjp.pl, licencja BSD.
  <https://github.com/morfologik/polimorfologik>
- **FrequencyWords** — listy frekwencyjne z korpusu OpenSubtitles 2018.
  <https://github.com/hermitdave/FrequencyWords>

## Dalsza lektura

- Jean Lescure, *The N+7 Method (An Individual Case of the W±n Method)* —
  <https://www.mcsweeneys.net/articles/jean-lescure-from-the-n-7-method-an-individual-case-of-the-w-n-method>
- Biuro Literackie, *Przypadek z clinamen w OuLiPo* —
  <https://www.biuroliterackie.pl/biblioteka/recenzje/przypadek-z-clinamen-w-oulipo-z-johnem-cageem-w-tle/>
- Jacek Olczyk, *Literatura polska w świetle przymusów Oulipo*, Wydawnictwo UJ.
