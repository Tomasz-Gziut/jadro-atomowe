<script>
  import AtomModel from './AtomModel.svelte';
  const slides = [
    { kicker: '18.1 · Jądro atomowe', title: 'Atom jest niemal pusty. Jądro skupia jego masę.', lead: 'Doświadczenie z folią złota zmieniło obraz atomu: masywny, dodatni środek zajmuje znikomo małą część jego rozmiaru.', visual: 'hero-composition', points: [
      { title: 'Co znajduje się w jądrze', text: 'Protony i neutrony — nukleony. Protony nadają jądru dodatni ładunek.' },
      { title: 'Jak czytać prezentację', text: 'Każdy schemat zaznacza, co przedstawia i które proporcje są umowne. Rozmiary cząstek nie są rysowane w skali.' }
    ]},
    { kicker: '01 · Przypomnienie', title: 'Atom składa się z jądra i otaczających go elektronów', lead: 'W tym temacie przenosimy uwagę z elektronów na budowę jądra atomowego.', visual: 'electron-cloud', points: [
      { title: 'Ładunki składników', text: 'Proton ma ładunek +e, elektron −e, a neutron jest elektrycznie obojętny. Ładunek elementarny e ≈ 1,602 · 10⁻¹⁹ C.' },
      { title: 'Atom obojętny', text: 'Liczba elektronów jest równa liczbie protonów, więc ładunki atomu się równoważą.' },
      { title: 'Uwaga na obraz', text: 'Elektron nie jest małą planetą na wyznaczonej orbicie. Chmura kwantowa pokazuje rozkład prawdopodobieństwa pomiaru jego położenia.' }
    ]},
    { kicker: '02 · Rozmiar i masa', title: 'Niewielkie jądro skupia niemal całą masę atomu', lead: 'Większość objętości atomu zajmuje przestrzeń wokół jądra, ale prawie cała jego masa znajduje się w jądrze.', visual: 'scale', points: [
      { title: 'Różnica skali', text: 'Promień jądra ma rząd 10⁻¹⁵ m, a rozmiar atomu rząd 10⁻¹⁰ m. To około 10⁵ razy różnicy liniowo; dokładny stosunek zależy od atomu i izotopu.' },
      { title: 'Masy składników', text: 'Proton i neutron mają zbliżone masy. Elektron jest od każdego z nich około 2000 razy lżejszy.' },
      { title: 'Wniosek', text: 'To nukleony, a nie elektrony, odpowiadają za niemal całą masę atomu.' }
    ]},
    { kicker: '03 · Nukleony', title: 'Protony i neutrony to nukleony', lead: 'Obie cząstki wchodzą w skład jądra i mają masy zbliżone do atomowej jednostki masy.', visual: 'particle-properties', points: [
      { title: 'Proton p⁺', text: 'Składnik jądra o ładunku +e i masie około 1,6726 · 10⁻²⁷ kg.' },
      { title: 'Neutron n⁰', text: 'Składnik jądra bez ładunku elektrycznego; jego masa to około 1,6749 · 10⁻²⁷ kg.' },
      { title: 'Elektron e⁻', text: 'Ma ładunek −e i masę około 1836 razy mniejszą od masy protonu (w przybliżeniu 2000 razy mniejszą od nukleonu).' }
    ]},
    { kicker: '04 · Izotopy', title: 'Izotopy mają tyle samo protonów, ale różną liczbę neutronów', lead: 'Jądra atomów tego samego pierwiastka mają jednakowe Z, lecz mogą różnić się składem neutronowym.', visual: 'isotopes', points: [
      { title: 'Wodór w przyrodzie', text: 'Prot stanowi około 99,985% wodoru, deuter około 0,015%, a tryt występuje w ilościach śladowych.' },
      { title: 'Izotopy węgla', text: 'Węgiel-12 ma 6 protonów i 6 neutronów, a węgiel-14 — 6 protonów i 8 neutronów.' },
      { title: 'Węgiel w obiegu przyrody', text: 'Węgiel-12 jest stabilny i zdecydowanie najczęstszy. Śladowy węgiel-14 powstaje w atmosferze pod wpływem promieniowania kosmicznego i trafia do organizmów w obiegu węgla.' }
    ]},
    { kicker: '05 · Właściwości chemiczne', title: 'Izotopy tego samego pierwiastka reagują prawie tak samo', lead: 'Różnice liczby neutronów zmieniają jądro, ale nie zmieniają liczby protonów pierwiastka.', visual: 'families', points: [
      { title: 'To samo miejsce w układzie', text: 'Nazwa „izotop” nawiązuje do wspólnego miejsca pierwiastka w układzie okresowym: izotopy mają to samo Z.' },
      { title: 'Ten sam atom obojętny', text: 'Izotopy obojętne mają taką samą liczbę elektronów i tę samą konfigurację elektronową.' },
      { title: 'Podobna chemia', text: 'O właściwościach chemicznych decydują głównie elektrony, zwłaszcza walencyjne, dlatego izotopy reagują prawie tak samo. Różnice mas mogą powodować niewielkie efekty izotopowe.' }
    ]},
    { kicker: '06 · Liczby Z i A', title: 'Liczby atomowa i masowa opisują skład jądra', lead: 'Zapis izotopu podaje symbol pierwiastka, liczbę protonów oraz łączną liczbę nukleonów.', visual: 'notation', points: [
      { title: 'Liczba atomowa Z', text: 'To liczba protonów w jądrze; określa pierwiastek i jego numer w układzie okresowym. Ładunek jądra to +Ze.' },
      { title: 'Liczba masowa A', text: 'To suma protonów i neutronów. Liczbę neutronów obliczamy: N = A − Z.' },
      { title: 'Przykład węgla-14', text: '¹⁴₆C ma Z = 6 protonów oraz A = 14 nukleonów, więc N = 14 − 6 = 8 neutronów. Ładunek jądra wynosi +6e.' }
    ]},
    { kicker: '07 · Doświadczenie', title: 'Kilka cząstek zawróciło. To zmieniło model atomu.', lead: 'Geiger i Marsden w 1909 r. badali rozpraszanie cząstek alfa na cienkiej folii złota. Rutherford wyjaśnił wyniki modelem jądrowym w 1911 r.', visual: 'scattering', points: [
      { title: 'Model Thomsona', text: 'W ówczesnym modelu ładunek dodatni był rozłożony w atomie, a elektrony znajdowały się wewnątrz tej masy („ciasto z rodzynkami”).' },
      { title: 'Układ pomiarowy', text: 'Źródło wysyłało cząstki alfa (jądra helu) przez kolimator z ołowiu na cienką folię złota. Ruch cząstek wykrywano ekranem scyntylacyjnym.' },
      { title: 'Obserwacje', text: 'Zdecydowana większość cząstek przechodziła prawie prosto, lecz nieliczne odchylały się silnie, a niektóre zawracały.' }
    ]},
    { kicker: '08 · Odkrycie jądra', title: 'Silne odchylenia ujawniły małe, dodatnie jądro', lead: 'Wyniki rozpraszania nie pasowały do ładunku dodatniego rozłożonego równomiernie w atomie.', visual: 'deflection', points: [
      { title: 'Większość przechodzi prosto', text: 'W atomie nie ma zwartej materii wypełniającej całą objętość. Większość cząstek alfa mija jądra daleko.' },
      { title: 'Nieliczne silnie się odchylają', text: 'Dodatnia cząstka alfa jest odpychana przez dodatnie jądro. Bliskie minięcie ciężkiego jądra może mocno zmienić jej tor, nie wymaga mechanicznego zderzenia.' },
      { title: 'Wniosek modelu', text: 'Dodatni ładunek i niemal cała masa atomu są skupione w małym jądrze. Eksperyment ogranicza możliwe modele budowy atomu; nie jest fotografią jądra.' }
    ]},
    { kicker: '09 · Masa atomowa', title: 'Liczba masowa to nie to samo co masa atomowa', lead: 'A jest całkowitą liczbą nukleonów, natomiast masa atomowa uwzględnia rzeczywistą masę atomu i występowanie jego izotopów.', visual: 'atomic-mass', points: [
      { title: 'Jednostka u', text: 'Jednostkę masy atomowej zdefiniowano jako 1/12 masy obojętnego atomu węgla-12. 1 u ≈ 1,6605 · 10⁻²⁷ kg.' },
      { title: 'Masy składników', text: 'Masy protonu, neutronu i jednostki u różnią się o mniej niż 1%. Elektron jest dużo lżejszy, ale jego masa także wchodzi do masy atomu.' },
      { title: 'Średnia izotopowa', text: 'Masa pierwiastka w układzie okresowym jest średnią ważoną mas jego naturalnych izotopów. Dla miedzi to około 63,55 u; w naturze występują głównie ⁶³Cu i ⁶⁵Cu.' }
    ]},
    { kicker: '10 · Oddziaływania jądrowe', title: 'Jądro utrzymuje siła o bardzo krótkim zasięgu', lead: 'Dodatnie protony odpychają się elektrycznie. W jądrze wiąże je silne oddziaływanie między nukleonami.', visual: 'forces', points: [
      { title: 'Odpychanie Coulombowskie', text: 'Działa między protonami i ma daleki zasięg. Im więcej protonów, tym większe łączne odpychanie w jądrze.' },
      { title: 'Oddziaływanie jądrowe', text: 'Jest skutkiem oddziaływania silnego między kwarkami; jego resztkowa postać wiąże bliskie nukleony: protony i neutrony. Działa na odległościach rzędu femtometrów.' },
      { title: 'Stabilność', text: 'Przy typowych odległościach przyciąganie jądrowe równoważy odpychanie protonów. W ciężkich jądrach równowaga jest mniej korzystna, dlatego wiele z nich jest niestabilnych.' }
    ]},
    { kicker: '11 · Cząstki', title: 'Proton i neutron nie są dziś uznawane za elementarne', lead: 'To doprecyzowanie terminologii użytej w szkolnym fragmencie: współczesna fizyka rozróżnia cząstki elementarne i złożone.', visual: 'quarks', points: [
      { title: 'Cząstki złożone', text: 'Protony i neutrony to hadrony zbudowane z kwarków związanych gluonami. Swobodnych kwarków nie obserwuje się.' },
      { title: 'Cząstki elementarne', text: 'Elektron i neutrina to leptony zaliczane do cząstek elementarnych. Ich niezerowa masa wymaga rozszerzenia minimalnego Modelu Standardowego. Foton jest kwantem pola elektromagnetycznego; w fizyce jądrowej γ oznacza foton o dowolnej energii.' },
      { title: 'Konwencja podręcznika', text: 'Szkolny tekst nazywa nukleony „cząstkami elementarnymi” jako składniki jądra. We współczesnym, ścisłym znaczeniu proton i neutron są złożone.' }
    ]},
    { kicker: '12 · Materia i antymateria', title: 'Pozyton jest antycząstką elektronu', lead: 'Antycząstka ma taką samą masę jak odpowiadająca jej cząstka; dla cząstek naładowanych znaki ładunku są przeciwne.', visual: 'antimatter', points: [
      { title: 'Antycząstka elektronu', text: 'Pozyton e⁺ ma taką samą masę jak elektron e⁻, ale ładunek +e. Foton jest własną antycząstką.' },
      { title: 'Anihilacja', text: 'Para elektron–pozyton w spoczynku może zamienić się w dwa przeciwbieżne fotony po 511 keV: e⁻ + e⁺ → 2γ. Zachowane są energia i pęd.' },
      { title: 'Kreacja pary', text: 'Foton w polu jądra może utworzyć elektron i pozyton, gdy ma co najmniej 1,022 MeV na ich masy spoczynkowe, a w praktyce nieco więcej na odrzut jądra. Przewaga materii we Wszechświecie nadal nie ma pełnego wyjaśnienia.' }
    ]},
    { kicker: '13 · Przykład', title: 'Hel ma niemal dwukrotnie większą gęstość niż wodór', lead: 'Oszacowanie wykorzystuje izotopy najczęściej spotykane w przyrodzie i jednakową objętość molową gazów.', visual: 'density-worked', points: [
      { title: 'Porównanie mas molowych', text: 'Wodór gazowy to głównie cząsteczki H₂ o masie około 2 u na cząsteczkę. Hel jest gazem jednoatomowym, głównie ⁴He, o masie około 4 u na atom.' },
      { title: 'Te same warunki', text: 'Dla gazów w tej samej temperaturze i pod tym samym ciśnieniem równe objętości zawierają tyle samo cząstek (prawo Avogadra).' },
      { title: 'Wynik', text: 'Stosunek gęstości jest więc w przybliżeniu równy stosunkowi mas cząstek: 4/2 = 2. Z podanych wartości tablicowych: (0,164 kg/m³)/(0,0823 kg/m³) ≈ 1,993.' }
    ]},
    { kicker: '14 · Średnia masa atomowa', title: 'Masa atomowa uwzględnia naturalne udziały izotopów', lead: 'W układzie okresowym podana jest średnia ważona mas izotopów danego pierwiastka.', visual: 'chlorine-average', points: [
      { title: 'Chlor w przyrodzie', text: 'Naturalny chlor to głównie izotopy ³⁵Cl i ³⁷Cl. Udziały atomów wynoszą w przybliżeniu 76% i 24%; wartości są zaokrąglone.' },
      { title: 'Średnia liczb masowych', text: 'Dla tych udziałów średnia ważona wynosi 0,76 · 35 + 0,24 · 37 = 35,48.' },
      { title: 'Porównanie z tablicami', text: 'Masa atomowa chloru to około 35,45 u. Różnica wynika m.in. z przybliżonych udziałów oraz z tego, że rzeczywiste masy izotopów nie są dokładnie równe ich liczbom masowym.' }
    ]},
    { kicker: '15 · Podsumowanie', title: 'Trzy liczby porządkują opis jądra', lead: 'Z określa pierwiastek, N liczbę neutronów, a A sumę nukleonów. Razem wyjaśniają zapis izotopu.', visual: 'conclusions', points: [
      { title: 'Jądro i nukleony', text: 'Jądro zawiera protony i neutrony; atom obojętny ma tyle elektronów, ile protonów.' },
      { title: 'Izotopy', text: 'Ten sam pierwiastek oznacza stałe Z, a izotopy różnią się liczbą neutronów i wartością A.' },
      { title: 'Dowody i oddziaływania', text: 'Rozpraszanie cząstek alfa odsłoniło dodatnie jądro. Krótkiego zasięgu siły jądrowe działają między nukleonami.' },
      { title: 'Pojęcia', text: 'Opis jądra wykorzystuje pojęcia: nukleon, izotop, liczba atomowa i liczba masowa; rozdział wprowadza też antymaterię, anihilację i kreację.' }
    ]},
    { kicker: '16 · Źródła', title: 'Materiały uzupełniające i atrybucje', lead: 'Treści tej prezentacji streszczono własnymi słowami na podstawie przekazanego fragmentu §18.1 oraz poniższych źródeł uzupełniających.', visual: 'references', points: []}
  ];

  const sources = [
    ['OpenStax · Properties of Nuclei', 'https://openstax.org/books/university-physics-volume-3/pages/10-1-properties-of-nuclei'],
    ['NIST/CODATA · Fundamental Physical Constants', 'https://www.nist.gov/pml/fundamental-physical-constants'],
    ['Nobel Prize · Ernest Rutherford', 'https://www.nobelprize.org/prizes/chemistry/1908/rutherford/biographical/'],
    ['CERN · The Standard Model', 'https://home.cern/science/physics/standard-model']
  ];

  /** @type {Record<number, string[][]>} */
  const slideSources = {
    0: [sources[0]], 1: [sources[0]], 2: [sources[0], sources[1]],
    3: [sources[0], sources[3]], 4: [sources[0]], 5: [sources[0]],
    6: [sources[0]], 7: [sources[0], sources[2]], 8: [sources[0], sources[2]],
    9: [sources[0], sources[1]], 10: [sources[0], sources[3]],
    11: [sources[0], sources[3]], 12: [sources[0]], 13: [sources[0], sources[1]],
    14: [sources[0], sources[1]], 15: [sources[0]]
  };
  const takeaways = [
    'W jądrze skupia się prawie cała masa atomu.',
    'Atom obojętny ma tyle samo protonów, co elektronów.',
    'Jądro jest około 100 000 razy mniejsze od atomu.',
    'Proton i neutron są ciężkie w porównaniu z elektronem.',
    'Ten sam pierwiastek oznacza tę samą liczbę protonów.',
    'Podobna konfiguracja elektronów oznacza podobną chemię.',
    'A = Z + N, więc N = A − Z.',
    'Rzadkie, duże odchylenia ujawniły małe jądro.',
    'Rozpraszanie to odpychanie elektrostatyczne, nie twarde zderzenie.',
    'Liczba masowa A nie jest masą atomową w u.',
    'Silne oddziaływanie wiąże bliskie nukleony.',
    'Proton i neutron są cząstkami złożonymi z kwarków.',
    'Anihilacja i kreacja zachowują energię oraz pęd.',
    'Przy tych samych T i p gęstość zależy od masy cząstek.',
    'Masa pierwiastka w tablicy jest średnią ważoną izotopów.',
    'Z określa pierwiastek; A i Z wyznaczają liczbę neutronów.'
  ];

  let active = 0;
  let tocOpen = false;
  let fullscreenError = '';
  let isotopeZ = 6;
  let isotopeA = 12;
  let touchStartX = 0;
  let touchStartY = 0;
  let touchIdentifier = -1;
  let touchCanNavigate = false;
  /** @type {HTMLElement | undefined} */
  let stageElement;
  /** @type {Record<number, string[]>} */
  const elements = { 1: ['H', 'wodór'], 2: ['He', 'hel'], 3: ['Li', 'lit'], 4: ['Be', 'beryl'], 5: ['B', 'bor'], 6: ['C', 'węgiel'], 7: ['N', 'azot'], 8: ['O', 'tlen'], 9: ['F', 'fluor'], 10: ['Ne', 'neon'], 11: ['Na', 'sód'], 12: ['Mg', 'magnez'], 13: ['Al', 'glin'], 14: ['Si', 'krzem'], 15: ['P', 'fosfor'], 16: ['S', 'siarka'], 17: ['Cl', 'chlor'], 18: ['Ar', 'argon'], 19: ['K', 'potas'], 20: ['Ca', 'wapń'], 26: ['Fe', 'żelazo'], 92: ['U', 'uran'] };
  /** @param {number} z */
  const symbolFor = (z) => elements[z]?.[0] ?? 'X';
  /** @param {number} z */
  const nameFor = (z) => elements[z]?.[1] ?? 'pierwiastek';
  $: isotopeNeutrons = isotopeA - isotopeZ;
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
    if (event.defaultPrevented || event.repeat || event.altKey || event.ctrlKey || event.metaKey) return;
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
    if (event.touches.length !== 1) {
      touchCancel();
      return;
    }
    const touch = event.changedTouches[0];
    if (!touch) return;
    const target = event.target;
    touchCanNavigate = target instanceof Element
      && target.closest('.stage') !== null
      && target.closest('button, input, textarea, select, a, [role="slider"]') === null;
    touchIdentifier = touch.identifier;
    touchStartX = touch.clientX;
    touchStartY = touch.clientY;
  }
  /** @param {TouchEvent} event */
  function touchEnd(event) {
    const touch = Array.from(event.changedTouches).find((item) => item.identifier === touchIdentifier);
    if (!touch) return;
    const canNavigate = touchCanNavigate;
    touchCanNavigate = false;
    touchIdentifier = -1;
    if (!canNavigate) return;
    const dx = touch.clientX - touchStartX;
    const dy = touch.clientY - touchStartY;
    if (Math.abs(dx) > 65 && Math.abs(dx) > Math.abs(dy) * 1.3) dx < 0 ? next() : previous();
  }
  function touchCancel() {
    touchCanNavigate = false;
    touchIdentifier = -1;
  }
