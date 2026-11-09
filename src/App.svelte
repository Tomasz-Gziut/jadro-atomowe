<script>
  import AtomModel from './AtomModel.svelte';
  import becquerelPortrait from './assets/history/becquerel.jpg';
  import geigerMarsdenReconstruction from './assets/history/geiger-marsden-reconstruction.jpg';
  import munsterGroup from './assets/history/munster-1932.jpg';
  import rutherfordPortrait from './assets/history/rutherford.jpg';

  const slides = [
    { kicker: 'Pytanie przewodnie', title: 'Jak małe jądro skupia niemal całą masę atomu?', lead: 'Podążymy od budowy atomu, przez doświadczenia i rozpady, aż do energii gwiazd oraz zastosowań medycznych.', visual: 'hero', points: [
      { title: 'Zacznijmy od skali', text: 'Jądro jest około sto tysięcy razy mniejsze od atomu w promieniu — a jednak skupia prawie całą jego masę.' },
      { title: 'Pytanie kursu', text: 'Co spaja dodatnio naładowane protony, skąd znamy budowę jądra i jak tę wiedzę wykorzystujemy?' }
    ]},
    { kicker: '01 · Atom i jądro', title: 'Protony i neutrony tworzą masywne centrum atomu', lead: 'Jądro tworzą protony i neutrony; znacznie lżejsze elektrony zajmują otaczający je obszar. W atomie obojętnym ładunki się równoważą.', visual: 'atom', points: [
      { title: 'Składniki', text: 'Proton ma ładunek dodatni, neutron jest obojętny, a elektron ma ładunek ujemny o tej samej wartości co proton.' },
      { title: 'Bilans atomu', text: 'W atomie obojętnym liczba elektronów jest równa liczbie protonów. Niemal cała masa atomu znajduje się w jądrze.' },
      { title: 'Skąd wiemy?', text: 'Rozpraszanie cząstek i pomiary widm ujawniają małe, dodatnie centrum oraz elektrony związane z atomem.' }
    ]},
    { kicker: '02 · Skala', title: 'Promień jądra jest około 100 000 razy mniejszy', lead: 'Typowa skala atomu to 10⁻¹⁰ m, a promienia jądra około 10⁻¹⁵ m. To porównanie promieni, nie średnic.', visual: 'scale', points: [
      { title: 'Różnica skali', text: 'Promień jądra jest około 100 000 razy mniejszy. „Pusta przestrzeń” oznacza tu, że jądro zajmuje bardzo małą część objętości atomu.' },
      { title: 'Jak rośnie jądro?', text: 'W przybliżeniu R ≈ r₀A^(1/3), gdzie r₀ ≈ 1,2 fm, a 1 fm = 10⁻¹⁵ m. Większe jądro rośnie wolniej niż liczba jego nukleonów.' },
      { title: 'Ważne zastrzeżenie', text: 'Elektrony nie krążą po sztywnych orbitach jak planety; rysunek przedstawia wyłącznie porównanie skali.' }
    ]},
    { kicker: '03 · Nukleony', title: 'Protony i neutrony wspólnie budują jądra', lead: 'Nukleon to wspólna nazwa protonów i neutronów, czyli składników jąder atomowych.', visual: 'nucleons', points: [
      { title: 'Ładunki', text: 'Proton p⁺ ma ładunek +e, neutron n⁰ ma ładunek 0. Elektron e⁻ ma ładunek −e.' },
      { title: 'Masy', text: 'Proton ma masę około 1,0073 u, neutron 1,0087 u, a elektron 0,00055 u. Jednostka u to atomowa jednostka masy.' },
      { title: 'Głębsza budowa', text: 'Protony i neutrony są hadronami zbudowanymi z kwarków. W zadaniach tego działu opisujemy jądro modelem protonów i neutronów.' }
    ]},
    { kicker: '04 · Zapis nuklidu', title: 'Z i A jednoznacznie określają skład nuklidu', lead: 'Nuklid to atom określony przez skład jądra. Zapis ᴬ_ZX podaje jego liczbę masową A, liczbę protonów Z i symbol pierwiastka X.', visual: 'notation', points: [
      { title: 'Dwa liczniki', text: 'A = Z + N, więc liczba neutronów N = A − Z. A jest liczbą nukleonów, nie dokładną masą w u.' },
      { title: 'Pierwiastek', text: 'Liczba protonów Z określa pierwiastek. Obojętny atom ma Z elektronów; jon różni się liczbą elektronów, a nie składem jądra.' },
      { title: 'Sprawdź na suwaku', text: 'Zmień A i Z, a odczytasz symbol pierwiastka oraz liczbę neutronów. Dla fizycznego nuklidu musi zachodzić A ≥ Z.' }
    ]},
    { kicker: '05 · Izotopy', title: 'Różna liczba neutronów tworzy izotopy pierwiastka', lead: 'Izotopy to nuklidy tego samego pierwiastka: mają tę samą liczbę protonów Z, lecz różną liczbę neutronów N.', visual: 'isotopes', points: [
      { title: 'Wodór', text: 'Wodór-1 ma 1 proton i 0 neutronów; deuter (²H) ma 1 proton i 1 neutron; tryt (³H) ma 1 proton i 2 neutrony.' },
      { title: 'Węgiel', text: 'Węgiel-12 i węgiel-14 mają po 6 protonów, ale odpowiednio 6 i 8 neutronów. Węgiel-14 jest promieniotwórczy.' },
      { title: 'Chemia a jądro', text: 'O własnościach chemicznych decyduje głównie układ elektronów, określany przez Z. Izotopy zwykle reagują podobnie, choć ich masy i stabilność jądrowa są różne.' }
    ]},
    { kicker: '06 · Rodziny nuklidów', title: 'Nuklidy grupuje wspólne Z, A albo N', lead: 'Nazwy opisują, którą wielkość dwa nuklidy mają wspólną. Zawsze najpierw oblicz N = A − Z.', visual: 'families', points: [
      { title: 'Izotopy', text: 'To samo Z, różne A i N; przykładem są ¹²₆C i ¹⁴₆C.' },
      { title: 'Izobary i izotony', text: 'Izobary mają to samo A, np. ¹⁴₆C i ¹⁴₇N. Izotony mają to samo N, np. ¹⁴₆C i ¹⁵₇N (N = 8).' },
      { title: 'Średnia masowa', text: 'Masa atomowa pierwiastka jest średnią ważoną: Σ(ułamek izotopu × jego masę). Dla naturalnego węgla to około 12,011 u — nie A jednego nuklidu.' }
    ]},
    { kicker: '07 · Doświadczenie', title: 'Większość cząstek α przeszła przez złotą folię', lead: 'Geiger i Marsden badali rozpraszanie dodatnich cząstek α na cienkiej folii złota (1909); Rutherford później zinterpretował wynik.', visual: 'scattering', points: [
      { title: 'Obserwacja', text: 'Większość cząstek przechodziła prawie bez odchylenia. Nieliczne zmieniały kierunek o duży kąt, a bardzo mała część zawracała.' },
      { title: 'Interpretacja', text: 'Skoro zwykle nie trafiały na przeszkodę, atom jest w większości przestrzenią. Rzadkie silne odchylenia wskazują na małe, dodatnie i masywne centrum.' },
      { title: 'Wniosek', text: 'Atom ma jądro skupiające niemal całą masę. Doświadczenie wykonywali Hans Geiger i Ernest Marsden, pod kierunkiem Rutherforda.' }
    ]},
    { kicker: '08 · Historia modelu', title: 'Nowe pomiary wymusiły zmianę modelu atomu', lead: 'Model atomu nie powstał w jednym momencie: kolejne obserwacje ujawniały zjawiska, których wcześniejsze wyobrażenia nie tłumaczyły.', visual: 'history', points: [
      { title: '1896 · Becquerel', text: 'Związki uranu zaczerniały osłoniętą kliszę. Promieniowanie pochodziło z materiału, nie z uprzedniego naświetlenia.' },
      { title: '1909–1911 · Geiger, Marsden, Rutherford', text: 'Rzadkie duże odchylenia cząstek α doprowadziły do jądrowego modelu atomu.' },
      { title: '1932 · Chadwick', text: 'Doświadczenia z berylem i parafiną wskazały neutralną cząstkę o masie zbliżonej do protonu: neutron.' }
    ]},
    { kicker: '09 · Odkrycie neutronu', title: 'Odrzut protonów ujawnił neutralny neutron', lead: 'James Chadwick połączył dwa pomiary: promieniowanie z berylu wybijało z parafiny protony, choć samo nie było strumieniem naładowanych cząstek.', visual: 'chadwick', points: [
      { title: 'Obserwacja', text: 'Promieniowanie z berylu uderzało w parafinę, z której wylatywały szybkie protony. Ich energie dało się zmierzyć.' },
      { title: 'Rozumowanie', text: 'Cząstka neutralna może przeniknąć do parafiny bez odpychania Coulombowskiego. Z przekazanego pędu wynikała masa zbliżona do protonu.' },
      { title: 'Wniosek', text: 'Najlepszym wyjaśnieniem był neutron. Pomiar odrzutu i bilans energii/pędu rozróżniły go od promieniowania γ.' }
    ]},
    { kicker: '10 · Oddziaływania', title: 'Krótkie oddziaływanie silne wiąże nukleony', lead: 'Protony odpychają się elektrycznie, ale blisko siebie nukleony przyciąga resztkowe oddziaływanie silne.', visual: 'forces', points: [
      { title: 'Konkurujące efekty', text: 'Oddziaływanie Coulombowskie między protonami działa na daleki zasięg i je odpycha. Oddziaływanie silne między nukleonami jest bardzo mocne, ale krótkiego zasięgu.' },
      { title: 'Dlaczego jądro nie rozpada się od razu?', text: 'Gdy nukleony są bardzo blisko, przyciąganie silne może przeważyć odpychanie protonów. Dla zbyt dużych jąder rosnąca repulsja utrudnia stabilność.' },
      { title: 'Rola słabego', text: 'Oddziaływanie słabe umożliwia przemiany typu β, np. neutronu w proton. Nie jest ono „klejem” utrzymującym jądro.' }
    ]},
    { kicker: '11 · Stabilność', title: 'Stabilne jądra tworzą wygięte pasmo N–Z', lead: 'Wykres neutronów N względem protonów Z pokazuje, które proporcje sprzyjają stabilności.', visual: 'stability', points: [
      { title: 'Co widać?', text: 'Lekkie stabilne jądra mają często N zbliżone do Z. W cięższych jądrach stabilnych neutronów zwykle jest więcej niż protonów.' },
      { title: 'Dlaczego krzywa się wygina?', text: 'Dodatkowe neutrony wzmacniają wiązanie silne, nie dodając ładunku elektrycznego. W ciężkich jądrach trzeba nimi równoważyć rosnące odpychanie protonów.' },
      { title: 'Poza pasmem', text: 'Nadmiar neutronów lub protonów może prowadzić do rozpadu β. Wykres jest mapą znanych jąder, nie prostą granicą jednej reguły.' }
    ]},
    { kicker: '12 · Promieniotwórczość', title: 'Niestabilne jądra rozpadają się spontanicznie i losowo', lead: 'Promieniotwórczość to spontaniczna przemiana niestabilnego jądra w inne jądro, połączona z emisją cząstki lub promieniowania.', visual: 'random', points: [
      { title: 'Losowość pojedyncza', text: 'Nie da się przewidzieć, kiedy rozpadnie się konkretne jądro. Każde ma stałe prawdopodobieństwo rozpadu w danym czasie.' },
      { title: 'Przewidywalność próbki', text: 'W ogromnym zbiorze jąder losowe zdarzenia tworzą regularne prawo statystyczne.' },
      { title: 'Czego zwykle nie zmieniamy?', text: 'Temperatura, ciśnienie i reakcje chemiczne nie zmieniają zauważalnie okresu półtrwania jądra. Zmienia go sam skład/stan jądra.' }
    ]},
    { kicker: '13 · Bilans jądrowy', title: 'Zachowanie A i Z wyznacza produkty rozpadu', lead: 'Po obu stronach równania zachowują się suma liczb masowych A oraz suma ładunków, zapisywana tu przez Z.', visual: 'balance', points: [
      { title: 'Przykład', text: '²³⁸₉₂U → ²³⁴₉₀Th + ⁴₂He.' },
      { title: 'Krok 1 · A', text: 'Po lewej A = 238. Po prawej 234 + 4 = 238.' },
      { title: 'Krok 2 · ładunek', text: 'Po lewej Z = 92. Po prawej 90 + 2 = 92. To bilans reakcji jądrowej, nie równanie reakcji chemicznej.' }
    ]},
    { kicker: '14 · Rozpad α', title: 'Rozpad alfa zmniejsza A o 4, a Z o 2', lead: 'Cząstka α jest jądrem helu-4: 2 protony i 2 neutrony związane razem.', visual: 'alpha', points: [
      { title: 'Zmiana jądra', text: 'Emisja ⁴₂He zmniejsza liczbę masową A o 4, a liczbę protonów Z o 2. Przykład: ²³⁸U → ²³⁴Th + ⁴He.' },
      { title: 'Jak ją rozpoznać?', text: 'Cząstka α ma ładunek +2e, silnie jonizuje materię i stosunkowo łatwo ją zatrzymać. Zasięg zależy od energii i ośrodka.' },
      { title: 'Zastosowanie wiedzy', text: 'Bilans pozwala ustalić produkt rozpadu; osłonę dobiera się do źródła i warunków, a nie do uniwersalnej reguły o kartce papieru.' }
    ]},
    { kicker: '15 · Rozpad β⁻', title: 'W rozpadzie β⁻ neutron zmienia się w proton', lead: 'W przemianie β⁻ neutron w jądrze zmienia się w proton, elektron i antyneutrino elektronowe.', visual: 'beta-minus', points: [
      { title: 'Zapis cząstek', text: 'n → p + e⁻ + ν̄ₑ. Elektron nie był wcześniej „schowany” w jądrze — powstaje w samej przemianie.' },
      { title: 'Zmiana jądra', text: 'Liczba nukleonów A pozostaje taka sama, a Z rośnie o 1, bo jeden neutron zmienił się w proton.' },
      { title: 'Po co antyneutrino?', text: 'Energia rozpadu dzieli się między elektron, antyneutrino i odrzut jądra. Neutrino pomaga zachować energię, pęd i liczbę leptonową.' }
    ]},
    { kicker: '16 · β⁺ i wychwyt elektronu', title: 'Proton może zmienić się w neutron', lead: 'Dwie przemiany obniżają Z o 1, a nie zmieniają A: emisja pozytonu β⁺ oraz wychwyt elektronu z powłoki.', visual: 'beta-plus', points: [
      { title: 'Emisja β⁺', text: 'p → n + e⁺ + νₑ. Pozyton e⁺ jest antycząstką elektronu: ma taką samą masę, lecz ładunek dodatni.' },
      { title: 'Wychwyt elektronu', text: 'p + e⁻ → n + νₑ. Jądro pochłania elektron atomowy; w zapisie nuklidów A pozostaje stałe, Z maleje o 1.' },
      { title: 'Warunek energii', text: 'Emisja pozytonu wymaga dostatecznej różnicy energii między atomami. Nie myl e⁺ z elektronem e⁻.' }
    ]},
    { kicker: '17 · Promieniowanie γ', title: 'Foton gamma obniża energię bez zmiany A i Z', lead: 'Wzbudzone jądro może przejść na niższy poziom energii i wyemitować foton γ.', visual: 'gamma', points: [
      { title: 'Co się zmienia?', text: 'Liczby A i Z pozostają bez zmian. Zmienia się stan energetyczny jądra: X* → X + γ.' },
      { title: 'Kiedy występuje?', text: 'Promieniowanie γ często towarzyszy innemu rozpadowi, gdy powstałe jądro-córka pozostaje wzbudzone.' },
      { title: 'Energia fotonu', text: 'Różnica poziomów ΔE = hν, gdzie h to stała Plancka, a ν — częstotliwość fotonu w Hz. Foton nie ma ładunku, więc nie odchyla się w polu elektrycznym.' }
    ]},
    { kicker: '18 · Rozpoznawanie promieniowania', title: 'Ładunek i przenikanie rozróżniają α, β i γ', lead: 'Pole elektryczne odchyla cząstki naładowane; neutralne fotony γ nie. Zasięg w materii zależy od energii i materiału.', visual: 'radiation', points: [
      { title: 'Alfa', text: 'Ładunek +2e, duże odchylenie w polu, silna jonizacja i zwykle mała przenikliwość.' },
      { title: 'Beta', text: 'Elektron β⁻ ma ładunek −e, pozyton β⁺ +e; oba odchylają się mocno, lecz w przeciwne strony.' },
      { title: 'Gamma', text: 'Foton jest neutralny i zwykle bardziej przenikliwy. Papier, metal czy gruba osłona nie są uniwersalną gwarancją bezpieczeństwa — liczą się źródło, energia i dawka.' }
    ]},
    { kicker: '19 · Okres półtrwania', title: 'Po jednym okresie półtrwania zostaje średnio połowa jąder', lead: 'Okres półtrwania T₁/₂ to czas, po którym w dużej próbce pozostaje średnio połowa jąder macierzystych.', visual: 'halflife', points: [
      { title: 'Sekwencja', text: 'Po 1 T₁/₂ zostaje 1/2; po 2 — 1/4; po 3 — 1/8. Próbka nie znika nagle po kilku okresach.' },
      { title: 'To nie zegar jądra', text: 'Nie wiadomo, kiedy rozpadnie się pojedyncze jądro. T₁/₂ opisuje statystykę zespołu.' },
      { title: 'Eksperyment', text: 'Suwak zmienia liczbę upłyniętych okresów; wykres pokazuje malejący odsetek jąder macierzystych.' }
    ]},
    { kicker: '20 · Prawo rozpadu', title: 'Prawo rozpadu przewiduje statystyczny ubytek jąder', lead: 'Prawo rozpadu opisuje liczbę N jąder macierzystych w chwili t. N₀ to ich liczba początkowa.', visual: 'carbon', points: [
      { title: 'Wzory', text: 'N(t) = N₀(1/2)^(t/T₁/₂) = N₀e^(−λt), gdzie λ = ln 2/T₁/₂. λ ma jednostkę odwrotności czasu.' },
      { title: 'Przykład C-14', text: 'T₁/₂ ≈ 5730 lat. Jeśli pozostała 1/4 początkowej ilości, minęły 2 okresy: około 11 460 lat w modelu uproszczonym.' },
      { title: 'Datowanie w praktyce', text: 'Rzeczywiste datowanie uwzględnia kalibrację, początkową zawartość izotopu oraz zanieczyszczenia; sam rachunek nie wystarcza.' }
    ]},
    { kicker: '21 · Aktywność', title: 'Aktywność mówi, ile rozpadów zachodzi na sekundę', lead: 'Aktywność A jest szybkością rozpadów: A = λN. Jej jednostką jest bekerel (Bq).', visual: 'activity', points: [
      { title: 'Jednostka', text: '1 Bq = 1 rozpad na sekundę. Więcej jąder N lub większa stała rozpadu λ oznacza większą aktywność.' },
      { title: 'Dlaczego maleje?', text: 'Wraz z rozpadem zmniejsza się liczba jąder macierzystych N, więc maleje też aktywność tej próbki.' },
      { title: 'Czego Bq nie mówi?', text: 'Bq nie jest samodzielną miarą dawki ani ryzyka. Znaczenie mają m.in. rodzaj promieniowania, energia, osłona i droga narażenia.' }
    ]},
    { kicker: '22 · Dawka i ochrona', title: 'Aktywność źródła to nie dawka pochłonięta', lead: 'Promieniowanie jonizujące może wyrywać elektrony z atomów i uszkadzać tkanki. Do opisu używamy różnych wielkości.', visual: 'dose', points: [
      { title: 'Bq · aktywność', text: 'Liczba rozpadów na sekundę w źródle. Nie opisuje bezpośrednio, ile energii pochłonęło ciało.' },
      { title: 'Gy i Sv · dawki', text: 'Dawka pochłonięta w Gy to energia na masę (1 Gy = 1 J/kg). Dawka równoważnikowa w Sv uwzględnia rodzaj promieniowania.' },
      { title: 'Ocena narażenia', text: 'Znaczenie mają rodzaj i energia promieniowania, dawka, czas oraz droga narażenia. Ogranicz czas, zwiększ odległość i używaj właściwej osłony pod nadzorem.' }
    ]},
    { kicker: '23 · Defekt masy', title: 'Związane jądro ma mniejszą masę niż swobodne nukleony', lead: 'Defekt masy Δm to różnica między sumą mas swobodnych nukleonów a masą związanego jądra.', visual: 'mass', points: [
      { title: 'Definicja', text: 'Δm = Z·mₚ + N·mₙ − m_jądra, gdzie mₚ i mₙ to masy protonu i neutronu, a m_jądra — masa związanego jądra. Dla stabilnego jądra Δm jest dodatni.' },
      { title: 'Uwaga na elektrony', text: 'Porównuj jądra z jądrami. Jeśli korzystasz z mas atomowych, uwzględnij elektrony — można użyć mas atomów wodoru zamiast protonów, gdy elektrony bilansują się po obu stronach.' },
      { title: 'Znaczenie', text: 'Różnica mas odpowiada energii wiązania, związanej z energią oddaną podczas tworzenia jądra.' }
    ]},
    { kicker: '24 · Energia wiązania', title: 'Defekt masy odpowiada energii wiązania', lead: 'Energia wiązania Eᵦ to energia potrzebna do rozdzielenia jądra na swobodne nukleony — tyle samo energii jądro oddaje przy związaniu.', visual: 'helium', points: [
      { title: 'Zależność', text: 'Eᵦ = Δmc², gdzie c to prędkość światła w próżni. Dla Δm wyrażonej w u użyj 1 u·c² ≈ 931,5 MeV.' },
      { title: 'Hel-4 · masa', text: 'Użyj mas atomowych: 2m(¹H) + 2mₙ − m(⁴He) = 2·1,007825 + 2·1,008665 − 4,002603 ≈ 0,03038 u.' },
      { title: 'Hel-4 · energia', text: 'Eᵦ ≈ 0,03038·931,5 ≈ 28,3 MeV. Masy atomowe wodoru uwzględniają elektrony, które bilansują elektrony helu.' }
    ]},
    { kicker: '25 · Porównanie jąder', title: 'Energia wiązania na nukleon rośnie ku Fe i Ni', lead: 'Eᵦ/A to średnia energia wiązania przypadająca na jeden nukleon. Większa wartość zwykle oznacza silniejsze związanie na nukleon.', visual: 'curve', points: [
      { title: 'Kształt krzywej', text: 'Dla lekkich jąder Eᵦ/A szybko rośnie, osiąga maksimum w okolicy żelaza i niklu, a dla ciężkich jąder nieco maleje.' },
      { title: 'Nie jedna wartość', text: 'Wykres jest jakościowy: izotopy w pobliżu Fe/Ni nie mają identycznej energii wiązania.' },
      { title: 'Po co to porównanie?', text: 'Zmiana ku większemu Eᵦ/A pomaga wyjaśnić, dlaczego fuzja lekkich i rozszczepienie ciężkich jąder mogą uwalniać energię.' }
    ]},
    { kicker: '26 · Skąd bierze się energia?', title: 'Fuzja i rozszczepienie mogą uwolnić energię wiązania', lead: 'W obu przypadkach produkty mogą mieć większą energię wiązania na nukleon niż substraty; różnica energii wynika z różnicy mas.', visual: 'energy', points: [
      { title: 'Lekkie jądra', text: 'Po połączeniu lekkich jąder (fuzja) produkt może leżeć wyżej na krzywej Eᵦ/A.' },
      { title: 'Ciężkie jądra', text: 'Podział bardzo ciężkiego jądra (rozszczepienie) tworzy średnie fragmenty silniej związane na nukleon.' },
      { title: 'Bilans', text: 'Jeśli masa produktów jest mniejsza, różnica przechodzi w energię kinetyczną i promieniowanie. To przemiana jądrowa, nie spalanie chemiczne.' }
    ]},
    { kicker: '27 · Rozszczepienie', title: 'Ciężkie jądro może podzielić się na fragmenty', lead: 'W rozszczepieniu ciężkie jądro rozpada się na dwa lżejsze jądra, zwykle uwalniając neutrony i energię.', visual: 'fission', points: [
      { title: 'Produkty są zmienne', text: 'Możliwy przykład: ²³⁵U + n → ¹⁴¹Ba + ⁹²Kr + 3n + energia. Istnieją też inne pary fragmentów.' },
      { title: 'Bilans przykładu', text: 'Liczby masowe: 235 + 1 = 141 + 92 + 3. Liczby protonów: 92 = 56 + 36.' },
      { title: 'Energia', text: 'Fragmenty i neutrony unoszą energię; późniejsze przemiany jąder potomnych mogą trwać dalej.' }
    ]},
    { kicker: '28 · Reakcja łańcuchowa', title: 'Neutrony mogą zapoczątkować kolejne rozszczepienia', lead: 'Gdy neutrony z jednego rozszczepienia wywołują następne, mówimy o reakcji łańcuchowej.', visual: 'chain', points: [
      { title: 'Liczba neutronów', text: 'Jeśli średnio jedno kolejne rozszczepienie podtrzymuje każde zdarzenie, reakcja może utrzymywać się w stanie krytycznym.' },
      { title: 'Sterowanie', text: 'W reaktorze liczbę neutronów i moc kontroluje się systemami zaprojektowanymi z myślą o bezpieczeństwie.' },
      { title: 'Zakres wyjaśnienia', text: 'To opis zasady działania. Konstrukcja i obsługa instalacji jądrowej wymagają specjalistycznej wiedzy i wielu zabezpieczeń.' }
    ]},
    { kicker: '29 · Fuzja', title: 'Gwiazdy łączą lekkie jądra; laboratoria badają D–T', lead: 'Fuzja to łączenie lekkich jąder. Dodatnie ładunki odpychają się, dlatego potrzebne są wysokie temperatury i odpowiednie warunki.', visual: 'fusion', points: [
      { title: 'W Słońcu', text: 'Dominującym źródłem energii jest łańcuch proton–proton: wodór stopniowo przekształca się w hel.' },
      { title: 'Przykład laboratoryjny', text: '²H + ³H → ⁴He + n + 17,6 MeV. Reakcja deuteru z trytem nie jest tym samym procesem co główny łańcuch w Słońcu.' },
      { title: 'Bariera elektrostatyczna', text: 'Wysoka temperatura zwiększa szansę zbliżenia jąder mimo odpychania; grawitacja ściska materię w gwiazdach, a laboratoria stosują inne metody.' }
    ]},
    { kicker: '30 · Antymateria i PET', title: 'Pozyton z elektronem może dać dwa fotony γ', lead: 'Anihilacja elektronu i pozytonu zamienia ich masę oraz energię ruchu w promieniowanie.', visual: 'antimatter', points: [
      { title: 'Anihilacja', text: 'e⁻ + e⁺ → 2γ. Dla pary w spoczynku dwa fotony mają po 511 keV i lecą w przeciwnych kierunkach, co zachowuje pęd.' },
      { title: 'Jak powstaje para?', text: 'W polu jądra wysokoenergetyczny foton może utworzyć e⁻ i e⁺; jądro przejmuje część pędu.' },
      { title: 'PET', text: 'W PET rejestruje się koincydencję fotonów z anihilacji pozytonów emitowanych przez radioznacznik. Obrazowanie ma ograniczenia i wiąże się z dawką promieniowania.' }
    ]},
    { kicker: '31 · Zastosowania', title: 'Izotopy pomagają badać, leczyć i mierzyć', lead: 'Radioizotop dobiera się do pytania: gdzie trafia substancja, jak długo jest aktywna i jaki sygnał można wykryć.', visual: 'applications', points: [
      { title: 'Diagnostyka · znacznik i PET', text: 'Znacznik podąża za wybraną cząsteczką, a emitowane promieniowanie pozwala śledzić jej rozmieszczenie. Ograniczenie: dawka i jakość sygnału.' },
      { title: 'Leczenie · radioterapia', text: 'Promieniowanie uszkadza DNA komórek w zaplanowanym obszarze; dawkę dobiera się, by ograniczać szkody w zdrowych tkankach.' },
      { title: 'Datowanie i przemysł', text: 'Stosunek izotopów pomaga szacować wiek materiału; pomiar osłabienia promieniowania kontroluje np. grubość. Wynik zależy od kalibracji, geometrii i ochrony.' }
    ]},
    { kicker: '32 · Przykład obliczeniowy', title: 'Defekt masy helu-4 daje energię wiązania 28,3 MeV', lead: 'Dane: m(¹H)=1,007825 u, mₙ=1,008665 u, m(⁴He)=4,002603 u, 1 u·c²=931,5 MeV.', visual: 'worked', points: [
      { title: '1 · Defekt masy', text: 'Δm = 2·1,007825 + 2·1,008665 − 4,002603 = 0,030377 u.' },
      { title: '2 · Energia całego jądra', text: 'Eᵦ = 0,030377·931,5 ≈ 28,3 MeV.' },
      { title: '3 · Na nukleon i kontrola', text: 'A=4, zatem Eᵦ/A ≈ 28,3/4 = 7,07 MeV/nukleon. Jednostki: u·c² daje MeV. Bilans α: ²³⁸₉₂U → ²³⁴₉₀Th + ⁴₂He; A i Z się zgadzają.' }
    ]},
    { kicker: '33 · Wnioski', title: 'Małe jądro skupia masę, a jego przemiany uwalniają energię', lead: 'Rozpraszanie odsłoniło jądro, pomiary wyjaśniły jego skład, a energia wiązania łączy budowę jądra z gwiazdami i zastosowaniami.', visual: 'conclusions', points: [
      { title: 'Masa skupia się w jądrze', text: 'Nukleony zajmują niewielką przestrzeń, lecz tworzą niemal całą masę atomu.' },
      { title: 'Dowody wyznaczają model', text: 'Rozpraszanie cząstek i bilanse rozpadu pozwalają wnioskować o składzie oraz przemianach jąder.' },
      { title: 'Wiązanie wyjaśnia energię', text: 'Fuzja lekkich i rozszczepienie ciężkich jąder mogą prowadzić do silniejszego związania i uwolnienia energii.' },
      { title: 'Zastosowanie wymaga pomiaru', text: 'Radioizotopy wspierają diagnostykę, leczenie i pomiary; aktywność, dawkę i ochronę ocenia się osobno.' }
    ]},
    { kicker: '34 · Dodatek · Pojęcia i wzory', title: 'Te definicje i zależności porządkują obliczenia', lead: 'Krótki słownik i zestaw podstawowych wzorów jako dodatek do wykładu.', visual: 'appendix', points: [
      { title: 'Słownik', text: 'Nukleon — proton lub neutron; nuklid — atom o określonym jądrze; izotopy — nuklidy o tym samym Z; defekt masy — różnica mas składników i jądra; energia wiązania — energia potrzebna do rozdzielenia jądra.' },
      { title: 'Skład i wiązanie', text: 'N = A − Z; Eᵦ = Δmc²; 1 u·c² ≈ 931,5 MeV. Dla atomowych mas helu użyj m(¹H), aby elektrony bilansowały się.' },
      { title: 'Rozpad i dawka', text: 'N = N₀·2^(−t/T₁/₂) = N₀e^(−λt); λ = ln2/T₁/₂; aktywność A = λN [Bq]. Dawka pochłonięta: Gy = J/kg; dawka równoważnikowa: Sv.' }
    ]},
    { kicker: '35 · Bibliografia i atrybucje', title: 'Źródła i atrybucje dokumentują wykład', lead: 'Pełne odnośniki do wykorzystanych rozdziałów, danych oraz lokalnych fotografii historycznych.', visual: 'references', points: []}
  ];

  const sources = [
    ['OpenStax · §10.1 Properties of Nuclei', 'https://openstax.org/books/university-physics-volume-3/pages/10-1-properties-of-nuclei'],
    ['OpenStax · §10.2 Nuclear Binding Energy', 'https://openstax.org/books/university-physics-volume-3/pages/10-2-nuclear-binding-energy'],
    ['OpenStax · §10.3 Radioactive Decay', 'https://openstax.org/books/university-physics-volume-3/pages/10-3-radioactive-decay'],
    ['OpenStax · §10.4 Nuclear Reactions', 'https://openstax.org/books/university-physics-volume-3/pages/10-4-nuclear-reactions'],
    ['OpenStax · §10.5 Fission', 'https://openstax.org/books/university-physics-volume-3/pages/10-5-fission'],
    ['OpenStax · §10.6 Nuclear Fusion', 'https://openstax.org/books/university-physics-volume-3/pages/10-6-nuclear-fusion'],
    ['OpenStax · §10.7 Medical Applications and Biological Effects', 'https://openstax.org/books/university-physics-volume-3/pages/10-7-medical-applications-and-biological-effects-of-nuclear-radiation'],
    ['NIST/CODATA · Fundamental Physical Constants', 'https://www.nist.gov/pml/fundamental-physical-constants'],
    ['Nobel Prize · Henri Becquerel', 'https://www.nobelprize.org/prizes/physics/1903/becquerel/biographical/'],
    ['Nobel Prize · Ernest Rutherford', 'https://www.nobelprize.org/prizes/chemistry/1908/rutherford/biographical/'],
    ['Nobel Prize · James Chadwick', 'https://www.nobelprize.org/prizes/physics/1935/chadwick/biographical/']
  ];

  /** @type {Record<number, string[][]>} */
  const slideSources = {
    1: [sources[0]], 2: [sources[0], sources[7]], 3: [sources[0], sources[7]],
    4: [sources[0]], 5: [sources[0]], 6: [sources[0], sources[7]],
    7: [sources[0], sources[9]], 8: [sources[8], sources[9], sources[10]],
    9: [sources[10]], 10: [sources[0]], 11: [sources[0]],
    12: [sources[2]], 13: [sources[2], sources[3]], 14: [sources[2]],
    15: [sources[2]], 16: [sources[2]], 17: [sources[2]], 18: [sources[2], sources[6]],
    19: [sources[2]], 20: [sources[2]], 21: [sources[2]], 22: [sources[6]],
    23: [sources[1], sources[7]], 24: [sources[1], sources[7]], 25: [sources[1]],
    26: [sources[1]], 27: [sources[4]], 28: [sources[4]], 29: [sources[5]],
    30: [sources[6]], 31: [sources[6]], 32: [sources[1], sources[7]],
    33: [sources[0], sources[1], sources[2], sources[4], sources[5], sources[6]]
  };

  let active = 0;
  let tocOpen = false;
  let fullscreenError = '';
  let isotopeZ = 6;
  let isotopeA = 12;
  let elapsedHalflives = 2;
  let touchStartX = 0;
  let touchStartY = 0;
  /** @type {HTMLElement | undefined} */
  let stageElement;
  /** @type {Record<number, string[]>} */
  const elements = { 1: ['H', 'wodór'], 2: ['He', 'hel'], 3: ['Li', 'lit'], 4: ['Be', 'beryl'], 5: ['B', 'bor'], 6: ['C', 'węgiel'], 7: ['N', 'azot'], 8: ['O', 'tlen'], 9: ['F', 'fluor'], 10: ['Ne', 'neon'], 11: ['Na', 'sód'], 12: ['Mg', 'magnez'], 13: ['Al', 'glin'], 14: ['Si', 'krzem'], 15: ['P', 'fosfor'], 16: ['S', 'siarka'], 17: ['Cl', 'chlor'], 18: ['Ar', 'argon'], 19: ['K', 'potas'], 20: ['Ca', 'wapń'], 26: ['Fe', 'żelazo'], 92: ['U', 'uran'] };
  /** @param {number} z */
  const symbolFor = (z) => elements[z]?.[0] ?? 'X';
  /** @param {number} z */
  const nameFor = (z) => elements[z]?.[1] ?? 'pierwiastek';
  $: isotopeNeutrons = isotopeA - isotopeZ;
  $: remainingFraction = 100 / (2 ** elapsedHalflives);
  $: slide = slides[active];

  /** @param {number} index */
  function goTo(index) {
    active = Math.max(0, Math.min(slides.length - 1, index));
    tocOpen = false;
    fullscreenError = '';
    if (stageElement) stageElement.scrollTop = 0;
  }
  const next = () => goTo(active + 1);
  const previous = () => goTo(active - 1);
  /** @param {Event & { currentTarget: HTMLInputElement }} event */
  function changeZ(event) {
    isotopeZ = Number(event.currentTarget.value);
    if (isotopeA < isotopeZ) isotopeA = isotopeZ;
  }
  /** @param {KeyboardEvent} event */
  function handleKeydown(event) {
    if (event.defaultPrevented || event.altKey || event.ctrlKey || event.metaKey) return;
    const target = event.target;
    const editing = target instanceof HTMLElement && (target.isContentEditable || ['INPUT', 'TEXTAREA', 'SELECT', 'BUTTON'].includes(target.tagName));
    if (event.key === 'Escape') { tocOpen = false; return; }
    if (editing || tocOpen) return;
    if (event.key === 'ArrowRight' || event.key === ' ') { event.preventDefault(); next(); }
    else if (event.key === 'ArrowLeft') { event.preventDefault(); previous(); }
    else if (event.key === 'Home') { event.preventDefault(); goTo(0); }
    else if (event.key === 'End') { event.preventDefault(); goTo(slides.length - 1); }
    else if (event.key.toLowerCase() === 'f') toggleFullscreen();
  }
  async function toggleFullscreen() {
    fullscreenError = '';
    try {
      if (document.fullscreenElement) await document.exitFullscreen();
      else await document.documentElement.requestFullscreen();
    } catch { fullscreenError = 'Przeglądarka nie udostępniła trybu pełnoekranowego.'; }
  }
  /** @param {TouchEvent} event */
  function touchStart(event) {
    touchStartX = event.changedTouches[0].clientX;
    touchStartY = event.changedTouches[0].clientY;
  }
  /** @param {TouchEvent} event */
  function touchEnd(event) {
    const dx = event.changedTouches[0].clientX - touchStartX;
    const dy = event.changedTouches[0].clientY - touchStartY;
    if (Math.abs(dx) > 65 && Math.abs(dx) > Math.abs(dy) * 1.3) dx < 0 ? next() : previous();
  }
