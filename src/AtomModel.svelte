<script>
  import { onMount } from 'svelte';
  import * as THREE from 'three';

  /** @type {'quantum' | 'illustrative'} */
  export let initialMode = 'quantum';
  /** @type {HTMLDivElement} */
  let mount;
  let renderError = '';
  let modelMode = initialMode;
  /** @type {(mode: 'quantum' | 'illustrative') => void} */
  let updateModel = () => {};

  /** @param {'quantum' | 'illustrative'} mode */
  function selectModel(mode) {
    modelMode = mode;
    updateModel(mode);
  }

  onMount(() => {
    let renderer;

    try {
      renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
    } catch (error) {
      console.error('Nie udało się uruchomić wizualizacji Three.js.', error);
      renderError = 'Przeglądarka nie obsługuje renderowania 3D.';
      return;
    }

    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(38, 1, 0.1, 40);
    camera.position.set(0, 0, 8.2);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, 2));
    renderer.setClearColor(0x000000, 0);
    renderer.outputColorSpace = THREE.SRGBColorSpace;
    renderer.toneMapping = THREE.ACESFilmicToneMapping;
    renderer.toneMappingExposure = 1.35;
    mount.appendChild(renderer.domElement);

    const atom = new THREE.Group();
    scene.add(atom);
    scene.add(new THREE.AmbientLight(0xb9e8ed, 1.35));

    const keyLight = new THREE.PointLight(0xffc98f, 27, 24);
    keyLight.position.set(-3.5, 3.5, 5);
    scene.add(keyLight);

    const fillLight = new THREE.PointLight(0x55d6d1, 18, 22);
    fillLight.position.set(4, -2, -3);
    scene.add(fillLight);

    const nucleons = new THREE.Group();
    atom.add(nucleons);
    const nucleonGeometry = new THREE.SphereGeometry(0.29, 32, 24);
    const protonMaterial = new THREE.MeshStandardMaterial({
      color: 0xff806d,
      emissive: 0x7d261c,
      emissiveIntensity: 0.35,
      roughness: 0.32,
      metalness: 0.08
    });
    const neutronMaterial = new THREE.MeshStandardMaterial({
      color: 0x65d8d1,
      emissive: 0x145653,
      emissiveIntensity: 0.3,
      roughness: 0.36,
      metalness: 0.08
    });

    const hydrogenProton = new THREE.Mesh(nucleonGeometry, protonMaterial);
    nucleons.add(hydrogenProton);

    const heliumNucleus = new THREE.Group();
    /** @type {Array<{position: [number, number, number], material: THREE.MeshStandardMaterial}>} */
    const heliumNucleons = [
      { position: [-0.35, 0.35, 0.15], material: protonMaterial },
      { position: [0.35, 0.35, -0.15], material: protonMaterial },
      { position: [-0.35, -0.35, -0.15], material: neutronMaterial },
      { position: [0.35, -0.35, 0.15], material: neutronMaterial }
    ];
    for (const nucleon of heliumNucleons) {
      const sphere = new THREE.Mesh(nucleonGeometry, nucleon.material);
      sphere.position.set(...nucleon.position);
      heliumNucleus.add(sphere);
    }
    atom.add(heliumNucleus);

    const cloudCount = 18000;
    const cloudPositions = new Float32Array(cloudCount * 3);
    const cloudColors = new Float32Array(cloudCount * 3);
    const innerColor = new THREE.Color(0x90eee3);
    const outerColor = new THREE.Color(0x528cf0);
    const bohrRadius = 1.1;

    for (let i = 0; i < cloudCount; i += 1) {
      const offset = i * 3;
      const radius = -Math.log(Math.random() * Math.random() * Math.random()) * bohrRadius / 2;
      const z = Math.random() * 2 - 1;
      const angle = Math.random() * Math.PI * 2;
      const spread = Math.sqrt(1 - z * z);

      cloudPositions[offset] = radius * spread * Math.cos(angle);
      cloudPositions[offset + 1] = radius * spread * Math.sin(angle);
      cloudPositions[offset + 2] = radius * z;

      const color = innerColor.clone().lerp(outerColor, Math.min(radius / 3.2, 1));
      cloudColors[offset] = color.r;
      cloudColors[offset + 1] = color.g;
      cloudColors[offset + 2] = color.b;
    }

    const cloudGeometry = new THREE.BufferGeometry();
    cloudGeometry.setAttribute('position', new THREE.BufferAttribute(cloudPositions, 3));
    cloudGeometry.setAttribute('color', new THREE.BufferAttribute(cloudColors, 3));
    const cloud = new THREE.Points(
      cloudGeometry,
      new THREE.PointsMaterial({
        size: 0.06,
        sizeAttenuation: true,
        vertexColors: true,
        transparent: true,
        opacity: 0.36,
        depthWrite: false,
        blending: THREE.AdditiveBlending
      })
    );
    atom.add(cloud);

    const electronMaterial = new THREE.MeshBasicMaterial({
      color: 0xf2fff9,
      blending: THREE.AdditiveBlending
    });
    const electronGeometry = new THREE.SphereGeometry(0.13, 24, 16);
    const electronHaloMaterial = new THREE.MeshBasicMaterial({
      color: 0x79ffe9,
      transparent: true,
      opacity: 0.3,
      depthWrite: false,
      blending: THREE.AdditiveBlending
    });
    const electronHaloGeometry = new THREE.SphereGeometry(0.25, 24, 16);
    const electron = new THREE.Group();
    electron.add(new THREE.Mesh(electronHaloGeometry, electronHaloMaterial));
    electron.add(new THREE.Mesh(electronGeometry, electronMaterial));
    electron.add(new THREE.PointLight(0x9bffe9, 3.2, 2));
    atom.add(electron);

    const heliumElectrons = new THREE.Group();
    /** @type {Array<[number, number, number]>} */
    const heliumElectronPositions = [[-2.25, 0.65, 0.25], [2.25, -0.65, -0.25]];
    for (const position of heliumElectronPositions) {
      const marker = new THREE.Group();
      marker.position.set(...position);
      marker.add(new THREE.Mesh(electronHaloGeometry, electronHaloMaterial));
      marker.add(new THREE.Mesh(electronGeometry, electronMaterial));
      heliumElectrons.add(marker);
    }
    heliumNucleus.add(heliumElectrons);

    const heliumCloudCount = 10000;
    const heliumCloudPositions = new Float32Array(heliumCloudCount * 3);
    for (let i = 0; i < heliumCloudCount; i += 1) {
      const offset = i * 3;
      const radius = 1.8 * Math.cbrt(Math.random());
      const z = Math.random() * 2 - 1;
      const angle = Math.random() * Math.PI * 2;
      const spread = Math.sqrt(1 - z * z);
      heliumCloudPositions[offset] = radius * spread * Math.cos(angle);
      heliumCloudPositions[offset + 1] = radius * spread * Math.sin(angle);
      heliumCloudPositions[offset + 2] = radius * z;
    }
    const heliumCloudGeometry = new THREE.BufferGeometry();
    heliumCloudGeometry.setAttribute('position', new THREE.BufferAttribute(heliumCloudPositions, 3));
    const heliumCloud = new THREE.Points(
      heliumCloudGeometry,
      new THREE.PointsMaterial({
        color: 0x79ffe9,
        size: 0.04,
        sizeAttenuation: true,
        transparent: true,
        opacity: 0.25,
        depthWrite: false
      })
    );
    atom.add(heliumCloud);

    updateModel = (mode) => {
      const isQuantum = mode === 'quantum';
      cloud.visible = isQuantum;
      electron.visible = isQuantum;
      heliumCloud.visible = !isQuantum;
      heliumElectrons.visible = !isQuantum;
      hydrogenProton.visible = isQuantum;
      heliumNucleus.visible = !isQuantum;
      renderer.render(scene, camera);
    };
    updateModel(modelMode);

    const resize = () => {
      const width = mount.clientWidth;
      const height = mount.clientHeight;
      if (!width || !height) return;
      camera.aspect = width / height;
      camera.updateProjectionMatrix();
      renderer.setSize(width, height, false);
      renderer.render(scene, camera);
    };

    const resizeObserver = new ResizeObserver(resize);
    resizeObserver.observe(mount);
    resize();

    /** @type {number | undefined} */
    let frameId;
    const reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;
    let lastMeasurement = 0;
    const setQuantumMeasurement = () => {
      const radius = -Math.log(Math.random() * Math.random() * Math.random()) * bohrRadius / 2;
      const z = Math.random() * 2 - 1;
      const angle = Math.random() * Math.PI * 2;
      const spread = Math.sqrt(1 - z * z);
      electron.position.set(
        radius * spread * Math.cos(angle),
        radius * spread * Math.sin(angle),
        radius * z
      );
    };
    setQuantumMeasurement();
    const animate = () => {
      const now = performance.now();
      atom.rotation.y += 0.0007;
      atom.rotation.x = Math.sin(now * 0.0001) * 0.04;
      if (modelMode === 'quantum' && now - lastMeasurement > 900) {
        setQuantumMeasurement();
        lastMeasurement = now;
      }
      renderer.render(scene, camera);
      frameId = window.requestAnimationFrame(animate);
    };

    if (reduceMotion) {
      renderer.render(scene, camera);
    } else {
      frameId = window.requestAnimationFrame(animate);
    }

    return () => {
      if (frameId !== undefined) window.cancelAnimationFrame(frameId);
      resizeObserver.disconnect();
      updateModel = () => {};
      cloudGeometry.dispose();
      cloud.material.dispose();
      heliumCloudGeometry.dispose();
      heliumCloud.material.dispose();
      nucleonGeometry.dispose();
      protonMaterial.dispose();
      neutronMaterial.dispose();
      electronGeometry.dispose();
      electronMaterial.dispose();
      electronHaloGeometry.dispose();
      electronHaloMaterial.dispose();
      renderer.dispose();
      renderer.domElement.remove();
    };
  });
