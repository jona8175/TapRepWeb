<!-- Hier wird das menu erstelt was wir across all pages benutzen, 
 an dieser stelle könnten ähnlich dinge gemacht werden-->
<div class = "scrollwrap">
<div class = "bar"></div>
<nav class = "menu">
  <input type="checkbox" id="check">
  <label for="check" class ="checkbtn">
    <ul>
      <li><a href="/wilkommen">Wilkommen</a></li>
      <li><a href="/blockdiagram">Blockdiagram</a></li>
      <li><a>Orte</a></li>
      <li><a href="#">Impressum</a></li>
      <li><a href="/help">Hilfe</a></li>
      <li><a href="/Quellen">Quellen</a></li>
    </ul>
  </label>
  
  
  <div class="nav-mobile">
      <a href="/findelen">Findelen</a>
      <a href="/grindelwald">Grindelwald</a>
  </div>
</nav>

<!-- im slot ist der inhalt der sub-page-->
<div class = "scene">
  <slot></slot>
</div>

</div>

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
  margin-left: 290px;
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



</style>

<script>
  let scene =1;
</script>