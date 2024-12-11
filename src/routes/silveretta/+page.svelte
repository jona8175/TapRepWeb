<script>
    import * as THREE from "three";
    import GeoScene from "$lib/geoScene.svelte";
    let points = [
      
      {
        position: new THREE.Vector3(0.15, 0.7, -0.6),
        canvasCordinates: new THREE.Vector2(0, 0),
        label: "Demo",
        text: "Click to watch a demo video",
        link: "https://www.youtube.com/embed/bcB4zxubK-0",
      },
    ];
  
    let models = ["Silv_tile_1.gltf",
    "Silv_tile_2.gltf",
    "Silv_tile_3.gltf",
    "Silv_tile_4.gltf",
    "Silv_tile_5.gltf",
    "Silv_tile_6.gltf",
    "Silv_tile_7.gltf",
    "Silv_tile_8.gltf",
    "Silv_tile_9.gltf",
    "Silv_tile_10.gltf",
    "Silv_tile_11.gltf",
    "Silv_tile_12.gltf",
    "Silv_tile_13.gltf",
    "Silv_tile_14.gltf",
    "Silv_tile_15.gltf",
    "Silv_tile_16.gltf",
    "Silv_tile_17.gltf",
    "Silv_tile_18.gltf",
    "Silv_tile_19.gltf",
    "Silv_tile_20.gltf",
    "Silv_tile_21.gltf",
    "Silv_tile_22.gltf",
    "Silv_tile_23.gltf",
    "Silv_tile_24.gltf",
    "Silv_tile_25.gltf",
    "Silv_tile_26.gltf",
    "Silv_tile_27.gltf",
    "Silv_tile_28.gltf",
    "Silv_tile_29.gltf",
    "Silv_tile_30.gltf",
    "Silv_tile_31.gltf",
    "Silv_tile_32.gltf",
    "Silv_tile_33.gltf",
    "Silv_tile_34.gltf",
    "Silv_tile_35.gltf",
    "Silv_tile_36.gltf",
    "Silv_tile_37.gltf",
    "Silv_tile_38.gltf",
    "Silv_tile_39.gltf",
    "Silv_tile_40.gltf",
    "Silv_tile_41.gltf",
    "Silv_tile_42.gltf",
    "Silv_tile_43.gltf",
    "Silv_tile_44.gltf"
    ];
  
    let cameraInitialPosition = new THREE.Vector3(-2,2,2);
  
    let light_type = "DroneImageScene" /*DroneImageScene or 3DModel*/
  
  
  </script>
  
  
  
  <GeoScene points = {points} models = {models} cameraInitialPosition = {cameraInitialPosition} light_type = {light_type}/>
  
  
  