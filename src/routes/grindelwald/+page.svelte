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
  
    let models = ["GrindScene1.gltf","GrindScene2.gltf","GrindScene3.gltf","GrindScene4.gltf","GrindScene5.gltf","GrindScen6.gltf","GrindScene7.gltf","GrindScene8.gltf","GrindScene9.gltf","GrindScene10.gltf","GrindScene11.gltf","GrindScene12.gltf","GrindScene13.gltf","GrindScene14.gltf","GrindScene15.gltf","GrindScene16.gltf","GrindScene17.gltf","GrindScene18.gltf"];
  
    let cameraInitialPosition = new THREE.Vector3(-2,0.5,2);
  
    let light_type = "DroneImageScene" /*DroneImageScene or 3DModel*/
  
  
  </script>
  
  
  
  <GeoScene points = {points} models = {models} cameraInitialPosition = {cameraInitialPosition} light_type = {light_type}/>
  
  
  