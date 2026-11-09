<script>
  import { onMount } from 'svelte';
  import * as THREE from 'three';

  /** @type {HTMLDivElement} */
  let mount;
  let renderError = '';
  let modelMode = 'quantum';
  /** @type {(mode: string) => void} */
  let updateModel = () => {};

  /** @param {string} mode */
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
    const nucleonGeometry = new THREE.SphereGeometry(0.235, 32, 24);
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

    const proton = new THREE.Mesh(nucleonGeometry, protonMaterial);
    nucleons.add(proton);

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
        size: 0.045,
        sizeAttenuation: true,
        vertexColors: true,
        transparent: true,
        opacity: 0.37,
        depthWrite: false,
        blending: THREE.AdditiveBlending
      })
    );
    atom.add(cloud);

    const electronMaterial = new THREE.MeshBasicMaterial({
      color: 0xe7fff7,
      transparent: true,
      blending: THREE.AdditiveBlending
    });
    const electronGeometry = new THREE.SphereGeometry(0.075, 24, 16);
    const electron = new THREE.Mesh(electronGeometry, electronMaterial);
    const electronGlow = new THREE.PointLight(0x9bffe9, 2.2, 1.5);
    electron.add(electronGlow);
    atom.add(electron);

    const orbitGroup = new THREE.Group();
    orbitGroup.rotation.set(0.8, 0.2, -0.28);
    const orbit = new THREE.Mesh(
      new THREE.TorusGeometry(bohrRadius, 0.012, 8, 180),
      new THREE.MeshBasicMaterial({ color: 0x7adfd6, transparent: true, opacity: 0.5 })
    );
    orbitGroup.add(orbit);
    const orbitalElectron = new THREE.Mesh(electronGeometry.clone(), electronMaterial.clone());
    orbitGroup.add(orbitalElectron);
    atom.add(orbitGroup);

    updateModel = (mode) => {
      const isQuantum = mode === 'quantum';
      cloud.visible = isQuantum;
      electron.visible = isQuantum;
      orbitGroup.visible = !isQuantum;
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
      atom.rotation.y += 0.0015;
      atom.rotation.x = Math.sin(now * 0.00015) * 0.08;
      if (now - lastMeasurement > 480) {
        setQuantumMeasurement();
        lastMeasurement = now;
      }
      orbitalElectron.position.set(
        bohrRadius * Math.cos(now * 0.0012),
        bohrRadius * Math.sin(now * 0.0012),
        0
      );
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
      nucleonGeometry.dispose();
      protonMaterial.dispose();
      neutronMaterial.dispose();
      electron.geometry.dispose();
      electron.material.dispose();
      orbitalElectron.geometry.dispose();
      orbitalElectron.material.dispose();
      orbit.geometry.dispose();
      orbit.material.dispose();
      renderer.dispose();
      renderer.domElement.remove();
    };
  });
</script>

<div class="atom-visual">
  <div class="model-switch" role="group" aria-label="Wybierz model atomu">
    <button class:active={modelMode === 'quantum'} aria-pressed={modelMode === 'quantum'} onclick={() => selectModel('quantum')}>
      Kwantowy · 1s
    </button>
    <button class:active={modelMode === 'illustrative'} aria-pressed={modelMode === 'illustrative'} onclick={() => selectModel('illustrative')}>
      Poglądowy
    </button>
  </div>
  <div class="atom-canvas" bind:this={mount} aria-hidden="true"></div>
  <div class="atom-legend" aria-hidden="true">
    <span><i class="electron-key"></i>{modelMode === 'quantum' ? 'prawdopodobieństwo elektronu' : 'umowna orbita elektronu'}</span>
    <span><i class="proton-key"></i>proton · jądro wodoru</span>
  </div>
  <div class="atom-caption">
    {#if modelMode === 'quantum'}
      <p>Wodór · stan 1s: chmura pokazuje, gdzie można wykryć elektron.</p>
      <small>Punkt to przykładowy pomiar; jądro powiększone, nie w skali.</small>
    {:else}
      <p>Uproszczenie: elektron obiega proton po umownej orbicie.</p>
      <small>Rzeczywisty elektron nie porusza się po takiej trajektorii.</small>
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
    font: 11px/1.2 system-ui, sans-serif;
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
    gap: 8px;
    color: #d7e9ed;
    font: 11px/1.2 system-ui, sans-serif;
  }

  .atom-legend span {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .atom-legend i {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: #90eee3;
    box-shadow: 0 0 10px currentColor;
  }

  .atom-legend .proton-key { background: #ff806d; }
  .atom-caption {
    position: absolute;
    right: 16px;
    bottom: 12px;
    left: 16px;
    display: flex;
    align-items: baseline;
    justify-content: space-between;
    gap: 12px;
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
    .atom-legend { top: 52px; left: 12px; gap: 6px; font-size: 10px; }
    .atom-caption { right: 12px; bottom: 10px; left: 12px; align-items: flex-start; flex-direction: column; gap: 3px; }
    .atom-caption p { font-size: 11px; }
    .atom-caption small { text-align: left; }
  }
</style>
