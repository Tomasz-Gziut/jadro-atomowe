# Jądro atomowe — prezentacja maturalna

**36-slajdowa** prezentacja po polsku dla uczniów liceum przygotowujących się do matury rozszerzonej z fizyki. Kurs prowadzi od budowy atomu, nuklidów i doświadczeń historycznych przez oddziaływania, rozpady, aktywność i dawkę, aż po energię wiązania, rozszczepienie, fuzję, PET i inne zastosowania. Po przykładzie obliczeniowym następują wnioski, dodatek z pojęciami i wzorami oraz osobna bibliografia.

Zawiera autorskie diagramy, lokalne fotografie historyczne z atrybucjami, suwaki składu nuklidu i okresów półtrwania, krótkie cytowania na slajdach oraz spis treści i pasek postępu powiązane z ich liczbą. Model atomu renderowany przez Three.js pokazuje przestrzenną chmurę prawdopodobieństwa elektronów zamiast orbit; zaznacza też, że jądro jest powiększone i nie zachowuje skali. Nie zawiera quizu. Projekt używa pełnoekranowej, kinowej palety granatu, ciepłej bieli i turkusu oraz nie pobiera zdalnych fontów ani obrazów.

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
- Suwaki służą do zmiany składu nuklidu i upływu okresów półtrwania.

## Źródła merytoryczne

- OpenStax, *University Physics, Volume 3*: [10.1 Properties of Nuclei](https://openstax.org/books/university-physics-volume-3/pages/10-1-properties-of-nuclei), [10.2 Nuclear Binding Energy](https://openstax.org/books/university-physics-volume-3/pages/10-2-nuclear-binding-energy), [10.3 Radioactive Decay](https://openstax.org/books/university-physics-volume-3/pages/10-3-radioactive-decay), [10.4 Nuclear Reactions](https://openstax.org/books/university-physics-volume-3/pages/10-4-nuclear-reactions), [10.5 Fission](https://openstax.org/books/university-physics-volume-3/pages/10-5-fission), [10.6 Nuclear Fusion](https://openstax.org/books/university-physics-volume-3/pages/10-6-nuclear-fusion), [10.7 Medical Applications and Biological Effects](https://openstax.org/books/university-physics-volume-3/pages/10-7-medical-applications-and-biological-effects-of-nuclear-radiation).
- NIST/CODATA, [Fundamental Physical Constants](https://www.nist.gov/pml/fundamental-physical-constants).
- Nobel Prize biographical material: [Henri Becquerel](https://www.nobelprize.org/prizes/physics/1903/becquerel/biographical/), [Ernest Rutherford](https://www.nobelprize.org/prizes/chemistry/1908/rutherford/biographical/), [James Chadwick](https://www.nobelprize.org/prizes/physics/1935/chadwick/biographical/).

## Lokalne zdjęcia i atrybucje

- Henri Becquerel — portret Paula Nadara (ok. 1890–1908), domena publiczna: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Paul_Nadar_-_Henri_Becquerel.jpg).
- Ernest Rutherford — Smithsonian Institution Libraries / Wikimedia Commons, „No known copyright restrictions”: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Portrait_of_Ernest_Rutherford_(1871-1937),_Physicist_and_Chemist_(2551070939).jpg).
- Aparatura Geigera–Marsdena — współczesna rekonstrukcja CGI, nie oryginalne urządzenie ani fotografia z 1909 r.; Kurzon, [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/): [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Geiger-Marsden_apparatus_2_CGI_mock-up.jpg).
- Zjazd naukowców w Münster (1932) — fotografia grupowa, na której są m.in. James Chadwick i Ernest Rutherford; US Department of Energy, domena publiczna: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Bunsentagung_1932_Münster.jpg). To nie jest fotografia doświadczenia Chadwicka.

Pliki zdjęć znajdują się w `src/assets/history/` i są dołączone lokalnie; nie wymagają połączenia z siecią podczas prezentacji. Atrybucje są zachowane na slajdach historycznych i w ostatnim slajdzie bibliografii.
