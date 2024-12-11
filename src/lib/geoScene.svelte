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

  export let points = [];
  export let cameraInitialPosition = new THREE.Vector3(0, 3, 5);
  export let scene_background_color = "#b7d9eb";
  export let light_type = "";

  export let models = [];
      //only works when file is in static/models

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
        color: scene_background_color,
      };
      scene.background = new THREE.Color(params.color);

      /**
       * Models
       */

      

      for (const block of models) {
        console.log(block);
        //add /TapRepWeb when deploying
        gltfLoader.load("/models/" + block , (gltf) => {
          gltf.scene.scale.set(1, 1, 1);
          gltf.scene.rotation.set(0, 0, 0);
          scene.add(gltf.scene);

          updateAllMaterials();
        });
      }


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

      
      if (light_type == "3DModel") {
        const directionalLight = new THREE.DirectionalLight("#ffffff", 3);
        directionalLight.castShadow = false;
        directionalLight.shadow.camera.far = 15;
        directionalLight.shadow.mapSize.set(1024, 1024);
        directionalLight.shadow.normalBias = 0.05;
        directionalLight.position.set(0.25, 3, -2.25);
        scene.add(directionalLight);
      } else if (light_type == "DroneImageScene") {
        const light = new THREE.AmbientLight( 0x404040 ); // soft white light
        light.intensity = 25
        scene.add( light );
      }

      
     

      

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

      camera.position.x = cameraInitialPosition.x;
      camera.position.y = cameraInitialPosition.y;
      camera.position.z = cameraInitialPosition.z;

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

  // instruction box
  let isStyled = false;

  function toggleStyle_Inst(a) { 
    isStyled = !a;
  }

</script>

<div bind:this={root} class="bind-div">
  <body>
    <canvas class="webgl"></canvas>

    {#each points as point, i}
      <div
        class="point"
        style="left: {point.canvasCordinates.x}px; top: {point.canvasCordinates
          .y}px"
      >
        {#if point.link}
          <div class="label" on:click={() => openVideo(point.link)}>
            {point.label}
          </div>
        {:else}
          <div class="label">{point.label}</div>
        {/if}
        <div class="text"> <a href= {point.textlink}> {point.text} </a> </div>
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

<div class="instruction_box {isStyled ? 'styled' : ''} ">
    <img class="centered_img" src="/src/Instructions.png" alt="Instructions" width="80%" height="80%">
    <br>
    <a on:click={() => toggleStyle_Inst()} > Tipp Auflösen </a>
</div>

<style>
  .instruction_box{
    z-index: 4;
    position: absolute;
    top: 70%;
    right: 30%;
    height: 10%;
    width: 40%;
    display: flex;
    flex-direction: column;
    text-align: center;
    background-color: rgba(177, 172, 172, 0.961);
    visibility: visible;
  }
  .instruction_box.a {
    cursor: pointer !important;
  }
  
  .centered_img {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  height: auto;
  }
  .instruction_box.styled {
    visibility: hidden;
  }
  body {
    height: 100%;
    width: 100%;
    overflow: hidden;
  }
  
  .webgl {
    position: static;
    top: 0;
    left: 0;
    outline: none;
    z-index: -10;
    height: 100%;
    width: 100%;
    display:flex;
    flex-flow: stretch; /*important for stretch bug*/
    overflow: hidden;
  }

  .point {
    position: absolute;
    font-size: 8pt;
    /* pointer-events: none; */
    z-index: 10;
    background-color: rgba(220, 220, 220, 0.594);
    padding: 0.5rem;
    border-radius: 0.5rem;
    -webkit-user-select: none; /* Safari */
    -ms-user-select: none; /* IE 10 and IE 11 */
    user-select: none; /* Standard syntax */
    overflow: hidden;
  }

  .point .label {
    user-select: none;
    overflow: hidden;
  }

  .point .text {
    opacity: 0;
    height: 0;
    width: 0;
    user-select: none;
    overflow: hidden;
  }

  .point:hover {
    background-color: rgba(217, 227, 219, 0.984);
    z-index: 11;
  }

  .point:hover .text {
    opacity: 1;
    height: auto;
    width:  150px;
    user-select: none;
    overflow: hidden;
    
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
    user-select: none;
    overflow: hidden;
  }
  iframe {
    display: block;
    width: 100%;
    height: 100%;
    margin-left: auto;
    margin-right: auto;
    border: none;
    overflow: hidden;
  }

  .close {
    position: absolute;
    top: 0;
    right: 0;
    background-color: red;
    color: white;
    border: none;
    padding: 0.5rem;
    border-radius: 0.5rem;
    overflow: hidden;
  }
  

</style>
