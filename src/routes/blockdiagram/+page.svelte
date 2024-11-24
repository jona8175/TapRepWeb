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
      position: new THREE.Vector3(-0.17, 0.22, -0.1),
      canvasCordinates: new THREE.Vector2(3, 0),
      label: "Toteis",
      text: "Wenn Gletscher abschmelzen, bleiben oft isolierte Eisblöcke als sogenanntes Toteis zurück. Diese schmelzen teilweise langsam ab während sich der Gletscher weiter zurückzieht. ",
    },
    {
      position: new THREE.Vector3(-0.05, 0.12, 0.1),
      canvasCordinates: new THREE.Vector2(3, 0),
      label: "Toteis-See",
      text: "Die Hohlform welche von Toteisblöcken zurückgelassen wird kann sich mit Wasser füllen. ",
    },
    {
      position: new THREE.Vector3(0, 0.6, 0.25),
      canvasCordinates: new THREE.Vector2(3, 0),
      label: "Gletscher Vorfeld",
      text: "Gletschervorfeld bezeichnet das Gelände zwischen dem Heutigen Gletscherrand und den Moränen des 1850 Vorstosses. Dieses Gebiet ist oft dominiert vom Schutt der Grundmoräne Vegetation ist erst auf dem Vormarsch. Der Formenschatz umfasst Bildungen wie Sander, Toteis, Rundhöcker und Drumlins.",
    },
    {
      position: new THREE.Vector3(0.28, 0.22, -0.1),
      canvasCordinates: new THREE.Vector2(3, 0),
      label: "Rundhöcker",
      text: "Längliche Hügel, aus dem im Untergrund-Gestein werden als Rundhöcker bezeichnet. Sie wurden durch das vorrückende Eis abgeschliffen. ",
    },
    {
      position: new THREE.Vector3(0.8, 0.15, 0.1),
      canvasCordinates: new THREE.Vector2(3, 0),
      label: "Massenbewegung",
      text: "In sogenannten Massenbewegungen Ereignissen werden grosse Mengen von Material Talabwärts bewegt. Solche es gibt sehr viele verschiedene Arten von Ereignissen wie Bergstürze, oder Murgänge die wiederum zu unzähligen verschiedenen Formen wie Sturzhalden, Lawinenhalden und Murgang Akkumulationen führen. Diese Events und formen werden von verschiedenen Autoren nach Grösse, Geschwindigkeit, involviertem Material oder weiteren Faktoren klassifiziert.",
    },
    {
      position: new THREE.Vector3(-0.25, 0.25, 0.4),
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

  let light_type = "3DModel" /*DroneImageScene or 3DModel*/

  let cameraInitialPosition = new THREE.Vector3(2,1,1);

</script>


<GeoScene points = {points} models = {models} light_type = {light_type} cameraInitialPosition = {cameraInitialPosition}/>

