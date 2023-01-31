<script>
	import Beranda from "./components/Inicio.svelte";
	import Profile from "./components/ListaUsuarios.svelte";
	
	export let menu = 1;
</script>

<style>
	ul#menu li{
		display : inline;
	}
</style>

<ul id="menu">
	<li><a href="/" on:click|preventDefault={() => (menu = 1)}>Inicio</a></li> |
	<li><a href="/" on:click|preventDefault={() => (menu = 2)}>Usuarios</a></li>
</ul>

{#if menu === 1}
<Beranda />
{:else if menu === 2}
<Profile />
{:else}
<h1>
	Page Not Found
</h1>
{/if}
