<script>
    // import {onMount} from 'svelte';
    // import { writable, derived } from 'svelte/store';
	// export const apiData = writable([]);
    // // let message = ''
    // export const Data = derived(apiData, ($apiData) => {
	//   if ($apiData.data){
	// 	return $apiData.data.map(username => username.username);
	// 	// return $apiData.data;
	//   }
	//   return [];
	// });
    // onMount(async () => {
    //     const response = await fetch('http://localhost:8000/api/userview', {
    //     // const response = await fetch('http://10.10.6.73/userview', {
    //     headers: {'Content-Type':'application/json'},
    //     credentials: 'include',
    //     })
    //     .then(response => response.json())
    //     .then(data => {
    //             console.log(data);
    //         apiData.set(data);
    //     }).catch(error => {
    //         console.log(error);
    //         return [];
    //     });
    //         // console.log(Data.username)
    //         // message = `${Data}`;
    // });

    import {onMount} from "svelte";
    let username = ''
    let is_prouser = ''
    onMount(async () => {
        const response1 = await fetch("http://localhost:8000/api/userview", {
            headers: {'Content-Type':'application/json'},
            credentials: 'include',
        })

        const content = await response1.json()
        // console.log(content.username)
        username =`${content.username}`,
        is_prouser =`${content.is_prouser}`;          
    });
</script>

{username}
{is_prouser}