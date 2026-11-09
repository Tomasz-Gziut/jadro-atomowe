<script>
  import { onMount } from 'svelte';
  import * as THREE from 'three';

  /** @type {HTMLDivElement} */
  let mount;
  let renderError = '';

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
    camera.position.set(0, 0, 9.5);
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

    [
      { x: -0.19, y: 0.2, z: 0.18, material: protonMaterial },
      { x: 0.2, y: -0.19, z: 0.18, material: protonMaterial },
      { x: 0.2, y: 0.2, z: -0.18, material: neutronMaterial },
      { x: -0.19, y: -0.19, z: -0.18, material: neutronMaterial }
    ].forEach(({ x, y, z, material }) => {
      const nucleon = new THREE.Mesh(nucleonGeometry, material);
      nucleon.position.set(x, y, z);
      nucleons.add(nucleon);
    });

    const cloudCount = 22000;
    const cloudPositions = new Float32Array(cloudCount * 3);
    const cloudColors = new Float32Array(cloudCount * 3);
    const innerColor = new THREE.Color(0x90eee3);
    const outerColor = new THREE.Color(0x528cf0);

    for (let i = 0; i < cloudCount; i += 1) {
      const offset = i * 3;
      const radius = -Math.log(Math.random() * Math.random() * Math.random()) * 0.35;
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
    const animate = () => {
      atom.rotation.y += 0.0015;
      atom.rotation.x = Math.sin(performance.now() * 0.00015) * 0.08;
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
      cloudGeometry.dispose();
      cloud.material.dispose();
      nucleonGeometry.dispose();
      protonMaterial.dispose();
      neutronMaterial.dispose();
      renderer.dispose();
      renderer.domElement.remove();
    };
  });
</script>

<div class="atom-visual">
  <div class="atom-canvas" bind:this={mount} aria-hidden="true"></div>
  <div class="atom-legend" aria-hidden="true">
    <span><i class="electron-key"></i>chmura elektronowa</span>
    <span><i class="proton-key"></i>proton</span>
    <span><i class="neutron-key"></i>neutron</span>
  </div>
  <div class="atom-caption">
    <p>Elektrony opisuje chmura prawdopodobieństwa, nie tory planet.</p>
    <small>Model poglądowy · jądro powiększone, nie w skali</small>
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
    inset: 0 0 43px;
  }

  .atom-canvas :global(canvas) {
    display: block;
    width: 100%;
    height: 100%;
  }

  .atom-legend {
    position: absolute;
    top: 16px;
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
  .atom-legend .neutron-key { background: #65d8d1; }

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
    .atom-legend { top: 12px; left: 12px; gap: 6px; font-size: 10px; }
    .atom-caption { right: 12px; bottom: 10px; left: 12px; align-items: flex-start; flex-direction: column; gap: 3px; }
    .atom-caption p { font-size: 11px; }
    .atom-caption small { text-align: left; }
  }
</style>
