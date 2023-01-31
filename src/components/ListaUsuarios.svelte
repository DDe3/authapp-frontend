<script>
	import SvelteTable from "svelte-table/src/SvelteTable.svelte";

	let rows = [];
	let remount= true;
	// define column configs
	let columns = []
	let username
	let result

	fetch('http://localhost:8081/apidistribuida/v1/clientes/all')
		.then(response => response.json())
		.then(json => {
		const data = json
		rows = json
		
		for (var i = 0; i < Object.keys(rows[0]).length; i++) {
			const key = Object.keys(rows[0])[i]
			columns.push({key, title: key, value: v => v[key], sortable: true})
		}
		
		remount = false;
		setTimeout(() => remount = true, 0);
	});

	async function doDelete() {
		const res = await fetch(
            `http://localhost:8081/apidistribuida/v1/clientes/${username}/delete`,
            {
                method: "PUT",
				headers: {
                    'Accept': 'application/json'
                },
            }
        ).then(r=>r.json());
		result = res
	}


</script>


{#if remount }
<SvelteTable columns="{columns}" rows="{rows}"></SvelteTable>
{/if}
<label for="name">Usuario</label>
<input type="text" id="name" bind:value={username} />
<button on:click={doDelete}> Eliminar usuario. </button>

<br>
<br>
<pre>
    {result}
</pre>