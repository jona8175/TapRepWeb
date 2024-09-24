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

  let models = ["Scene5_1.gltf","Scene5_2.gltf","Scene5_3.gltf","Scene5_4.gltf","Scene5_5.gltf","Scene5_6.gltf","Scene5_7.gltf","Scene5_8.gltf"];

  let cameraInitialPosition = new THREE.Vector3(-2,1,1);


</script>



<GeoScene points = {points} models = {models} cameraInitialPosition = {cameraInitialPosition}/>


