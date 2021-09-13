<!-- <script>
    import { page } from '$app/stores';
</script>
{$page.params.slug} -->

<script>
import { page } from "$app/stores";
import {goto} from "$app/navigation"
        // import { handleErrors } from "../shared.js";
        import {onMount} from "svelte";
    let username = ''
    onMount(async () => {
        const response1 = await fetch("http://localhost:8000/api/userview", {
            headers: {'Content-Type':'application/json'},
            credentials: 'include',
        })

        const content = await response1.json()
        // console.log(content)
        username =`${content.username}`;          
    });
    export let id = $page.params.slug;
    let Total_sequenced = '', Sequenced_last_week ='', Uploaded_IGIB_SFTP ='',Uploaded_NIBMG_DataHub ='',Uploaded_GISAID ='',Any_collaboration =''

    const editdata = async () => {
        await fetch(`http://localhost:8000/api/updatedata/${id}`, {
            method : 'PUT',
            method : 'POST',
            headers : {'content-type':'application/json'},
            credentials : 'include',
            body : JSON.stringify({
                username,
                Total_sequenced,
                Sequenced_last_week,
                Uploaded_IGIB_SFTP,
                Uploaded_NIBMG_DataHub,
                Uploaded_GISAID,
                Any_collaboration
            })
        });
        await goto("/sequenceddata")
    };
</script>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
<div class="section">
    <div class="column">
    <div class="box">
        <h1 class="title is-4">Update your data here</h1>
                <form on:submit|preventDefault={editdata}>
                            <div class="columns is-centered mb-0">
                                <div class="column is-4">
                                    <input type="hidden" class="input" name='username' bind:value={username} hidden>
                                        <div class="column">
                                            <!-- svelte-ignore a11y-label-has-associated-control -->
                                            <label>Total sequenced:</label>
                                            <input bind:value={Total_sequenced} class="input" type="number" name="Total_sequenced"  required="required">                                
                                        </div>
                                        <div class="column">
                                            <!-- svelte-ignore a11y-label-has-associated-control -->
                                            <label class="lable">Last week:</label>
                                            <input bind:value={Sequenced_last_week} class="input" type="number" name="Sequenced_last_week"  required="required">                                
                                        </div>                            
                                
                                    
                                        <div class="column">
                                            <!-- svelte-ignore a11y-label-has-associated-control -->
                                            <label class="lable">IGIB SFTP:</label>
                                            <input bind:value={Uploaded_IGIB_SFTP} class="input" type="number" name="Uploaded_IGIB_SFTP"  required="required">                                
                                        </div>
                                    </div>
                                    <div class="column is-4">
                                        <div class="column">
                                            <!-- svelte-ignore a11y-label-has-associated-control -->
                                            <label class="lable">NIBMG DataHub:</label>
                                            <input bind:value={Uploaded_NIBMG_DataHub} class="input" type="number" name="Uploaded_NIBMG_DataHub"  required="required">                                
                                        </div>
                                        <div class="column">
                                            <!-- svelte-ignore a11y-label-has-associated-control -->
                                            <label class="lable">GISAID:</label>
                                            <input bind:value={Uploaded_GISAID} class="input" type="number" name="Uploaded_GISAID"  required="required">                                
                                        </div>    
                                        <div class="column">
                                            <label for="lable">Any collaboration:</label>
                                            <input bind:value={Any_collaboration} class="input" id="lable" type="text" name="Any_collaboration"  required="required">                                
                                        </div>
    
                                </div>
                            </div>
    
                            <div class="column is-4 is-offset-4 mt-0 pt-0">
                                <div class="column">
                                    <button class="button is-fullwidth  is-primary">Update</button>
                                </div>
                            </div>
                            <!-- </div>   -->
                </form>
            </div>
        </div>
    </div>