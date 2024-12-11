
<script>
    export let menupoints=[];

    let isStyled = false;

    function toggleStyle() {
        isStyled = !isStyled;
    }
    function setStyle(a) { 
        isStyled = a;
    }
</script>

<div class="menu">
<ul>
{#each menupoints as menupoint, i}
      
    {#if menupoint.sub}
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <a href="#" on:click={() => toggleStyle()} > {menupoint.label}</a>
    {:else}
    <a href="{menupoint.link}" on:click={() => setStyle(true)}>{menupoint.label}</a>
    {/if}
{/each}
</ul>
</div>

<!--{isStyled ? 'styled' : ''}-->
<div class="submenu {isStyled ? 'styled' : ''}">
    <ul>
        <li><a href="/TapRepWeb/findelen" on:click={() => setStyle(true)}>Findelen</a></li>
        <li><a href="/TapRepWeb/grindelwald" on:click={() => setStyle(true)}>Grindelwald</a></li>
        <li><a href="/TapRepWeb/silveretta" on:click={() => setStyle(true)}>Silveretta</a></li>
    </ul>
</div>



<style>
    .menu{
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        z-index: 30;
        flex-direction: row;
        background-color: rgb(61, 61, 61);;
    }
    .menu ul{
        list-style-type: none;
        height: 100%;
    }
    .menu ul a{
        padding:16px;
        color: black;
        background-color: rgb(61, 61, 61);
        text-align: center;
        text-decoration: none;
    }
    .menu ul a:hover{
        background-color: grey;
        color:white;
        text-align: center;
        text-decoration: none;
        transition: background-color 1s;
    }

    .submenu{
        position: absolute;
        top: 34px;
        left: 267px;
        z-index: 29;
        visibility: visible;
        display: block;
        flex-direction: column;
    }

    .submenu.styled{
        visibility: collapse;
    }

    .submenu ul{
        list-style: none;
        background-color: blue;
        align-items: left;
        padding-left: 0rem;
   
    }

    .submenu ul a{
        
        list-style: none;
        color: black;
        background-color: rgb(115, 113, 113);
        text-decoration: none;
        color: var(--text-col);
        padding: 1rem  1rem;
        
        display: block;
    }
    .submenu ul a:hover{
        color: rgb(63, 61, 61);
        background-color: rgb(114, 113, 113);
        transition: background-color 1s;
        
    }

</style>