</script>

<div class="atom-visual">
  <div class="model-switch" role="group" aria-label="Wybierz model atomu">
    <button class:active={modelMode === 'quantum'} aria-pressed={modelMode === 'quantum'} onclick={() => selectModel('quantum')}>
      Wodór · 1s
    </button>
    <button class:active={modelMode === 'illustrative'} aria-pressed={modelMode === 'illustrative'} onclick={() => selectModel('illustrative')}>
      Hel-4 · schemat
    </button>
  </div>
  <div class="atom-canvas" bind:this={mount} aria-hidden="true"></div>
  <div class="atom-legend">
    {#if modelMode === 'quantum'}
      <span><i class="electron-cloud-key"></i>chmura: możliwe położenie e⁻</span>
      <span><i class="electron-key"></i>e⁻: przykładowy pomiar</span>
    {:else}
      <span><i class="electron-cloud-key"></i>umowny obszar 2 elektronów</span>
      <span><i class="electron-key"></i>e⁻: 2 elektrony, położenia umowne</span>
    {/if}
    <span><i class="proton-key"></i>p⁺: proton</span>
    {#if modelMode === 'illustrative'}
      <span><i class="neutron-key"></i>n⁰: neutron</span>
    {/if}
  </div>
  <div class="atom-caption">
    {#if modelMode === 'quantum'}
      <p>Wodór · stan 1s. Chmura pokazuje prawdopodobieństwo pomiaru e⁻.</p>
      <small>Jasny punkt to przykładowy wynik pomiaru, nie tor. Jądro powiększono; obraca się widok.</small>
    {:else}
      <p>Hel-4: 2 p⁺ + 2 n⁰ w jądrze oraz 2 e⁻ poza jądrem.</p>
      <small>Jasne znaczniki e⁻ są umowne, nie orbitami ani rzeczywistymi położeniami; jądro powiększono.</small>
    {/if}
  </div>
  {#if renderError}
    <p class="atom-error" role="status">{renderError}</p>
  {/if}
</div>

<style>
  .atom-visual {
    position: relative;
    width: 100%;
    height: clamp(310px, 42vh, 500px);
    min-height: 270px;
    overflow: hidden;
    border: 1px solid rgba(115, 204, 211, 0.2);
    border-radius: 20px;
    background:
      radial-gradient(ellipse at 50% 46%, rgba(32, 87, 107, 0.46), transparent 49%),
      linear-gradient(145deg, #0b1823, #112633 58%, #101a2d);
    box-shadow: inset 0 1px rgba(255, 255, 255, 0.06), 0 18px 48px rgba(15, 33, 45, 0.13);
  }

  .atom-canvas {
    position: absolute;
    inset: 44px 0 57px;
  }

  .model-switch {
    position: absolute;
    z-index: 1;
    top: 12px;
    right: 12px;
    display: flex;
    gap: 4px;
    padding: 3px;
    border: 1px solid rgba(164, 210, 218, 0.2);
    border-radius: 9px;
    background: rgba(8, 21, 31, 0.72);
  }

  .model-switch button {
    padding: 7px 10px;
    border: 0;
    border-radius: 6px;
    background: transparent;
    color: #b7cbd0;
    cursor: pointer;
    font: 12px/1.3 system-ui, sans-serif;
  }

  .model-switch button.active {
    background: #d6f1ed;
    color: #10232b;
  }

  .model-switch button:focus-visible {
    outline: 2px solid #90eee3;
    outline-offset: 2px;
  }

  .atom-canvas :global(canvas) {
    display: block;
    width: 100%;
    height: 100%;
  }

  .atom-legend {
    position: absolute;
    top: 64px;
    left: 18px;
    display: grid;
    gap: 9px;
    color: #d7e9ed;
    font: 11px/1.2 system-ui, sans-serif;
  }

  .atom-legend span {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .atom-legend i {
    width: 12px;
    height: 12px;
    flex: 0 0 12px;
    border-radius: 50%;
    background: #90eee3;
    box-shadow: 0 0 10px currentColor;
  }

  .atom-legend .electron-key { background: #f2fff9; box-shadow: 0 0 0 3px rgba(121, 255, 233, .2), 0 0 12px #79ffe9; }
  .atom-legend .electron-cloud-key { width: 14px; height: 14px; border: 1px solid #79ffe9; background: radial-gradient(circle, rgba(121,255,233,.7), rgba(82,140,240,.12) 72%, transparent); }
  .atom-legend .proton-key { background: #ff806d; }
  .atom-legend .neutron-key { background: #65d8d1; }
  .atom-caption {
    position: absolute;
    right: 16px;
    bottom: 0;
    left: 16px;
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    gap: 12px;
    padding: 9px 10px 12px;
    border-top: 1px solid rgba(164, 210, 218, 0.18);
    background: linear-gradient(90deg, rgba(8, 18, 24, 0.96), rgba(8, 18, 24, 0.8));
    color: #d7e9ed;
  }

  .atom-caption p {
    margin: 0;
    font: 12px/1.35 system-ui, sans-serif;
  }

  .atom-caption small {
    color: #a4bdc5;
    font: 10px/1.35 system-ui, sans-serif;
    text-align: right;
  }

  .atom-caption, .atom-legend { z-index: 1; }
  .atom-legend { max-width: 44%; }

  .atom-error {
    position: absolute;
    right: 16px;
    bottom: 55px;
    left: 16px;
    margin: 0;
    color: #ffd2bf;
    font: 13px/1.4 system-ui, sans-serif;
    text-align: center;
  }

  @media (max-width: 620px) {
    .atom-visual { height: clamp(280px, 36svh, 390px); }
    .model-switch { top: 8px; right: 8px; }
    .model-switch button { padding: 6px 8px; font-size: 10px; }
    .atom-canvas { inset: 42px 0 62px; }
    .atom-legend { top: 52px; left: 12px; gap: 6px; max-width: 47%; font-size: 10px; }
    .atom-caption { right: 0; bottom: 0; left: 0; align-items: flex-start; flex-direction: column; gap: 3px; padding: 8px 12px 10px; }
    .atom-caption p { font-size: 11px; }
    .atom-caption small { text-align: left; }
  }
</style>
