<script>

    import { form, field } from 'svelte-forms';
    import { required } from 'svelte-forms/validators';

    const name = field('name', '', [required()]);
    const password = field('name', '', [required()]);
    const myForm = form(name);

    

    export let register = "";
    export let registered;

    async function doRegister() {
        let user = { username : $name.value, password : $password.value}
        const res = await fetch(
            "http://localhost:8081/apidistribuida/v1/clientes/register",
            {
                method: "POST",
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(user),
            }
        );

        const json = await res.json()
		register = JSON.stringify(json)
    }

    function back() {
        registered = false;
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

<h1>Registrarse</h1>
<section>
    <input type="text" bind:value={$name.value} placeholder="username"/>
    {#if $myForm.hasError('name.required')}
        <div>Name is required</div>
    {/if}
    <input type="password" bind:value={$password.value} placeholder="password"/>
    {#if $myForm.hasError('name.required')}
        <div>Password is required</div>
    {/if}
  
    <button disabled={!$myForm.valid} on:click={doRegister}>Registrarse</button>
</section>

<pre>
    {register}
</pre>
<button on:click={back}>Volver al Menu Principal</button>