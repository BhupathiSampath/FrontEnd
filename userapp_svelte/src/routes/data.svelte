<script>
    import {onMount} from 'svelte';
    import { writable, derived } from 'svelte/store';
	export const apiData = writable([]);
    // let message = ''
    export const Data = derived(apiData, ($apiData) => {
	  if ($apiData.data){
		return $apiData.data.map(username => username.username);
		// return $apiData.data;
	  }
	  return [];
	});
    onMount(async () => {
        const response = await fetch('http://localhost:8000/userview', {
        // const response = await fetch('http://10.10.6.73/userview', {
        headers: {'Content-Type':'application/json'},
        credentials: 'include',
        })
        .then(response => response.json())
        .then(data => {
                console.log(data);
            apiData.set(data);
        }).catch(error => {
            console.log(error);
            return [];
        });
            // console.log(Data.username)
            // message = `${Data}`;
    });
</script>

{#each $Data as data}
		<li>{data}</li>
{/each}