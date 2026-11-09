<script>
  import AtomModel from './AtomModel.svelte';
  import geigerMarsdenReconstruction from './assets/history/geiger-marsden-reconstruction.jpg';

  const slides = [
    { kicker: '18.1 · Jądro atomowe', title: 'Jądro jest małe, dodatnie i ciężkie', lead: 'Budowa atomu, izotopy i doświadczenie Rutherforda wyjaśniają skład oraz właściwości jądra.', visual: 'hero', points: [
      { title: 'Skład jądra', text: 'Jądro tworzą protony i neutrony, wspólnie nazywane nukleonami.' },
      { title: 'Odkrycie', text: 'Rozpraszanie cząstek alfa ujawniło, że dodatni ładunek i niemal cała masa atomu są skupione w małym jądrze.' }
    ]},
    { kicker: '01 · Przypomnienie', title: 'Atom składa się z jądra i otaczających go elektronów', lead: 'W tym temacie przenosimy uwagę z elektronów na budowę jądra atomowego.', visual: 'atom', points: [
      { title: 'Ładunki', text: 'Elektron ma ładunek −e, proton +e, a neutron nie ma ładunku elektrycznego. e = 1,6 · 10⁻¹⁹ C.' },
      { title: 'Atom obojętny', text: 'Liczba elektronów jest równa liczbie protonów, więc ładunki atomu się równoważą.' },
      { title: 'Jądro', text: 'Jądro jest zbudowane z protonów i neutronów. Skupia prawie całą masę atomu.' }
    ]},
    { kicker: '02 · Rozmiar i masa', title: 'Niewielkie jądro skupia niemal całą masę atomu', lead: 'Większość objętości atomu zajmuje przestrzeń wokół jądra, ale prawie cała jego masa znajduje się w jądrze.', visual: 'scale', points: [
      { title: 'Mały rozmiar', text: 'Jądro zajmuje bardzo małą objętość w porównaniu z całym atomem.' },
      { title: 'Masy składników', text: 'Proton i neutron mają zbliżone masy. Elektron jest od każdego z nich około 2000 razy lżejszy.' },
      { title: 'Wniosek', text: 'To nukleony, a nie elektrony, odpowiadają za niemal całą masę atomu.' }
    ]},
    { kicker: '03 · Nukleony', title: 'Protony i neutrony to nukleony', lead: 'Obie cząstki wchodzą w skład jądra i mają masy zbliżone do atomowej jednostki masy.', visual: 'nucleons', points: [
      { title: 'Proton', text: 'Ma ładunek +e i masę około 1,6726 · 10⁻²⁷ kg.' },
      { title: 'Neutron', text: 'Jest elektrycznie obojętny, a jego masa wynosi około 1,6749 · 10⁻²⁷ kg.' },
      { title: 'Elektron', text: 'Ma ładunek −e i masę około 2000 razy mniejszą niż nukleon.' }
    ]},
    { kicker: '04 · Izotopy', title: 'Izotopy mają tyle samo protonów, ale różną liczbę neutronów', lead: 'Jądra atomów tego samego pierwiastka mają jednakowe Z, lecz mogą różnić się składem neutronowym.', visual: 'isotopes', points: [
      { title: 'Wodór w przyrodzie', text: 'Prot stanowi około 99,985% wodoru, deuter około 0,015%, a tryt występuje w ilościach śladowych.' },
      { title: 'Izotopy węgla', text: 'Węgiel-12 ma 6 protonów i 6 neutronów, a węgiel-14 — 6 protonów i 8 neutronów.' },
      { title: 'Węgiel w przyrodzie', text: 'Oba izotopy występują w atmosferycznym CO₂, trafiają do roślin podczas fotosyntezy, a następnie do łańcucha pokarmowego.' }
    ]},
    { kicker: '05 · Właściwości chemiczne', title: 'Izotopy tego samego pierwiastka reagują prawie tak samo', lead: 'Różnice liczby neutronów zmieniają jądro, ale nie zmieniają liczby protonów pierwiastka.', visual: 'families', points: [
      { title: 'To samo miejsce w układzie', text: 'Nazwa „izotop” nawiązuje do wspólnego miejsca pierwiastka w układzie okresowym: izotopy mają to samo Z.' },
      { title: 'Podobny układ elektronów', text: 'Ich konfiguracje elektronowe, w tym obsadzenie powłoki walencyjnej, są praktycznie jednakowe.' },
      { title: 'Skutek chemiczny', text: 'Ponieważ za właściwości chemiczne odpowiadają głównie elektrony walencyjne, izotopy reagują bardzo podobnie.' }
    ]},
    { kicker: '06 · Liczby Z i A', title: 'Liczby atomowa i masowa opisują skład jądra', lead: 'Zapis izotopu podaje symbol pierwiastka, liczbę protonów oraz łączną liczbę nukleonów.', visual: 'notation', points: [
      { title: 'Liczba atomowa Z', text: 'To liczba protonów w jądrze; określa pierwiastek i jego numer w układzie okresowym. Ładunek jądra to +Ze.' },
      { title: 'Liczba masowa A', text: 'To suma protonów i neutronów. Liczbę neutronów obliczamy: N = A − Z.' },
      { title: 'Przykład węgla-14', text: '¹⁴₆C ma Z = 6 protonów oraz A = 14 nukleonów, więc N = 14 − 6 = 8 neutronów. Ładunek jądra wynosi +6e.' }
    ]},
    { kicker: '07 · Doświadczenie', title: 'Rozpraszanie cząstek alfa zmieniło model atomu', lead: 'Wyniki Geigera i Marsdena doprowadziły Rutherforda do nowego opisu budowy atomu, opublikowanego w 1911 roku.', visual: 'scattering', points: [
      { title: 'Wcześniejszy pogląd', text: 'W modelu Thomsona ładunek dodatni był rozłożony w całej objętości atomu, a elektrony znajdowały się wewnątrz tej masy.' },
      { title: 'Układ doświadczenia', text: 'Strumień cząstek alfa, czyli jąder helu, kierowano na bardzo cienką złotą folię; ekran wykrywał cząstki po przejściu przez folię.' },
      { title: 'Obserwacje', text: 'Zdecydowana większość cząstek przechodziła prawie prosto, lecz nieliczne odchylały się silnie, a niektóre zawracały.' }
    ]},
    { kicker: '08 · Odkrycie jądra', title: 'Silne odchylenia ujawniły małe, dodatnie jądro', lead: 'Wyniki rozpraszania nie pasowały do ładunku dodatniego rozłożonego równomiernie w atomie.', visual: 'atom', points: [
      { title: 'Większość torów', text: 'Prawie niezmieniony kierunek większości cząstek wskazywał, że w atomie dużo przestrzeni nie stanowi zwartej przeszkody.' },
      { title: 'Rzadkie odbicia', text: 'Silne odchylenia, także bliskie 180°, wynikały z odpychania Coulombowskiego cząstek alfa w pobliżu małego, dodatniego jądra.' },
      { title: 'Nowy obraz atomu', text: 'Dodatni ładunek i prawie cała masa są skupione w jądrze; elektrony znajdują się wokół niego.' }
    ]},
    { kicker: '09 · Masa atomowa', title: 'Liczba masowa to nie to samo co masa atomowa', lead: 'A jest całkowitą liczbą nukleonów, natomiast masa atomowa uwzględnia rzeczywistą masę atomu i występowanie jego izotopów.', visual: 'atomic-mass', points: [
      { title: 'Jednostka u', text: 'Jednostkę masy atomowej zdefiniowano jako 1/12 masy obojętnego atomu węgla-12. 1 u ≈ 1,6605 · 10⁻²⁷ kg.' },
      { title: 'Masa nukleonu', text: 'Masy protonu i neutronu różnią się od 1 u o mniej niż 1%; elektron wnosi niewielki wkład do masy atomu.' },
      { title: 'Średnia izotopowa', text: 'Masa podana w układzie okresowym jest średnią ważoną mas izotopów. Miedź ma masę około 63,54 u; jej częste izotopy to ⁶³Cu i ⁶⁵Cu, przy czym drugi stanowi około 30%.' }
    ]},
    { kicker: '10 · Oddziaływania jądrowe', title: 'Bliskie nukleony przyciągają siły jądrowe', lead: 'Odpychanie elektryczne protonów jest równoważone przez krótkiego zasięgu oddziaływanie między nukleonami.', visual: 'forces', points: [
      { title: 'Odpychanie elektryczne', text: 'Każdy proton ma ładunek dodatni, dlatego protony odpychają się na dużych odległościach.' },
      { title: 'Przyciąganie jądrowe', text: 'Siły jądrowe działają między protonami i neutronami oraz między samymi neutronami, ale tylko wtedy, gdy nukleony są blisko.' },
      { title: 'Ciężkie jądra', text: 'W bardzo dużym jądrze wiele protonów odpycha się, a nukleony odległe od siebie nie wzmacniają wiązania krótkiego zasięgu. Takie jądra mogą rozpadać się samorzutnie.' }
    ]},
    { kicker: '11 · Cząstki', title: 'Elektrony i fotony należą do cząstek elementarnych', lead: 'W szkolnym opisie mówi się o cząstkach elementarnych; dokładniejszy opis ujawnia także budowę nukleonów.', visual: 'nucleons', points: [
      { title: 'Termin w tym rozdziale', text: 'Do omawianych cząstek elementarnych zaliczamy elektrony, protony, neutrony i fotony.' },
      { title: 'Kwarki', text: 'Protony i neutrony składają się z kwarków, które nie występują jako swobodne cząstki; w dokładniejszym opisie nukleony mają więc wewnętrzną strukturę.' },
      { title: 'Fotony i neutrina', text: 'Światło składa się z fotonów; neutrino jest inną cząstką elementarną. W fizyce jądrowej symbolem γ oznacza się fotony o dowolnej energii.' }
    ]},
    { kicker: '12 · Materia i antymateria', title: 'Pozyton jest antycząstką elektronu', lead: 'Cząstki i antycząstki mają wiele cech wspólnych, lecz przeciwne ładunki elektryczne.', visual: 'antimatter', points: [
      { title: 'Antycząstka elektronu', text: 'Pozyton e⁺ ma taką samą masę jak elektron e⁻, ale ładunek +e. Foton jest własną antycząstką.' },
      { title: 'Anihilacja', text: 'Po spotkaniu elektronu z pozytonem powstają inne cząstki; przykładem jest e⁻ + e⁺ → 2γ.' },
      { title: 'Kreacja i asymetria', text: 'W pobliżu jądra wysokoenergetyczny foton może wytworzyć parę elektron–pozyton; jądro uczestniczy w bilansie pędu. Przewaga materii we Wszechświecie nadal nie ma pełnego wyjaśnienia.' }
    ]},
    { kicker: '13 · Przykład', title: 'Hel ma niemal dwukrotnie większą gęstość niż wodór', lead: 'Oszacowanie wykorzystuje izotopy najczęściej spotykane w przyrodzie i jednakową objętość molową gazów.', visual: 'density-worked', points: [
      { title: 'Wodór', text: 'Wodór występuje głównie jako H₂ złożony z dwóch atomów izotopu ¹H; masa cząsteczki jest w przybliżeniu równa masie dwóch nukleonów.' },
      { title: 'Hel', text: 'Hel jest gazem jednoatomowym, a jego atomy to niemal wyłącznie ⁴He — około cztery nukleony na atom.' },
      { title: 'Wynik', text: 'Równe objętości zawierają tyle samo moli cząstek, więc hel ma w przybliżeniu dwukrotnie większą gęstość. Dane tablicowe dają stosunek około 1,993.' }
    ]},
    { kicker: '14 · Średnia masa atomowa', title: 'Masa atomowa uwzględnia naturalne udziały izotopów', lead: 'W układzie okresowym podana jest średnia ważona mas izotopów danego pierwiastka.', visual: 'chlorine-average', points: [
      { title: 'Chlor w przyrodzie', text: 'Naturalny chlor zawiera izotopy ³⁵Cl i ³⁷Cl; w podanym przybliżeniu ich udziały wynoszą odpowiednio 76% i 24%.' },
      { title: 'Średnia liczb masowych', text: 'Dla tych udziałów średnia ważona wynosi 0,76 · 35 + 0,24 · 37 = 35,48.' },
      { title: 'Porównanie z tablicami', text: 'Masa atomowa chloru to około 35,45 u. Różnica wynika m.in. z przybliżonych udziałów oraz z tego, że rzeczywiste masy izotopów nie są dokładnie równe ich liczbom masowym.' }
    ]},
    { kicker: '15 · Wnioski', title: 'Z i A opisują jądro, a doświadczenie wyjaśnia jego rolę', lead: 'Skład jądra oraz różnice między liczbą masową i średnią masą atomową porządkują opis izotopów.', visual: 'conclusions', points: [
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
    ['Nobel Prize · Ernest Rutherford', 'https://www.nobelprize.org/prizes/chemistry/1908/rutherford/biographical/']
  ];

  /** @type {Record<number, string[][]>} */
  const slideSources = {
    1: [sources[0]], 2: [sources[0]], 3: [sources[0], sources[1]],
    4: [sources[0]], 5: [sources[0]], 6: [sources[0]],
    7: [sources[0], sources[2]], 8: [sources[0], sources[2]],
    9: [sources[0], sources[1]], 10: [sources[0]], 11: [sources[0]],
    12: [sources[0]], 13: [sources[0], sources[1]]
  };

  let active = 0;
  let tocOpen = false;
  let fullscreenError = '';
  let isotopeZ = 6;
  let isotopeA = 12;
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
              <div class="scale-sketch"><div class="scale-atom" aria-hidden="true"><div class="scale-cloud"></div><div class="scale-nucleus"></div></div><div class="scale-labels"><b>ATOM <span>elektrony</span></b><i>jądro zajmuje niewielką część atomu</i><b>JĄDRO <span>protony i neutrony</span></b><small>Schemat, nie w skali</small></div></div>
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
              <div class="isotope-chem"><div><b>¹²₆C</b><span>6 p · 6 n · 6 e⁻</span></div><i>ten sam Z = 6</i><div><b>¹⁴₆C</b><span>6 p · 8 n · 6 e⁻</span></div><p>jednakowy układ elektronów walencyjnych<br /><strong>→</strong> podobne właściwości chemiczne</p></div>
            {:else if slide.visual === 'scattering'}
              <div class="scattering-figure"><img src={geigerMarsdenReconstruction} alt="Współczesna rekonstrukcja CGI aparatury Geigera–Marsdena, nie fotografia z 1909 roku." /><div class="scatter-paths"><span class="straight">α → → →</span><span class="deflect">↗</span><span class="return">←</span><b>folia Au</b></div><p>większość prosto · nieliczne silne odchylenia</p></div>
            {:else if slide.visual === 'forces'}
              <div class="force-diagram"><div class="force-pair"><span>p⁺</span><span>p⁺</span><span>n⁰</span></div><div class="force-repel">← odpychanie Coulombowskie →</div><div class="force-bind">↔ przyciąganie silne blisko</div><div class="range-scale">daleki zasięg <i></i> krótki zasięg</div></div>
            {:else if slide.visual === 'atomic-mass'}
              <div class="atomic-mass-visual"><div><span>¹²C</span><b>A = 12</b><small>jedno jądro · liczba nukleonów</small></div><i>≠</i><div><span>Cu</span><b>≈ 63,54 u</b><small>średnia mas izotopów w naturze</small></div></div>
            {:else if slide.visual === 'chlorine-average'}
              <div class="chlorine-average"><div><span><b>³⁵Cl</b><i style="--fraction: 76%"></i><small>76%</small></span><span><b>³⁷Cl</b><i style="--fraction: 24%"></i><small>24%</small></span></div><p>0,76 · 35 + 0,24 · 37</p><strong>35,48</strong><small>średnia liczb masowych · tablicowa masa atomowa: 35,45 u</small></div>
            {:else if slide.visual === 'antimatter'}
              <div class="antimatter-visual"><div class="particle-pair"><span>e⁻<small>elektron</small></span><b>+</b><span>e⁺<small>pozyton</small></span></div><i>anihilacja</i><div class="photon-pair"><b>γ</b><span>fotony</span><b>γ</b></div><small>energia i pęd układu są zachowane</small></div>
            {:else if slide.visual === 'density-worked'}
              <div class="density-worked"><div><b>H₂</b><span>2 nukleony</span></div><i>masa cząstek · te same T i p</i><div><b>He</b><span>4 nukleony</span></div><strong>ρ(He) / ρ(H₂) ≈ 4 / 2 ≈ 2</strong><small>Tablice: 0,164 / 0,0823 ≈ 1,993</small></div>
            {:else if slide.visual === 'conclusions'}
              <div class="conclusion-map" aria-label="Od składu atomu przez obserwacje do opisu jądra">
                <div><b>01</b><span>protony<br />i neutrony</span></div><i>→</i><div><b>02</b><span>izotopy<br />i zapis Z, A</span></div><i>→</i><div><b>03</b><span>doświadczenie<br />Rutherforda</span></div><i>→</i><div><b>04</b><span>oddziaływania<br />jądrowe</span></div>
              </div>
            {:else}
              <div class="reference-lead"><b>Materiały źródłowe</b><span>Przekazany fragment §18.1 · OpenStax · NIST/CODATA · Nobel Prize</span><small>Treść fragmentu streszczono własnymi słowami; pełne odnośniki i atrybucje po prawej.</small></div>
            {/if}
          </div>
          {#if slide.visual === 'scattering'}<figcaption class="figure-credit">Współczesna rekonstrukcja CGI (nie oryginalna aparatura): <a href="https://commons.wikimedia.org/wiki/File:Geiger-Marsden_apparatus_2_CGI_mock-up.jpg" target="_blank" rel="noreferrer">Kurzon · CC BY 4.0 · Wikimedia Commons ↗</a></figcaption>{/if}
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
            <div class="image-credits"><b>Atrybucja ilustracji</b><ul>
              <li>Rekonstrukcja Geigera–Marsdena · Kurzon, CC BY 4.0 · <a href="https://commons.wikimedia.org/wiki/File:Geiger-Marsden_apparatus_2_CGI_mock-up.jpg" target="_blank" rel="noreferrer">Wikimedia Commons</a></li>
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
