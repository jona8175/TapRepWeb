<script>
  import * as THREE from "three";
  import GeoScene from "$lib/geoScene.svelte";
  let points = [
    {
      position: new THREE.Vector3(0.05, 0.35, -0.3),
      canvasCordinates: new THREE.Vector2(3, 0),
      label: "Gletscher",
      text: "Gletscher sind große Eismassen, die sich unter ihrem eigenen Gewicht aktiv bewegen.",
    },
    {
      position: new THREE.Vector3(-0.25, 0.33, 0.4),
      canvasCordinates: new THREE.Vector2(0, 0),
      label: "Moräne",
      text: "Mächtigere Abfolgen aus steinigem, sandigem und tonigem Sedimentmaterial, die durch den Gletscher verfrachtet und abgelagert wurden",
    },
    {
      position: new THREE.Vector3(0.05, 0.15, 0.45),
      canvasCordinates: new THREE.Vector2(0, 0),
      label: "Sander",
      text: "Ein glazifluviales System, in dem überwiegend Ablagerungsprozesse stattfinden. Sander treten oft vor Talgletschern des Hochgebirges auf.",
    },
  ];

  let models = ["BlockDiagram.gltf"];




</script>



<GeoScene points = {points} models = {models}/>


