<script>
  import * as THREE from "three";
  import GeoScene from "$lib/geoScene.svelte";
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

  let models = ["Scene5_1.gltf","Scene5_2.gltf","Scene5_3.gltf"];




</script>



<GeoScene points = {points} models = {models}/>