</script>

<svelte:window onkeydown={handleKeydown} />

<div class="presentation" role="region" aria-label="Prezentacja o jądrze atomowym" ontouchstart={touchStart} ontouchend={touchEnd}>
  <header class="topbar">
    <a class="brand" href="#start" onclick={(event) => { event.preventDefault(); goTo(0); }} aria-label="Wróć do początku"><span class="brand-mark">J</span><span>Jądro atomowe</span></a>
    <div class="chapter-label">{slide.kicker}</div>
    <div class="top-actions">
      <span class="counter"><b>{String(active + 1).padStart(2, '0')}</b><span>/</span>{String(slides.length).padStart(2, '0')}</span>
      <button class="icon-button" onclick={() => tocOpen = !tocOpen} aria-label="Otwórz spis slajdów" aria-expanded={tocOpen} title="Spis slajdów">☷</button>
      <button class="icon-button" onclick={toggleFullscreen} aria-label="Przełącz tryb pełnoekranowy" title="Pełny ekran (F)">⛶</button>
    </div>
  </header>

  <main class="stage" bind:this={stageElement} aria-live="polite">
    {#key active}
    <section class:hero-slide={active === 0} class:conclusions-slide={slide.visual === 'conclusions'} class:references-slide={slide.visual === 'references'} class="slide" aria-labelledby="slide-title">
      <div class="slide-heading">
        <div class="heading-copy">
          <div class="eyebrow"><span class="eyebrow-line"></span>{slide.kicker}</div>
          <h1 id="slide-title">{slide.title}</h1>
          <p class="lead">{slide.lead}</p>
        </div>
      </div>

      <div class="lesson-layout">
        <figure class="visual-panel">
          <figcaption class="visual-label"><span>Wizualizacja</span></figcaption>
          <div class="visual-body">
            {#if slide.visual === 'hero' || slide.visual === 'atom'}
              <AtomModel />
            {:else if slide.visual === 'scale'}
              <div class="scale-sketch"><div class="scale-atom" aria-hidden="true"><div class="scale-cloud"></div><div class="scale-nucleus"></div></div><div class="scale-labels"><b>ATOM <span>≈ 10⁻¹⁰ m</span></b><i>Promień ≈ 100 000 × większy</i><b>JĄDRO <span>≈ 10⁻¹⁵ m</span></b><small>Chmura elektronowa · jądro powiększone</small><small>R ≈ 1,2 fm · A^(1/3)</small></div></div>
            {:else if slide.visual === 'nucleons'}
              <div class="particle-row"><div class="particle proton">p⁺<small>proton</small></div><div class="particle neutron">n⁰<small>neutron</small></div><div class="particle electron">e⁻<small>elektron</small></div></div>
            {:else if slide.visual === 'notation'}
              <div class="notation-demo">
                <div class="nuclide"><sup>{isotopeA}</sup><sub>{isotopeZ}</sub>{symbolFor(isotopeZ)}</div>
                <div class="notation-key"><span><b>A</b> protony + neutrony</span><span><b>Z</b> protony</span><span><b>N</b> {isotopeA} − {isotopeZ} = {isotopeNeutrons}</span></div>
                <label for="protons">Z · protony <output>{isotopeZ} · {nameFor(isotopeZ)}</output></label><input id="protons" type="range" min="1" max="20" value={isotopeZ} oninput={changeZ} />
                <label for="mass-number">A · liczba nukleonów <output>{isotopeA}</output></label><input id="mass-number" type="range" min={isotopeZ} max="40" value={isotopeA} oninput={(event) => isotopeA = Number(event.currentTarget.value)} />
              </div>
            {:else if slide.visual === 'isotopes'}
              <div class="isotope-compare">
                <div><strong>¹H</strong><span>1 p · 0 n</span><i class="nucleus tiny"><b>p</b></i></div><div class="same-z">TEN SAM Z = 1</div><div><strong>²H</strong><span>1 p · 1 n</span><i class="nucleus"><b>p</b><b>n</b></i></div><div><strong>³H</strong><span>1 p · 2 n</span><i class="nucleus"><b>p</b><b>n</b><b>n</b></i></div>
              </div>
            {:else if slide.visual === 'families'}
              <div class="family-board"><div class="family-equation"><b>¹²₆C</b><span>izotopy</span><b>¹⁴₆C</b></div><div class="family-equation"><b>¹⁴₆C</b><span>izobary</span><b>¹⁴₇N</b></div><div class="family-equation"><b>¹⁴₆C</b><span>izotony · N = 8</span><b>¹⁵₇N</b></div><div class="average">węgiel naturalny <strong>≈ 12,011 u</strong><small>średnia ważona izotopów</small></div></div>
            {:else if slide.visual === 'scattering'}
              <div class="scattering-figure"><img src={geigerMarsdenReconstruction} alt="Współczesna rekonstrukcja CGI aparatury Geigera–Marsdena, nie fotografia z 1909 roku." /><div class="scatter-paths"><span class="straight">α → → →</span><span class="deflect">↗</span><span class="return">←</span><b>folia Au</b></div><p>większość prosto · nieliczne silne odchylenia</p></div>
            {:else if slide.visual === 'history'}
              <div class="history-figure"><div class="history-images"><figure><img src={becquerelPortrait} alt="Portret Henriego Becquerela, fotografia Paula Nadara." /><figcaption>Becquerel · 1896</figcaption></figure><figure><img src={rutherfordPortrait} alt="Portret Ernesta Rutherforda ze zbiorów Smithsonian." /><figcaption>Rutherford · model jądra</figcaption></figure><figure><img src={munsterGroup} alt="Grupowe zdjęcie zjazdu naukowców w Münster w 1932 roku; wśród uczestników Chadwick i Rutherford." /><figcaption>Münster · 1932</figcaption></figure></div><ol><li><b>1896</b> klisza uranowa</li><li><b>1909–11</b> rozpraszanie α</li><li><b>1932</b> neutron</li></ol><small>Zdjęcie zjazdu nie przedstawia doświadczenia Chadwicka.</small></div>
            {:else if slide.visual === 'chadwick'}
              <div class="chadwick-diagram"><div class="target berillium">Be</div><span class="beam">n⁰? → →</span><div class="target paraffin">parafina</div><span class="proton-track">H⁺ ↗</span><div class="measure">pomiar<br />odrzutu</div></div>
            {:else if slide.visual === 'forces'}
              <div class="force-diagram"><div class="force-pair"><span>p⁺</span><span>p⁺</span><span>n⁰</span></div><div class="force-repel">← odpychanie Coulombowskie →</div><div class="force-bind">↔ przyciąganie silne blisko</div><div class="range-scale">daleki zasięg <i></i> krótki zasięg</div></div>
            {:else if slide.visual === 'stability'}
              <svg class="diagram-svg stability-chart" viewBox="0 0 560 310" role="img" aria-labelledby="stability-title"><title id="stability-title">Schematyczny wykres neutronów N względem protonów Z</title><path class="axis" d="M70 25V245H485"/><path class="grid" d="M70 190H485M70 135H485M70 80H485"/><path class="valley" d="M90 211C180 180 250 145 315 112S420 76 466 53"/><path class="line-of-equal" d="M90 230L445 35"/><circle cx="128" cy="197" r="8"/><circle cx="206" cy="166" r="8"/><circle cx="290" cy="129" r="8"/><circle cx="367" cy="97" r="8"/><text x="285" y="52">pasmo stabilności</text><text x="240" y="278">liczba protonów Z →</text><text class="stability-y-label" transform="translate(22 255) rotate(-90)">liczba neutronów N →</text><text x="99" y="115">N = Z</text></svg>
            {:else if slide.visual === 'random'}
              <div class="random-decay"><div class="parent-nucleus">jądro<br />niestabilne</div><span class="decay-arrow">→</span><div class="daughter-nucleus">jądro<br />córka</div><div class="random-dots"><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i></div><small>chwile rozpadu są różne</small></div>
            {:else if slide.visual === 'balance'}
              <div class="balance-visual"><div class="nuclear-equation"><span>²³⁸₉₂U</span><i>→</i><span>²³⁴₉₀Th</span><b>+</b><span>⁴₂He</span></div><div class="balance-check"><p>A: <b>238 = 234 + 4</b></p><p>Z: <b>92 = 90 + 2</b></p></div><small>liczba masowa · ładunek jądrowy</small></div>
            {:else if slide.visual === 'alpha' || slide.visual === 'beta-minus' || slide.visual === 'beta-plus'}
              <div class="decay-visual"><div class="decay-parent">X</div><span class="decay-arrow">→</span><div class="decay-products">{#if slide.visual === 'alpha'}<span>Y + ⁴₂He</span><small>A−4 · Z−2</small>{:else if slide.visual === 'beta-minus'}<span>Y + e⁻ + ν̄ₑ</span><small>A bez zmian · Z+1</small>{:else}<span>Y + e⁺ + νₑ</span><small>A bez zmian · Z−1</small>{/if}</div>{#if slide.visual === 'beta-minus'}<div class="conversion">n → p</div>{:else if slide.visual === 'beta-plus'}<div class="conversion">p → n</div>{:else}<div class="alpha-cluster">2p + 2n</div>{/if}</div>
            {:else if slide.visual === 'gamma'}
              <div class="energy-levels"><div class="level high"><b>X*</b><span>stan wzbudzony</span></div><div class="photon">γ ↘</div><div class="level low"><b>X</b><span>stan o niższej energii</span></div><small>ΔE = hν · A i Z bez zmian</small></div>
            {:else if slide.visual === 'radiation'}
              <div class="radiation-figure"><div class="field-label">pole elektryczne</div><div class="radiation-row"><b>α</b><span class="ray alpha-ray">↗</span><small>+2e</small></div><div class="radiation-row"><b>β⁻</b><span class="ray beta-ray">↘</span><small>−e</small></div><div class="radiation-row"><b>γ</b><span class="ray gamma-ray">→</span><small>0</small></div><div class="shields"><span>papier</span><span>metal</span><span>gruba osłona*</span></div><small>*schemat jakościowy, nie gwarancja ochrony</small></div>
            {:else if slide.visual === 'halflife' || slide.visual === 'carbon'}
              <div class="decay-chart"><div class="chart-title">{slide.visual === 'carbon' ? 'PRAWO ROZPADU · PRÓBKA' : 'POZOSTAŁE JĄDRA · %'}</div><svg viewBox="0 0 560 300" role="img" aria-label="Wykres wykładniczego spadku liczby jąder w kolejnych okresach półtrwania"><path class="chart-axis" d="M55 30V235H495"/><path class="chart-grid" d="M55 81H495M55 132H495M55 183H495"/><text class="axis-label" text-anchor="end" x="54" y="36">100%</text><text class="axis-label" text-anchor="end" x="54" y="137">50%</text><text class="axis-label" text-anchor="end" x="54" y="239">0</text><path class="decay-curve" d="M55 30C90 93 125 130 143 132S190 182 231 183S276 208 319 209S369 221 407 222S455 228 495 230"/><path class="chart-cursor" d={`M${55 + elapsedHalflives * 88} 30V235`} /><circle class="chart-point" cx={55 + elapsedHalflives * 88} cy={235 - remainingFraction * 2.05} r="9"/><text x="65" y="260">0</text><text x="142" y="260">1</text><text x="230" y="260">2</text><text x="318" y="260">3</text><text x="406" y="260">4</text><text x="435" y="260">5 T₁/₂</text></svg>{#if slide.visual === 'halflife'}<label for="halflives">Upływ czasu <output>{elapsedHalflives} × T₁/₂ · {remainingFraction.toFixed(2)}%</output></label><input id="halflives" type="range" min="0" max="5" step="1" bind:value={elapsedHalflives} />{:else}<div class="c14-line"><b>5730 lat</b><span>1 → 1/2 → 1/4</span><small>2 T₁/₂ ≈ 11 460 lat</small></div>{/if}</div>
            {:else if slide.visual === 'activity'}
              <div class="activity-diagram"><div class="activity-row"><b>Aktywność</b><span>A = λN</span><small>rozpad / s</small></div><div class="activity-row"><b>Wielkość źródła</b><span>N</span><small>liczba jąder</small></div><div class="activity-row"><b>Stała rozpadu</b><span>λ</span><small>prawdopodobieństwo / czas</small></div><div class="unit-seal">1 Bq = 1 rozpad/s</div></div>
            {:else if slide.visual === 'dose'}
              <div class="dose-diagram"><div><b>Bq</b><span>źródło</span><i></i><small>rozpady/s</small></div><div><b>Gy</b><span>pochłonięta energia</span><i></i><small>J/kg</small></div><div><b>Sv</b><span>rodzaj promieniowania</span><i></i><small>równoważnik dawki</small></div></div>
            {:else if slide.visual === 'mass'}
              <div class="mass-diagram"><div class="free-mass"><span>p⁺</span><span>p⁺</span><span>n⁰</span><span>n⁰</span></div><b>−</b><div class="bound-mass">⁴He</div><i>Δm</i><p>masa swobodnych nukleonów większa</p></div>
            {:else if slide.visual === 'helium'}
              <div class="helium-work"><div class="mass-line"><span>2m(¹H)+2mₙ</span><b>4,03298 u</b></div><div class="mass-line"><span>m(⁴He)</span><b>4,002603 u</b></div><div class="mass-difference">Δm ≈ 0,03038 u</div><div class="energy-result">Eᵦ ≈ <strong>28,3 MeV</strong></div><small>dla 4 nukleonów ≈ 7,07 MeV/nukleon</small></div>
            {:else if slide.visual === 'curve' || slide.visual === 'energy'}
              <div class="binding-curve"><svg viewBox="0 0 600 320" role="img" aria-label="Jakościowa krzywa energii wiązania na nukleon, maksimum w okolicy żelaza i niklu"><path class="chart-axis" d="M52 25V240H555"/><path class="chart-grid" d="M52 187H555M52 133H555M52 79H555"/><text transform="translate(26 210) rotate(-90)">Eᵦ/A [MeV]</text><text x="240" y="285">liczba masowa A →</text><path class="binding-fill" d="M55 230C100 130 142 84 190 66S285 41 337 49S425 66 550 83V240H55Z"/><path class="binding-line" d="M55 230C100 130 142 84 190 66S285 41 337 49S425 66 550 83"/><text x="260" y="38">okolice Fe / Ni</text><text x="63" y="260">fuzja</text><text x="380" y="107">rozszczepienie</text></svg><p>Lżejsze i cięższe jądra mogą przejść ku większemu Eᵦ/A.</p></div>
            {:else if slide.visual === 'fission'}
              <div class="fission-diagram"><div class="nucleus-large">²³⁵U + n</div><span class="reaction-arrow">→</span><div class="fragments"><b>¹⁴¹Ba</b><b>⁹²Kr</b><small>+ 3n + energia</small></div><div class="variable-products">możliwy kanał rozszczepienia · produkty bywają różne</div></div>
            {:else if slide.visual === 'chain'}
              <div class="chain-diagram"><div class="chain-node">jądro<br />dzieli się</div><div class="chain-arrows">↙ <span>n</span> ↘</div><div class="chain-node small-node">jądro</div><div class="chain-node small-node">jądro</div><div class="chain-footer">kontrolowana liczba neutronów → reakcja ustalona</div></div>
            {:else if slide.visual === 'fusion'}
              <div class="fusion-diagram"><div class="deuterium">²H</div><b>+</b><div class="tritium">³H</div><i>→</i><div class="helium-product">⁴He</div><span>+ n + 17,6 MeV</span><small>Słońce: głównie łańcuch proton–proton</small></div>
            {:else if slide.visual === 'antimatter'}
              <div class="pet-diagram"><div class="annihilation-equation"><b>e⁻</b> + <b>e⁺</b> → <strong>γ ↗　↙ γ</strong></div><div class="photons">511 keV <i>←</i> <i>→</i> 511 keV</div><div class="pet-ring"><span>detektory</span><b>●</b></div><small>koincydencja fotonów lokalizuje miejsce anihilacji</small></div>
            {:else if slide.visual === 'applications'}
              <div class="application-map"><div class="app-node"><b>znacznik</b><span>diagnostyka / PET</span></div><div class="app-node"><b>wiązka</b><span>radioterapia</span></div><div class="app-node"><b>izotopy</b><span>datowanie</span></div><div class="app-node"><b>sygnał</b><span>pomiary przemysłowe</span></div></div>
            {:else if slide.visual === 'worked'}
              <div class="worked-diagram"><div class="worked-step"><b>01</b><span>Δm = 0,030377 u</span></div><div class="worked-step"><b>02</b><span>× 931,5 MeV/u</span></div><div class="worked-step"><b>03</b><span>28,3 MeV</span></div><div class="worked-step final-step"><b>04</b><span>÷ A = 4 → 7,07 MeV/nukleon</span></div></div>
            {:else if slide.visual === 'conclusions'}
              <div class="conclusion-map" aria-label="Od budowy jądra do dowodów, energii i zastosowań">
                <div><b>01</b><span>skład<br />jądra</span></div><i>→</i><div><b>02</b><span>obserwacje<br />i pomiary</span></div><i>→</i><div><b>03</b><span>energia<br />wiązania</span></div><i>→</i><div><b>04</b><span>zastosowania<br />i ochrona</span></div>
              </div>
            {:else if slide.visual === 'appendix'}
              <div class="formula-sheet">
                <p><b>Skład nuklidu</b><span>N = A − Z</span></p>
                <p><b>Energia wiązania</b><span>Eᵦ = Δmc²</span></p>
                <p><b>Prawo rozpadu</b><span>N(t) = N₀ · 2<sup>−t/T₁/₂</sup> = N₀e<sup>−λt</sup></span></p>
                <p><b>Aktywność</b><span>A = λN · [Bq]</span></p>
                <p><b>Dawka</b><span>Gy = J/kg · Sv</span></p>
              </div>
            {:else}
              <div class="reference-lead"><b>Materiały źródłowe</b><span>OpenStax · NIST/CODATA · Nobel Prize</span><small>Pełne odnośniki i atrybucje po prawej.</small></div>
            {/if}
          </div>
          {#if slide.visual === 'scattering'}<figcaption class="figure-credit">Współczesna rekonstrukcja CGI (nie oryginalna aparatura): <a href="https://commons.wikimedia.org/wiki/File:Geiger-Marsden_apparatus_2_CGI_mock-up.jpg" target="_blank" rel="noreferrer">Kurzon · CC BY 4.0 · Wikimedia Commons ↗</a></figcaption>{/if}
          {#if slide.visual === 'history'}<figcaption class="figure-credit">Atrybucje: <a href="https://commons.wikimedia.org/wiki/File:Paul_Nadar_-_Henri_Becquerel.jpg" target="_blank" rel="noreferrer">Paul Nadar · domena publiczna</a> · <a href="https://commons.wikimedia.org/wiki/File:Portrait_of_Ernest_Rutherford_(1871-1937),_Physicist_and_Chemist_(2551070939).jpg" target="_blank" rel="noreferrer">Smithsonian / Wikimedia Commons</a> · <a href="https://commons.wikimedia.org/wiki/File:Bunsentagung_1932_Münster.jpg" target="_blank" rel="noreferrer">US Department of Energy · domena publiczna</a></figcaption>{/if}
        </figure>

        <div class="explanation-panel">
          {#if slide.visual === 'notation'}<div class="definition-strip"><b>Przeczytaj:</b> ᴬ_ZX = nuklid o Z protonach i A−Z neutronach.</div>{/if}
          <div class="point-list">
            {#each slide.points as point, i}
              <article class="point"><span class="point-index">{String(i + 1).padStart(2, '0')}</span><div><h2>{point.title}</h2><p>{point.text}</p></div></article>
            {/each}
          </div>
          {#if slideSources[active]}
            <p class="slide-citation">Źródła: {#each slideSources[active] as source, i}{#if i},&nbsp;{/if}<a href={source[1]} target="_blank" rel="noreferrer">{source[0]}</a>{/each}</p>
          {/if}
          {#if slide.visual === 'references'}
            <div class="source-links"><h2>Źródła merytoryczne</h2><ul>{#each sources as source}<li><a href={source[1]} target="_blank" rel="noreferrer">{source[0]} ↗</a></li>{/each}</ul></div>
            <div class="image-credits"><b>Atrybucje lokalnych zdjęć</b><ul>
              <li>Becquerel · Paul Nadar, domena publiczna · <a href="https://commons.wikimedia.org/wiki/File:Paul_Nadar_-_Henri_Becquerel.jpg" target="_blank" rel="noreferrer">Wikimedia Commons</a></li>
              <li>Rutherford · Smithsonian Institution Libraries, „No known copyright restrictions” · <a href="https://commons.wikimedia.org/wiki/File:Portrait_of_Ernest_Rutherford_(1871-1937),_Physicist_and_Chemist_(2551070939).jpg" target="_blank" rel="noreferrer">Wikimedia Commons</a></li>
              <li>Rekonstrukcja Geigera–Marsdena · Kurzon, CC BY 4.0 · <a href="https://commons.wikimedia.org/wiki/File:Geiger-Marsden_apparatus_2_CGI_mock-up.jpg" target="_blank" rel="noreferrer">Wikimedia Commons</a></li>
              <li>Münster 1932 · US Department of Energy, domena publiczna · <a href="https://commons.wikimedia.org/wiki/File:Bunsentagung_1932_Münster.jpg" target="_blank" rel="noreferrer">Wikimedia Commons</a></li>
            </ul></div>
          {/if}
        </div>
      </div>
    </section>
    {/key}
  </main>

  <footer class="bottombar">
    <div class="progress-label"><span>POSTĘP</span><span>{active + 1} / {slides.length}</span></div>
    <div class="progress-track" role="progressbar" aria-label="Postęp prezentacji" aria-valuemin="1" aria-valuemax={slides.length} aria-valuenow={active + 1}>
      <div class="progress-fill" style={`width:${((active + 1) / slides.length) * 100}%`}></div>
      {#each slides as item, i}<button class:current={active === i} class="progress-point" style={`left:${(i / (slides.length - 1)) * 100}%`} onclick={() => goTo(i)} aria-label={`Przejdź do slajdu ${i + 1}: ${item.title}`} title={item.title}></button>{/each}
    </div>
    <div class="footer-controls"><span class="footer-caption">Fizyka jądrowa · kurs maturalny</span><div class="nav-buttons"><button class="nav-arrow" onclick={previous} disabled={active === 0} aria-label="Poprzedni slajd">←</button><button class="nav-arrow" onclick={next} disabled={active === slides.length - 1} aria-label="Następny slajd">→</button></div></div>
  </footer>

  {#if fullscreenError}<div class="toast" role="status">{fullscreenError}</div>{/if}
  {#if tocOpen}<div class="toc-backdrop" role="presentation" onclick={(event) => { if (event.target === event.currentTarget) tocOpen = false; }}><nav class="toc-panel" aria-label="Spis slajdów"><div class="toc-header"><div><span>NAWIGACJA</span><h2>Spis treści</h2></div><button class="icon-button" onclick={() => tocOpen = false} aria-label="Zamknij spis">×</button></div><ol>{#each slides as item, i}<li><button class:toc-current={active === i} onclick={() => goTo(i)}><span>{String(i + 1).padStart(2, '0')}</span><b>{item.title}</b><i>↗</i></button></li>{/each}</ol><p class="toc-help">Klawisze ← → · Home / End · Esc zamyka</p></nav></div>{/if}
</div>
