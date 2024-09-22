<script>
  import { browser } from "$app/environment";
  import * as THREE from "three";
  import { onMount } from "svelte";

  import { OrbitControls } from "three/examples/jsm/controls/OrbitControls.js";
  import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader.js";
  //import { gsap } from "gsap";

  let root;
  onMount(() => {
    const canvas = root.querySelector(".webgl");
    // Do something with nd, such as adding event listeners, styles, etc.

    if (browser) {
      const loadingManager = new THREE.LoadingManager(
        // Loaded
        () => {
          // Wait a little
          window.setTimeout(() => {
            // Animate overlay
            gsap.to(overlayMaterial.uniforms.uAlpha, {
              duration: 3,
              value: 0,
              delay: 1,
            });

            // Update loadingBarElement
            loadingBarElement.classList.add("ended");
            loadingBarElement.style.transform = "";
          }, 500);

          window.setTimeout(() => {
            sceneReady = true;
          }, 2000);
        },

        // Progress
        (itemUrl, itemsLoaded, itemsTotal) => {
          // Calculate the progress and update the loadingBarElement
          const progressRatio = itemsLoaded / itemsTotal;
          loadingBarElement.style.transform = `scaleX(${progressRatio})`;
        }
      );

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

        updateAllMaterials();
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
      const points = [
        {
          position: new THREE.Vector3(0.05, 0.15, 0.45),
          element: document.querySelector(".point-0"),
        },
        {
          position: new THREE.Vector3(-0.25, 0.33, 0.4),
          element: document.querySelector(".point-1"),
        },
        {
          position: new THREE.Vector3(-0.37, 0.3, 0.05),
          element: document.querySelector(".point-2"),
        },
        {
          position: new THREE.Vector3(0.05, 0.35, -0.3),
          element: document.querySelector(".point-3"),
        },
      ];
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
          console.log(point);

          // Get 2D screen position
          const screenPosition = point.position.clone();
          screenPosition.project(camera);

          // Set the raycaster
          raycaster.setFromCamera(screenPosition, camera);
          const intersects = raycaster.intersectObjects(scene.children, true);

          point.element.classList.add("visible"); //add this and comment out the if else so tags allways show

          const translateX = screenPosition.x * sizes.width * 0.5;
          const translateY = -screenPosition.y * sizes.height * 0.5;
          point.element.style.transform = `translateX(${translateX}px) translateY(${translateY}px)`;
        }

        // TODO: Implement points and Loading

        renderer.render(scene, camera);
        window.requestAnimationFrame(tick);
      };
      tick();
      
      /*function closeVideo() {
        var element = document.getElementById("PopUp");
        element.classList.remove("active");
        document.getElementById("iframeVid").src = "https://www.google.ch";
      }

      function summonVideo(link) {
        var element = document.getElementById("PopUp");
        element.classList.add("active");
        document.getElementById("iframeVid").src = link;
      }*/
    }
  });
</script>

<div bind:this={root} class="bind-div">
  <body>
    <canvas class="webgl"></canvas>
    <div class="point point-0">
      <div
        class="label"
      >
        Sander
      </div>
      <div class="text">Im Gletschervorfeld.</div>
    </div>
    <div class="point point-1">
      <div class="label">UferMoräne</div>
      <div class="text">
        Sie war seitlich vom Gletscher und besteht aus erosions Material vom
        Gletscher und den angrenzenden Berghängen. Nach dem Abschmelzen des
        Gletschers ebleibt ein Wall am Hangfuß des Tals.
      </div>
    </div>
    <div class="point point-2">
      <div
        class="label"
      >
        See
      </div>
      <div class="text">Durch die Moräne angestaut.</div>
    </div>
    <div class="point point-3">
      <div
        class="label">
        Gletscher
      </div>
      <div class="text">Zusatz Text.</div>
    </div>

    <!-- pop up
    <div id="PopUp" class="PopUp active youtube-player-popup">
      <button onclick="closeVideo()">Close</button>
      <iframe id="iframeVid" src="https://www.youtube.com/embed/64R2MYUt394">
      </iframe>
    </div>
    -->
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
    top: 50%;
    left: 50%;
    /* pointer-events: none; */
    z-index: 10;
  }

  .point .label {
  }

  .point .text {
    opacity: 0;
  }

  .point:hover .text {
    opacity: 1;
  }

  /*.PopUp {
    position: absolute;
    background-color: blueviolet;
    top: 20%;
    left: 20%;
    width: 60%;
    height: 60%;
    z-index: -20;
    opacity: 0;
    pointer-events: none;
  }
  .PopUp.active {
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
  }*/
</style>
