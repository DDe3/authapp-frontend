<script>
    import { user } from "../js/store.js";
    import { form, field } from 'svelte-forms';
    import { required } from 'svelte-forms/validators';

    const username = field('name', '', [required()]);
    const password = field('name', '', [required()]);
    const myForm = form(username);
    

    export let name;
    export let logged;
    let response = ""

    function signOut() {
        logged = false;
        user.set({ username: "", password: "" })
    }

    async function doChangePassword() {
        let usuario = { username : $username.value, password : $password.value}
        const res = await fetch(
            "http://localhost:8081/apidistribuida/v1/clientes/update-password",
            {
                method: "PUT",
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(usuario),
            }
        ).then(r => r.json());
        response = res
    }

</script>



<style>

  input[type=text], input[type=password] {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    box-sizing: border-box;
  }
  
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

<h1>Bienvenido {name}</h1>
<button on:click={signOut}>Cerrar sesión</button>
<br>
<br>
<br>
<h1>Cambiar contraseña</h1>
<section>
    <input type="text" bind:value={$username.value} placeholder="username"/>
    {#if $myForm.hasError('name.required')}
        <div>Name is required</div>
    {/if}
    <input type="password" bind:value={$password.value} placeholder="new password"/>
    {#if $myForm.hasError('name.required')}
        <div>Password is required</div>
    {/if}
  
    <button disabled={!$myForm.valid} on:click={doChangePassword}>Actualizar</button>
</section>

<pre>
    {response}
</pre>

