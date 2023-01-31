<script>
    import Home from "./Home.svelte";
    import Login from "./Login.svelte";
    import Signin from "./Signin.svelte";
    import { user } from "../js/store.js";

    let register = false;
    let logged = false;

    function registerShow() {
        register = true;
    }
</script>

{#if logged && !register}
    <Home name={$user.username} bind:logged />
{/if}

{#if !logged && !register}
    <Login bind:logged />
    <button on:click={registerShow}>Registrarse</button>
{/if}

{#if !logged && register}
    <Signin bind:registered={register} />
{/if}

<style>
    button {
        background-color: #04aa6d;
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
