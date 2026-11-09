# Jądro atomowe — prezentacja maturalna

**17-slajdowa** prezentacja po polsku o temacie 18.1 „Jądro atomowe”. Prowadzi od eksperymentu Geigera–Marsdena przez model jądra, izotopy oraz liczby Z i A do oddziaływań, mas atomowych i antymaterii. Każdy model oznacza, co przedstawia i gdzie zastosowano umowną skalę.

Każdy slajd ma osobny diagram dopasowany do omawianej idei: od składu atomu helu i porównania cząstek po aparaturę Rutherforda, tory rozpraszania oraz kwarki w protonie i neutronie. Prezentacja zawiera też interaktywny zapis nuklidu oraz model Three.js wodoru w stanie 1s, pokazujący rozkład prawdopodobieństwa elektronu. Kolory protonów, neutronów i elektronów są stałe w całym materiale; promieniowanie alfa i kwarki mają osobne oznaczenia. Schemat izotopów wodoru pokazuje osobno protony, neutrony i elektrony. Nie przedstawia elektronów jako planet na orbitach i odróżnia pomiar od animacji widoku. Szkolne określenie nukleonów jako „cząstek elementarnych” zestawiono z ich współczesnym opisem jako cząstek złożonych z kwarków. Treści fragmentu podręcznika streszczono własnymi słowami.

Szczegółowy skrypt prezentera z objaśnieniami pojęć, intencją wizualizacji, wskazówkami do prowadzenia każdego slajdu i typowymi nieporozumieniami znajduje się w pliku `skrypt-prezentera.txt` (około 15–18 minut).

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
- CERN, [The Standard Model](https://home.cern/science/physics/standard-model).
