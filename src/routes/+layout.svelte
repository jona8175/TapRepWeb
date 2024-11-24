<!-- Hier wird das menu erstelt was wir across all pages benutzen, 
 an dieser stelle könnten ähnlich dinge gemacht werden-->


<Menu menupoints = {menureiter}></Menu>

<!--
<div class = "bar"></div>
<nav class = "menu">
  <input type="checkbox" id="check">
  <label for="check" class ="checkbtn">
    <ul>
      <li><a href="/wilkommen" on:click={() => toggleStyle(true)}>Wilkommen</a></li>
      <li><a href="/blockdiagram" on:click={() => toggleStyle(false)}>Blockdiagram</a></li>
      <li><a>Orte</a></li>
      <li><a href="#" on:click={() => toggleStyle(true)}>Impressum</a></li>
      <li><a href="/help" on:click={() => toggleStyle(true)}>Hilfe</a></li>
      <li><a href="/Quellen" on:click={() => toggleStyle(true)}>Quellen</a></li>
    </ul>
  </label>
  
  <div class="nav-mobile">
      <a href="/findelen" on:click={() => toggleStyle(false)}>findelen</a>
      <a href="/grindelwald" on:click={() => toggleStyle(false)}>Grindelwald</a>
  </div>
</nav>
-->

<!--Help
<div class="helpbox {isStyled ? 'styled' : ''}">
  <div>
    <h1>Help</h1>
    <a>Beim Navigieren den Cursor nicht über Text Elementen halten.</a>
    <br>
    <br>
    <a>Navigieren:</a><br>
    <a> Scrollen um die grösse zu ändern.</a><br>
    <a>Rechtsklick gedrückt halten und Maus bewegen um zu rotieren. </a><br>
    <a>Shift & Rechtsklick gedrückt halten und Maus bewegen um das Model zu verschieben. </a><br>
    <a on:click={() => toggleStyle(true)}>close</a>
  </div>
  
</div>
-->
<!-- im slot ist der inhalt der sub-page-->
<div class = "scene">
  <slot></slot>
</div>

<script>
  import Menu from "$lib/menu.svelte";
  let scene =1;

  let isStyled_Inst = false; // Function to toggle the style 

  function toggleStyle_Inst(a) { 
    isStyled = a;
  }

  let menureiter = [
    {
      label: "Wilkommen",
      link: "/TapRepWeb/",
      sub: false
    },
    {
      label: "Blockdiagram",
      link: "/TapRepWeb/blockdiagram",
      sub: false
    },
    {
      label: "Orte",
      link: "#",
      sub: true
    },
    {
      label: "Impressum",
      link: "/TapRepWeb/impressum",
      sub: false
    },
    {
      label: "Quellen",
      link: "/TapRepWeb/Quellen",
      sub: false
    },
  ]

</script>

<style>
/* Menu stuff*/
:root{
  --background_prim: grey;
  --background_sec:lightgrey;
  --accent_prim:darkblue;
  --accent_sec:lightblue;
  --text-col:white;
  
  font-family: Helvetica, sans-serif;
}

.menu{
  z-index: 3;
  position: absolute;
  top: 0;
  left: 0;
  height: 55px;
  flex-direction: row;
  
}

.bar{
  z-index: 2;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 55px;
  background-color:var(--background_prim);
  
}

.scene{
  z-index: 1;
  position: absolute;
  top: 0;
  left: 0;

}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: var(--background_prim);
  height:55px;
}

li {
  float: left;
  background-color: var(--background_prim);
}

li a {
  display: block;
  color: var(--text-col);
  text-align: center;
  padding: 16px 16px;
  text-decoration: none;
}

li a:hover {
  background-color: var(--accent_prim);
  transition: background-color 0.4s;
}

/*burger menu*/

.checkbtn{
  text-decoration: none; 
  font-size: 20px;
  cursor: pointer;
  color: var(--text-col);
}

.checkbtn a { 
}

.checkbtn a:hover {
  background-color: var(--accent_sec);
}

#check{
  display: none;
}

#check:checked ~ .nav-mobile{
  display: block ;
  transition: background-color 1s;
}

.nav-mobile {
  display: none;
  position: absolute;
  top: 55px;
  margin-left: 500px;
  overflow: hidden;
  background: var(--background_sec);
  z-index: 1;
  width: 200px;
}


.nav-mobile a:hover {
  background: var(--accent_sec);
  transition: background-color 0.8s;
}

.nav-mobile a {
  text-decoration: none;
  color: var(--text-col);
  padding: 1rem 1.5rem;
  display: block;
}

/* Text pages*/
.sheet {
  background-color: rgb(230, 236, 236);
  padding-right: 70pt;
  padding-left: 50pt;
  padding-bottom: 100pt;
  margin-top: 0px;
  margin-bottom: 0px;
  margin-right: 50px;
  margin-left: 50px;
  display: flex;
  flex-direction: column;
}

.helpbox{
  
  z-index: 4;
  position: absolute;
  top: 100px;
  right: 20px;
  height: 400px;
  width: 200px;
  flex-direction: column;
  background-color: rgba(177, 172, 172, 0.961);
  visibility: visible;
}

/* Additional style when isStyled is true */ 
.helpbox.styled {
  visibility: hidden;
}
.helpbox div{
  margin-left: 10px;
  margin-right: 10px;
}
.helpbox a{
  color: blue;
}



</style>

