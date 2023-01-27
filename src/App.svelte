<script>
  import Home from "./components/Home.svelte";
  import Login from "./components/Login.svelte";
  import Signin from "./components/Signin.svelte";
  import { user } from "./js/store.js";


  let register = false
  let logged = false

  function registerShow() {
    register = true
  }
  
</script>

<main>
  {#if logged && !register}
    <Home name={$user.username} bind:logged={logged}/>
  {/if}

  {#if !logged && !register}
    <Login bind:logged={logged}/>
    <button on:click={registerShow}>Registrarse</button>
  {/if}


  {#if !logged && register}
    <Signin bind:registered={register}/>
  {/if}

</main>

<style>
button {
  background-color: #04AA6D;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 100%;
}

button:hover {
  opacity: 0.8;
}
</style>
