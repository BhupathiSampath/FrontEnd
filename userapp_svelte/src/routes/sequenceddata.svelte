<script>

    // import id from './update.svelte'
    // // import { handleErrors } from "../shared.js";
    import {onMount} from "svelte";

    let username = ''
    let is_prouser = ''
    // let user = { is_prouser: false };
    onMount(async () => {
        const response1 = await fetch("http://localhost:8000/api/userview", {
            headers: {'Content-Type':'application/json'},
            credentials: 'include',
        })

        const content = await response1.json()
        // console.log(content)
        username =`${content.username}`,
        is_prouser =`${content.is_prouser}`;
        console.log(content);       
    });


    import {goto} from "$app/navigation"
    // import user from './data.svelte'

    let Total_sequenced = '', Sequenced_last_week ='', Uploaded_IGIB_SFTP ='',Uploaded_NIBMG_DataHub ='',Uploaded_GISAID ='',Any_collaboration =''

    const submit = async () => {
        await fetch('http://localhost:8000/api/SequenceUpload', {
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
// ________________homeview_________________________
    // import {onMount} from 'svelte';
	import { writable, derived } from 'svelte/store';
	export const apiData = writable([]);
	
	export const Data = derived(apiData, ($apiData) => {
	  if ($apiData.data){
		// return $apiData.data.map(username => username.username);
		return $apiData.data;
	  }
	  return [];
	});
    onMount(async () => {
        // const response = await fetch('http://127.0.0.1:8000/userview', {
        const response = await fetch('http://localhost:8000/api/homeview', {
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
            // console.log(content)
    });



</script>


    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css" >
        <title>User Data</title>
        
    </head>
    {#if is_prouser === 'true'}
        <div class="section">
            <div class="cloumns">
            <div class="column">
            <div class="box">
                <p class="title is-4 has-text-centered">
                    Upload your sequences here.
                </p>
                <form on:submit|preventDefault={submit}>
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
                                    <button class="button is-fullwidth  is-primary" type="submit">Submit</button>
                                </div>
                            </div>  
                </form>
            </div>
            </div>
        </div>

            <div class="box">
            <div class="column">
            
            <!-- <section class="hero"> -->
                <!-- <div class="hero-body"> -->
                    <div class="table-container">
                        <p class="title is-4 has-text-centered">
                            Your sequences are here.
                        </p>
                        <table class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth">
                        <thead id="head" class="has-text-centered">
                            <tr>
                            <th rowspan="2">ID</th>
                            <th rowspan="2">Date</th>
                            <!-- <th rowspan="2">Username</th> -->
                            <th rowspan="2">Total sequenced</th>
                            <th rowspan="2">Sequenced last week</th>
                            
                            <th rowspan="2">Cumulative sequenced</th>
                            <th colspan="3">Uploaded</th>
                            <th rowspan="2">Any collaboration</th>
                            <th rowspan="2">Action</th>
                            </tr>
                            <tr>
                                <th>IGIB SFTP</th>
                                <th>NIBMG DataHub</th>
                                <th>GISAID</th>
                                
                            </tr>
                        </thead>
                        <tbody>
                            {#each $Data as data}
                            <tr>
                                <th scope="row">{data.id}</th>
                                <td>{data.data_entry}</td>
                                <!-- <td>{{data.username}}</td> -->
                                <td>{data.Total_sequenced}</td>
                                <td>{data.Sequenced_last_week}</td>
                                <td>{data.Cumulative_sequenced}</td>
                                <td>{data.Uploaded_IGIB_SFTP}</td>
                                <td>{data.Uploaded_NIBMG_DataHub}</td>
                                <td>{data.Uploaded_GISAID}</td>
                                <td>{data.Any_collaboration}</td>
                                <td><a href={`/blog/${data.id}`}>Update</a>
                                </td>
                                <td>
            
                                    <div>
                                            <!-- <form action={url 'update' data.id}> -->
                                                <!-- {% csrf_token %} --> 
                                                <!-- <button class="tag is-primary">Update</button>  -->
                                                <!-- <input class="is-success" id="pointer" type="submit" value="update"> -->
                                                <!-- <a href="/update">Update</a> -->
                                            <!-- </form> -->
                                            <!-- <form action="{% url 'delete' data.id %}" method="POST">
                                                {% csrf_token %} -->
                                                <button class="tag is-danger">Delete</button>
                                                <!-- <input id="pointer" type="submit" value="delete" -->
                                                <!-- > -->
                                            <!-- </form> -->
                                    </div>
                                </td>
                            </tr>
                            {/each}
                        </tbody>
                    </table>
            <!-- </div> -->
        <!-- </section> -->
        </div>
        </div>
    </div>
    </div>
    {:else}

        <div class="container">
            <h1 class="has-text-centered">Welcome to Account Management system.</h1>
            <h2 class="has-text-centered">Please upgrade your account to upload your sequenced data.</h2>
            <!-- <h3 class="title is-4 has-text-centered">Upgrade your Account</h3> -->
            <!-- <div class="box"> -->
                <!-- <div class="container"> -->
                    <form>
                        <!-- <div class="column is-4">
                            <input bind:value={Sequenced_last_week} class="hidden" type="number" name="Sequenced_last_week"  required="required" hidden >                                
                        </div>  -->
                        <!-- <fieldset class="text">
                            <legend class="text"></legend>
                            <input class="text" type="text" name="is_prouser" value="True" required=""><br>
                        </fieldset> -->
                        <div class="column is-2 has-text-centered container">
                            <button class="button is-fullwidth  is-primary" type="submit"><a href={`/blog1/${username}`}>Update</a></button>
                        </div>
                    </form>
                </div>
            <!-- </div> -->
        <!-- </div> -->

    {/if}