<script>
    import logo from '../assets/logo.png'
    import { user } from "../js/store.js";

    export let name;
    export let logged;

    function signOut() {
        logged = false;
        user.set({ username: "", password: "" })
    }

</script>



<style>
img {
  padding: 5px;
  width: 150px;
}

img:hover {
  box-shadow: 0 0 2px 1px rgba(0, 140, 186, 0.5);
}


</style>

<h1>Bienvenido {name}</h1>
<button on:click={signOut}>Cerrar sesión</button>
<br>
<br>
<br>
<a href="https://svelte.dev">
    <img src="{logo}" alt="Error">
</a>
<h6>Hecho en Svelte</h6>
<a href="https://github.com/DDe3/authapp-frontend">Repositorio</a>

