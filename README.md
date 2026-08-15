# Maszyna S+7

Mechaniczne narzędzie do przekształcania tekstu polskiego metodą oulipijską **S+7**,
opracowaną przez Jeana Lescure'a na czwartym zebraniu grupy Oulipo, 13 lutego 1961 roku.

Każdy rzeczownik zostaje zastąpiony siódmym kolejnym rzeczownikiem ze słownika.
Ta wersja rozszerza regułę na **czasowniki i przymiotniki**, a podstawione słowo
odmienia tak, jak odmienione było słowo pierwotne.

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

**Nazwy własne pominięto** — słowniki języka polskiego ich nie notują, więc ich brak
czyni maszynę wierniejszą metodzie.

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
