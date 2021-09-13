<script>
    import { page } from "$app/stores";
    import {goto} from "$app/navigation"
            // import { handleErrors } from "../shared.js";
        //     import {onMount} from "svelte";
        // let username = ''
        // onMount(async () => {
        //     const response1 = await fetch("http://localhost:8000/api/userview", {
        //         headers: {'Content-Type':'application/json'},
        //         credentials: 'include',
        //     })
    
        //     const content = await response1.json()
        //     // console.log(content)
        //     username =`${content.username}`;          
        // });
        export let username = $page.params.upgrade;
        let is_prouser = 'true'
    
        const upgradeAccount = async () => {
            await fetch(`http://localhost:8000/api/UpgradeAccount/${username}`, {
                method : 'PUT',
                method : 'POST',
                headers : {'content-type':'application/json'},
                credentials : 'include',
                body : JSON.stringify({
                   is_prouser,
                })
            });
            await goto("/sequenceddata")
        };
    </script>

<div class="container">
    <h1 class="has-text-centered">Welcome to Account Management system.</h1>
    <h2 class="has-text-centered">Please upgrade your account to upload your sequenced data.</h2>
    <!-- <h3 class="title is-4 has-text-centered">Upgrade your Account</h3> -->
    <!-- <div class="box"> -->
        <!-- <div class="container"> -->
    <form on:submit|preventDefault={upgradeAccount}>
        <div class="container">
        <div class="column is-4">
            <input bind:value={is_prouser} class="text" type="text" name="Sequenced_last_week" required="required">                                
        </div> 
        <!-- <fieldset class="text">
            <legend class="text"></legend>
            <input class="text" type="text" name="is_prouser" value="True" required=""><br>
        </fieldset> -->
        <div class="column is-2 has-text-centered container">
            <button class="button is-fullwidth  is-primary">Update</button>
        </div>
    </div>
    </form>
</div>