</script>

<svelte:window onkeydown={handleKeydown} />

<div class="presentation" role="region" aria-label="Prezentacja o jądrze atomowym" ontouchstart={touchStart} ontouchend={touchEnd} ontouchcancel={touchCancel}>
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
    <section class:hero-slide={active === 0} class:conclusions-slide={slide.visual === 'conclusions'} class:references-slide={slide.visual === 'references'} class={`slide slide-${slide.visual}`} aria-labelledby="slide-title">
      <div class="slide-heading">
        <div class="heading-copy">
          <div class="eyebrow"><span class="eyebrow-line"></span>{slide.kicker}</div>
          <h1 id="slide-title">{slide.title}</h1>
          <p class="lead">{slide.lead}</p>
        </div>
      </div>

      <div class="lesson-layout">
        <figure class="visual-panel">
          <figcaption class="visual-label"><span>MODEL / SCHEMAT</span><span>{String(active + 1).padStart(2, '0')} — {String(slides.length).padStart(2, '0')}</span></figcaption>
          <div class="visual-body">
            {#if slide.visual === 'hero-composition'}
              <div class="hero-atom-map" role="img" aria-label="Schemat obojętnego atomu helu-4: jądro z dwóch czerwonych protonów i dwóch turkusowych neutronów, otoczone umownym obszarem elektronów oraz dwoma jasnymi elektronami">
                <div class="hero-atom-cloud" aria-hidden="true"></div>
                <span class="hero-electron hero-electron-a">e⁻</span><span class="hero-electron hero-electron-b">e⁻</span>
                <div class="hero-nucleus">
                  <b class="particle-proton">p⁺</b><b class="particle-neutron">n⁰</b>
                  <b class="particle-neutron">n⁰</b><b class="particle-proton">p⁺</b>
                </div>
                <div class="hero-label hero-label-nucleus"><b>JĄDRO · ⁴He</b><span>2 p⁺ + 2 n⁰<br />prawie cała masa</span></div>
                <div class="hero-label hero-label-electrons"><b>2 e⁻</b><span>poza jądrem<br />chmura: możliwe położenia</span></div>
                <small class="hero-map-caveat">Schemat budowy · rozmiary i położenia umowne, nie w skali</small>
              </div>
            {:else if slide.visual === 'electron-cloud'}
              <AtomModel />
            {:else if slide.visual === 'scale'}
              <div class="scale-sketch">
                <div class="scale-atom" aria-hidden="true"><div class="scale-cloud"></div><div class="scale-nucleus"></div><span class="scale-orbit-label">granica umownego rozmiaru atomu</span></div>
                <div class="scale-labels"><b>ATOM <span>≈ 10⁻¹⁰ m</span></b><i class="scale-ratio"><strong>100 000×</strong><small>różnicy w rozmiarze liniowym</small></i><b>JĄDRO <span>≈ 10⁻¹⁵ m</span></b><small>Schemat rozmiarów, nie w skali.</small></div>
              </div>
            {:else if slide.visual === 'particle-properties'}
              <div class="particle-properties" role="img" aria-label="Porównanie ładunków i mas protonu, neutronu i elektronu: proton +e, neutron 0, elektron −e; proton i neutron mają masy około 1,67 razy 10 do minus 27 kilograma, elektron około 9,11 razy 10 do minus 31 kilograma">
                <div class="particle-property proton-property"><i class="particle-icon proton-icon">p⁺</i><b>PROTON</b><span>ładunek +e</span><strong>1,6726 · 10⁻²⁷ kg</strong><small>jądro · nukleon</small></div>
                <div class="particle-property neutron-property"><i class="particle-icon neutron-icon">n⁰</i><b>NEUTRON</b><span>ładunek 0</span><strong>1,6749 · 10⁻²⁷ kg</strong><small>jądro · nukleon</small></div>
                <div class="particle-property electron-property"><i class="particle-icon electron-icon">e⁻</i><b>ELEKTRON</b><span>ładunek −e</span><strong>9,109 · 10⁻³¹ kg</strong><small>poza jądrem</small></div>
                <div class="mass-comparison"><span>Proton i neutron mają niemal takie same masy.</span><b>Elektron jest ok. 1836× lżejszy od protonu.</b></div>
              </div>
            {:else if slide.visual === 'notation'}
              <div class="notation-demo">
                <div class="nuclide"><sup>{isotopeA}</sup><sub>{isotopeZ}</sub>{symbolFor(isotopeZ)}</div>
                <div class="notation-key"><span><b class="mass-mark">A</b> protony + neutrony</span><span><b class="proton-mark">Z</b> protony</span><span><b class="neutron-mark">N</b> {isotopeA} − {isotopeZ} = {isotopeNeutrons}</span></div>
                <label for="protons">Z · protony <output>{isotopeZ} · {nameFor(isotopeZ)}</output></label><input id="protons" type="range" min="1" max="20" value={isotopeZ} oninput={changeZ} />
                <label for="mass-number">A · liczba nukleonów <output>{isotopeA}</output></label><input id="mass-number" type="range" min={isotopeZ} max="40" value={isotopeA} oninput={(event) => isotopeA = Number(event.currentTarget.value)} />
              </div>
            {:else if slide.visual === 'isotopes'}
              <div class="isotope-compare">
                <div><strong>¹H</strong><span>1 p · 0 n · 1 e⁻</span><div class="isotope-atom"><i class="nucleus tiny"><b class="particle-proton">p⁺</b></i><i class="isotope-electron">e⁻</i></div></div><div class="same-z">TEN SAM Z = 1</div><div><strong>²H</strong><span>1 p · 1 n · 1 e⁻</span><div class="isotope-atom"><i class="nucleus"><b class="particle-proton">p⁺</b><b class="particle-neutron">n⁰</b></i><i class="isotope-electron">e⁻</i></div></div><div><strong>³H</strong><span>1 p · 2 n · 1 e⁻</span><div class="isotope-atom"><i class="nucleus"><b class="particle-proton">p⁺</b><b class="particle-neutron">n⁰</b><b class="particle-neutron">n⁰</b></i><i class="isotope-electron">e⁻</i></div></div>
                <small class="diagram-caveat">Elektron e⁻ ma ten sam ładunek i liczbę w każdym atomie obojętnym · schemat, nie w skali.</small>
              </div>
            {:else if slide.visual === 'families'}
              <div class="isotope-chem">
                <div class="isotope-chem-row"><b>¹²₆C</b><span><i class="particle-count particle-proton">6 p⁺</i><i class="particle-count particle-neutron">6 n⁰</i><i class="particle-count particle-electron">6 e⁻</i></span></div>
                <i class="same-element">to samo Z = 6 → ten sam pierwiastek</i>
                <div class="isotope-chem-row"><b>¹⁴₆C</b><span><i class="particle-count particle-proton">6 p⁺</i><i class="particle-count particle-neutron">8 n⁰</i><i class="particle-count particle-electron">6 e⁻</i></span></div>
                <p>ta sama konfiguracja elektronów walencyjnych<strong>→</strong> podobne właściwości chemiczne</p>
              </div>
            {:else if slide.visual === 'scattering'}
              <div class="rutherford-diagram">
                <svg viewBox="0 0 760 470" role="img" aria-labelledby="rutherford-title rutherford-desc">
                  <title id="rutherford-title">Schemat doświadczenia Geigera i Marsdena</title>
                  <desc id="rutherford-desc">Źródło cząstek alfa w ołowianej osłonie wysyła wiązkę na cienką folię złota. Ekran scyntylacyjny wokół miejsca folii wykrywa cząstki, które przechodzą prosto lub zmieniają kierunek.</desc>
                  <defs>
                    <linearGradient id="lead-fill" x2="1" y2="1"><stop stop-color="#293743"/><stop offset="1" stop-color="#101c27"/></linearGradient>
                    <radialGradient id="foil-glow"><stop stop-color="#fff0b0"/><stop offset="1" stop-color="#e7a950"/></radialGradient>
                    <marker id="alpha-arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M 0 0 L 10 5 L 0 10 z" fill="#f3c66e"/></marker>
                  </defs>
                  <path class="detector-arc" d="M438 92 A190 190 0 0 1 438 378"/>
                  <path class="detector-tick" d="M490 128l17-11M527 185l20-4M530 280l20 4M490 342l17 11"/>
                  <text class="diagram-label" x="540" y="106">EKRAN</text><text class="diagram-sub" x="540" y="127">scyntylacyjny</text>
                  <rect x="36" y="169" width="145" height="132" rx="8" class="lead-block"/>
                  <circle cx="77" cy="235" r="20" class="source-core"/><text class="source-mark" x="77" y="241">α</text>
                  <rect x="130" y="218" width="64" height="34" rx="4" class="collimator"/>
                  <text class="diagram-label" x="40" y="333">ŹRÓDŁO</text><text class="diagram-sub" x="40" y="353">cząstek α</text>
                  <text class="diagram-label" x="131" y="281">OŁÓW</text>
                  <path class="alpha-path alpha-straight" d="M194 235 L560 235" marker-end="url(#alpha-arrow)"/>
                  <path class="alpha-path alpha-small" d="M330 235 Q415 232 500 165" marker-end="url(#alpha-arrow)"/>
                  <path class="alpha-path alpha-back" d="M330 235 Q264 222 205 183" marker-end="url(#alpha-arrow)"/>
                  <circle class="animated-alpha" r="6"><animateMotion dur="3.2s" repeatCount="indefinite" path="M194 235 L560 235"/></circle>
                  <circle class="animated-alpha delayed" r="5"><animateMotion dur="4.3s" begin="-1.7s" repeatCount="indefinite" path="M330 235 Q415 232 500 165"/></circle>
                  <rect x="320" y="168" width="18" height="134" rx="3" class="gold-foil"/>
                  <circle cx="329" cy="235" r="12" class="foil-target"/>
                  <text class="diagram-label" x="274" y="330">FOLIA Au</text><text class="diagram-sub" x="255" y="351">cienka · schemat</text>
                  <text class="trajectory-note" x="365" y="274">większość</text><text class="trajectory-note" x="365" y="293">przechodzi</text>
                  <text class="trajectory-note rare" x="397" y="146">rzadkie silne</text><text class="trajectory-note rare" x="413" y="164">odchylenia</text>
                </svg>
                <p><span>SCHEMAT, NIE W SKALI</span><span>Jądro odpycha cząstki α elektrostatycznie</span></p>
              </div>
            {:else if slide.visual === 'deflection'}
              <div class="deflection-diagram" role="img" aria-label="Trzy dodatnio naładowane cząstki alfa mijają dodatnie jądro: daleka zmienia tor mało, bliska mocno, a bardzo bliska zawraca wskutek odpychania elektrostatycznego">
                <div class="deflection-nucleus"><b>Au</b><span>jądro<br />dodatnie</span></div>
                <svg viewBox="0 0 640 360" aria-hidden="true">
                  <defs><marker id="deflection-arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0 0L10 5L0 10z" fill="#ff806d"/></marker></defs>
                  <path class="deflect-path far" d="M24 72 C220 72 368 82 610 92" marker-end="url(#deflection-arrow)"/>
                  <path class="deflect-path near" d="M24 180 C216 180 295 130 382 92 C454 62 530 52 610 48" marker-end="url(#deflection-arrow)"/>
                  <path class="deflect-path close" d="M24 288 C182 288 263 276 303 242 C340 211 335 172 306 151 C279 131 240 133 210 149" marker-end="url(#deflection-arrow)"/>
                  <circle class="alpha-marker far-marker" cx="88" cy="72" r="10"/><circle class="alpha-marker near-marker" cx="150" cy="180" r="10"/><circle class="alpha-marker close-marker" cx="130" cy="288" r="10"/>
                  <path class="coulomb-arrow" d="M224 176L278 156"/><path class="coulomb-arrow" d="M226 283L270 262"/>
                </svg>
                <div class="deflection-label label-far"><b>Dalek przelot</b><span>małe odchylenie</span></div>
                <div class="deflection-label label-near"><b>Bliski przelot</b><span>silne odchylenie</span></div>
                <div class="deflection-label label-close"><b>Bardzo blisko</b><span>cząstka zawraca</span></div>
                <p class="diagram-caveat">α: jądro helu-4 (+2e) · tory schematyczne · nie zderzenie z twardą kulką</p>
              </div>
            {:else if slide.visual === 'quarks'}
              <div class="quark-comparison" role="img" aria-label="Proton złożony z dwóch kwarków górnych u o ładunku plus dwie trzecie e i jednego kwarku dolnego d o ładunku minus jedna trzecia e; neutron z jednego u i dwóch d">
                <div class="quark-hadron proton-hadron">
                  <div class="hadron-heading"><b>PROTON p⁺</b><span>ładunek całkowity +e</span></div>
                  <div class="quark-triplet"><i class="quark-up">u<small>+⅔e</small></i><i class="quark-up">u<small>+⅔e</small></i><i class="quark-down">d<small>−⅓e</small></i></div>
                  <p>u + u + d → +1e</p>
                </div>
                <div class="quark-hadron neutron-hadron">
                  <div class="hadron-heading"><b>NEUTRON n⁰</b><span>ładunek całkowity 0</span></div>
                  <div class="quark-triplet"><i class="quark-up">u<small>+⅔e</small></i><i class="quark-down">d<small>−⅓e</small></i><i class="quark-down">d<small>−⅓e</small></i></div>
                  <p>u + d + d → 0</p>
                </div>
                <div class="gluon-note"><i aria-hidden="true">〰</i> gluony przenoszą oddziaływanie silne i wiążą kwarki</div>
                <small class="diagram-caveat">Schemat składu kwarkowego · kwarki nie występują jako swobodne cząstki</small>
              </div>
            {:else if slide.visual === 'forces'}
              <div class="force-diagram">
                <div class="force-interaction"><div class="force-pair"><span class="proton-ball">p⁺</span><b>↔</b><span class="proton-ball">p⁺</span></div><p class="force-repel">protony odpychają się elektrycznie</p></div>
                <div class="force-interaction"><div class="force-pair"><span class="proton-ball">p⁺</span><b>≈</b><span class="neutron-ball">n⁰</span></div><p class="force-bind">bliskie nukleony przyciągają siły jądrowe</p></div>
                <div class="range-scale">odpychanie: daleki zasięg <i></i> wiązanie jądra: kilka fm</div>
                <small class="diagram-caveat">Uproszczony schemat oddziaływań, nie obraz rzeczywistych torów.</small>
              </div>
            {:else if slide.visual === 'atomic-mass'}
              <div class="atomic-mass-visual"><div><span>¹²C</span><b>A = 12</b><small>nukleony w jednym jądrze</small></div><i>≠</i><div><span>Cu</span><b>≈ 63,55 u</b><small>średnia mas naturalnych izotopów</small></div></div>
            {:else if slide.visual === 'chlorine-average'}
              <div class="chlorine-average"><div><span><b>³⁵Cl</b><i style="--fraction: 76%"></i><small>76%</small></span><span><b>³⁷Cl</b><i style="--fraction: 24%"></i><small>24%</small></span></div><p>0,76 · 35 + 0,24 · 37</p><strong>35,48</strong><small>średnia liczb masowych; udziały atomów · tablicowa masa atomowa: 35,45 u</small></div>
            {:else if slide.visual === 'antimatter'}
              <div class="antimatter-visual"><div class="particle-pair"><span class="electron-particle">e⁻<small>elektron</small></span><b>+</b><span class="positron-particle">e⁺<small>pozyton</small></span></div><i>anihilacja</i><div class="photon-pair"><b>γ</b><span>fotony</span><b>γ</b></div><small>energia i pęd układu są zachowane</small></div>
            {:else if slide.visual === 'density-worked'}
              <div class="density-worked"><div><b>H₂</b><span>2 nukleony</span></div><i>masa cząstek · te same T i p</i><div><b>He</b><span>4 nukleony</span></div><strong>ρ(He) / ρ(H₂) ≈ 4 / 2 ≈ 2</strong><small>Tablice: ρHe = 0,164 kg/m³; ρH₂ = 0,0823 kg/m³ → 1,993</small></div>
            {:else if slide.visual === 'conclusions'}
              <div class="conclusion-map" aria-label="Od składu atomu przez obserwacje do opisu jądra">
                <div><b>01</b><span>protony<br />i neutrony</span></div><i>→</i><div><b>02</b><span>izotopy<br />i zapis Z, A</span></div><i>→</i><div><b>03</b><span>doświadczenie<br />Rutherforda</span></div><i>→</i><div><b>04</b><span>oddziaływania<br />jądrowe</span></div>
              </div>
            {:else}
              <div class="reference-lead"><b>Materiały źródłowe</b><span>Przekazany fragment §18.1 · OpenStax · NIST/CODATA · Nobel Prize</span><small>Treść fragmentu streszczono własnymi słowami; pełne odnośniki i atrybucje po prawej.</small></div>
            {/if}
          </div>
        </figure>

        <div class="explanation-panel">
          {#if slide.visual === 'notation'}<div class="definition-strip"><b>Przeczytaj:</b> ᴬ_ZX = nuklid o Z protonach i A−Z neutronach.</div>{/if}
          <div class="point-list">
            {#each slide.points as point, i}
              <article class="point"><span class="point-index">{String(i + 1).padStart(2, '0')}</span><div><h2>{point.title}</h2><p>{point.text}</p></div></article>
            {/each}
          </div>
          {#if slide.visual !== 'references'}
            <aside class="takeaway">
              <span>SEDNO</span>
              <p>{takeaways[active]}</p>
            </aside>
          {/if}
          {#if slideSources[active]}
            <p class="slide-citation">Źródła: {#each slideSources[active] as source, i}{#if i},&nbsp;{/if}<a href={source[1]} target="_blank" rel="noreferrer">{source[0]}</a>{/each}</p>
          {/if}
          {#if slide.visual === 'references'}
            <div class="source-links"><h2>Źródła merytoryczne</h2><ul>{#each sources as source}<li><a href={source[1]} target="_blank" rel="noreferrer">{source[0]} ↗</a></li>{/each}</ul></div>
            <div class="image-credits"><b>Atrybucja ilustracji</b><ul>
              <li>Diagramy doświadczenia i budowy atomu są autorskimi schematami edukacyjnymi; nie przedstawiają fotografii ani układów w skali.</li>
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
    <div class="footer-controls"><div class="nav-buttons"><button class="nav-arrow" onclick={previous} disabled={active === 0} aria-label="Poprzedni slajd">←</button><button class="nav-arrow" onclick={next} disabled={active === slides.length - 1} aria-label="Następny slajd">→</button></div></div>
  </footer>

  {#if fullscreenError}<div class="toast" role="status">{fullscreenError}</div>{/if}
  {#if tocOpen}<div class="toc-backdrop" role="presentation" onclick={(event) => { if (event.target === event.currentTarget) tocOpen = false; }}><nav class="toc-panel" aria-label="Spis slajdów"><div class="toc-header"><div><span>NAWIGACJA</span><h2>Spis treści</h2></div><button class="icon-button" onclick={() => tocOpen = false} aria-label="Zamknij spis">×</button></div><ol>{#each slides as item, i}<li><button class:toc-current={active === i} onclick={() => goTo(i)}><span>{String(i + 1).padStart(2, '0')}</span><b>{item.title}</b><i>↗</i></button></li>{/each}</ol><p class="toc-help">Klawisze ← → · Home / End · Esc zamyka</p></nav></div>{/if}
</div>
