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

  let models = ["Scene1.gltf","Scene2.gltf","Scene3.gltf","Scene4.gltf","Scene5.gltf","Scene6.gltf","Scene7.gltf","Scene8.gltf","Scene9.gltf","Scene10.gltf"];

  let cameraInitialPosition = new THREE.Vector3(-2,1,1);

  let light_type = "DroneImageScene" /*DroneImageScene or 3DModel*/


</script>



<GeoScene points = {points} models = {models} cameraInitialPosition = {cameraInitialPosition} light_type = {light_type}/>


