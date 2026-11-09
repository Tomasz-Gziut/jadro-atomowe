# Jądro atomowe — prezentacja maturalna

**17-slajdowa** prezentacja informacyjna po polsku o temacie 18.1 „Jądro atomowe”. Obejmuje skład atomu i jądra, nukleony, izotopy, liczby Z i A, doświadczenie Rutherforda, masę atomową, oddziaływania jądrowe, cząstki elementarne oraz antymaterię. Zawiera przykłady objaśniające pojęcia.

Zawiera autorskie diagramy, rekonstrukcję aparatury Geigera–Marsdena z atrybucją, interaktywny zapis nuklidu oraz spis treści i pasek postępu powiązane z liczbą slajdów. Animowany model Three.js pozwala przełączyć się między chmurą prawdopodobieństwa elektronu wodoru (stan 1s) a uproszczonym modelem z umowną orbitą; wyjaśnia różnicę między pomiarem położenia i poglądową trajektorią. Treści fragmentu źródłowego streszczono własnymi słowami. Projekt używa pełnoekranowej, kinowej palety granatu, ciepłej bieli i turkusu oraz nie pobiera zdalnych fontów.

## Uruchomienie

Wymagany Node.js 20.19+ lub 22.12+.

```powershell
npm install
npm run dev
```

Uruchom polecenia z katalogu projektu. Otwórz `http://127.0.0.1:5173` w przeglądarce. Serwer developerski i podgląd wersji produkcyjnej nasłuchują wyłącznie na `127.0.0.1`. Komendą `npm run build` utworzysz wersję produkcyjną w `dist/`; `npm run preview` uruchamia jej lokalny podgląd.

## Sterowanie

- `←` / `→` lub spacja — poprzedni / następny slajd; `Home` / `End` — początek / koniec.
- Przyciski nawigacji, spis treści oraz gest przesunięcia w lewo/prawo na ekranie dotykowym.
- `F` lub przycisk pełnego ekranu — przełączenie prezentacji; `Esc` zamyka spis treści.
- Suwaki pozwalają zmieniać liczbę protonów i nukleonów w przykładzie zapisu izotopu.

## Źródła merytoryczne

- Podstawa zakresu: przekazany fragment podręcznika, §18.1 „Jądro atomowe”.
- OpenStax, *University Physics, Volume 3*: [10.1 Properties of Nuclei](https://openstax.org/books/university-physics-volume-3/pages/10-1-properties-of-nuclei).
- NIST/CODATA, [Fundamental Physical Constants](https://www.nist.gov/pml/fundamental-physical-constants).
- Nobel Prize biographical material: [Ernest Rutherford](https://www.nobelprize.org/prizes/chemistry/1908/rutherford/biographical/).

## Ilustracje i atrybucje

- Aparatura Geigera–Marsdena — współczesna rekonstrukcja CGI, nie oryginalne urządzenie ani fotografia z 1909 r.; Kurzon, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Geiger-Marsden_apparatus_2_CGI_mock-up.jpg).

Rekonstrukcja jest dołączona lokalnie i nie wymaga połączenia z siecią podczas prezentacji. Atrybucja znajduje się na slajdzie o doświadczeniu i w bibliografii.
