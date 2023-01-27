<script>
    import { user } from "../js/store.js";

    let userInput;

	user.subscribe(value => {
		userInput = value;
	});

    let result = "Ingresa tus credenciales"; 
    export let logged;

    async function doLogin() {
        const res = await fetch(
            "http://localhost:8081/apidistribuida/v1/clientes/authenticate",
            {
                method: "POST",
                headers: {
                    'Accept': 'application/json',
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify($user),
            }
        );

        const json = await res.json()
		result = JSON.stringify(json)
        if (result.includes("Autenticado")) {
            logged = true
        }
    }



</script>

<h1>Log In</h1>
<label for="name">Usuario</label>
<input type="text" id="name" bind:value={userInput.username} />
<label for="">Contraseña</label>
<input type="password" id="password" bind:value={userInput.password} />
<pre>
    {result}
</pre>
<button on:click={doLogin}> Iniciar sesión. </button>

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
