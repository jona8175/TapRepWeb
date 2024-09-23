<script>
  import { browser } from "$app/environment";
  import * as THREE from "three";
  import { onMount } from "svelte";

  import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
  import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader.js";
  //import { gsap } from "gsap";

  let root;

  let toggle = false;
  let curentVideo = "";

  function openVideo(link) {
    toggle = true;
    curentVideo = link;
  }
  function closeWindow() {
    toggle = false;
  }
  let points = [
    {
      position: new THREE.Vector3(0.05, 0.15, 0.45),
      canvasCordinates: new THREE.Vector2(3, 0),
      label: "Sander1",
      text: "Im Gletschervorfeld.",
    },
    {
      position: new THREE.Vector3(-0.25, 0.33, 0.4),
      canvasCordinates: new THREE.Vector2(0, 0),
      label: "sda",
      text: "Im Gletschervorfeld.",
    },
    {
      position: new THREE.Vector3(-0.37, 0.3, 0.05),
      canvasCordinates: new THREE.Vector2(0, 0),
      label: "Sander 4",
      text: "Im Gletschervorfeld.",
      link: "https://www.youtube.com/embed/64R2MYUt394",
    },
    {
      position: new THREE.Vector3(0.05, 0.35, -0.3),
      canvasCordinates: new THREE.Vector2(0, 0),
      label: "Sander",
      text: "Im Gletschervorfeld.",
    },
  ];

  onMount(() => {
    const canvas = root.querySelector(".webgl");
    // Do something with nd, such as adding event listeners, styles, etc.

    if (browser) {
      const loadingManager = new THREE.LoadingManager();

      const gltfLoader = new GLTFLoader(loadingManager);
      const cubeTextureLoader = new THREE.CubeTextureLoader(loadingManager);

      const scene = new THREE.Scene();

      /**
       * Background
       */
      const params = {
        color: "#ffffff",
      };
      scene.background = new THREE.Color(params.color);

      /**
       * Models
       */

      gltfLoader.load("/models/BlockDiagram.gltf", (gltf) => {
        gltf.scene.scale.set(1, 1, 1);
        gltf.scene.rotation.set(0, 0, 0);
        scene.add(gltf.scene);
      });

      const camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      );

      /**
       * Points of interest
       */
      const raycaster = new THREE.Raycaster();

      /**
       * Lights
       */
      const directionalLight = new THREE.DirectionalLight("#ffffff", 3);
      directionalLight.castShadow = true;
      directionalLight.shadow.camera.far = 15;
      directionalLight.shadow.mapSize.set(1024, 1024);
      directionalLight.shadow.normalBias = 0.05;
      directionalLight.position.set(0.25, 3, -2.25);
      scene.add(directionalLight);

      // Controls
      const controls = new OrbitControls(camera, canvas);
      controls.enableDamping = true;

      /**
       * Renderer
       */

      const renderer = new THREE.WebGLRenderer({
        canvas: canvas,
        antialias: true,
      });

      renderer.toneMapping = THREE.ReinhardToneMapping;
      renderer.toneMappingExposure = 3;
      renderer.shadowMap.enabled = true;
      renderer.shadowMap.type = THREE.PCFSoftShadowMap;

      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

      renderer.setSize(window.innerWidth, window.innerHeight);

      /**
       * Sizes
       */

      const sizes = {
        width: window.innerWidth,
        height: window.innerHeight,
      };

      window.addEventListener("resize", () => {
        // Update sizes
        sizes.width = window.innerWidth;
        sizes.height = window.innerHeight;

        // Update camera
        camera.aspect = sizes.width / sizes.height;
        camera.updateProjectionMatrix();

        // Update renderer
        renderer.setSize(sizes.width, sizes.height);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      });

      camera.position.z = 5;




      const tick = () => {
        controls.update();

        for (const point of points) {
          // Get 2D screen position
          const screenPosition = point.position.clone();
          screenPosition.project(camera);
          const translateX = (0.5 + screenPosition.x * 0.5) * sizes.width;
          const translateY =
            (1 - (0.5 + screenPosition.y * 0.5)) * sizes.height;
          point.canvasCordinates.set(translateX, translateY);

          points = points; //normally completely unnecessary, but it triggers a rerender in svelte
        }

        renderer.render(scene, camera);
        window.requestAnimationFrame(tick);
      };

      tick();
    }
  });
</script>

<div bind:this={root} class="bind-div">
  <body>
    <canvas class="webgl"></canvas>

    {#each points as point, i}
      <div class="point" style="left: {point.canvasCordinates.x}px; top: {point.canvasCordinates.y}px">
        {#if point.link}
          <div class="label" on:click={()=> openVideo(point.link)}>{point.label}</div>
        {:else}
          <div class="label">{point.label}</div>
        {/if}
        <div class="text">{point.text}</div>
      </div>
    {/each}

    {#if toggle}
      <div id="PopUp" class="PopUp">
        <button class="close" on:click={closeWindow}>x</button>
        <iframe id="iframeVid" src={curentVideo}> </iframe>
      </div>
    {/if}
  </body>
</div>

<style>
  body {
    height: 100%;
    overflow: hidden;
  }
  .webgl {
    position: static;
    top: 0;
    left: 0;
    outline: none;
    z-index: -10;
    height: 100%;
  }

  .point {
    position: absolute;
    /* pointer-events: none; */
    z-index: 10;
    background-color: rgba(220, 220, 220, 0.594);
    padding: 0.5rem;
    border-radius: 0.5rem;
  }

  .point .label {
    
  }

  .point .text {
    opacity: 0;
    height: 0;
    width: 0;
  }

  .point:hover .text {
    opacity: 1;
    height: auto;
    width: auto;
  }

  .PopUp {
    position: absolute;
    background-color: gainsboro;
    padding: 1rem;
    top: 20%;
    left: 20%;
    width: 60%;
    height: 60%;
    z-index: -20;
    pointer-events: none;
    border-radius: 1rem;
    opacity: 1;
    pointer-events: auto;
    z-index: 30;
  }
  iframe {
    display: block;
    width: 100%;
    height: 100%;
    margin-left: auto;
    margin-right: auto;
    border: none;
  }
  
  .close{
    position: absolute;
    top: 0;
    right: 0;
    background-color: red;
    color: white;
    border: none;
    padding: 0.5rem;
    border-radius: 0.5rem;
  }
  
    
</style>
