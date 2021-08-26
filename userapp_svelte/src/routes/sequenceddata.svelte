<script>
import {onMount} from 'svelte';

onMount(async () => {
    const response = await fetch('http://127.0.0.1:8000/homeview', {
    headers: {'Content-Type':'application/json'},
    credentials: 'include',
    });
    
    const content = await response.json();
    console.log(content)
});

</script>

<!-- <script>
	// import Router from 'svelte-spa-router';
	// import registration from './registration.svelte'
	import { onMount } from "svelte";
	import { writable, derived } from 'svelte/store';
	// import Login from './login.svelte';
	
	/** Store for your data. 
	This assumes the data you're pulling back will be an array.
	If it's going to be an object, default this to an empty object.
	**/
	export const apiData = writable([]);
	
	/** Data transformation.
	For our use case, we only care about the drink names, not the other information.
	Here, we'll create a derived store to hold the drink names.
	**/
	export const Data = derived(apiData, ($apiData) => {
	  if ($apiData.data){
		// return $apiData.data.map(username => username.username);
		return $apiData.data;
	  }
	  return [];
	});
	onMount(async () => {
	  fetch("http://127.0.0.1:8000/homeview",  {
    headers : {'content-type':'application/json'},
    credentials : 'include',
    })
	  .then(response => response.json())
	  .then(data => {
			console.log(data);
		apiData.set(data);
	  }).catch(error => {
		console.log(error);
		return [];
	  });
	});
	</script> -->


<html lang="en">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Data</title>
    
</head>
<body>


    <div class="box">
        <h1>Upload your sequenced data here.</h1>
            <form action="upload" method="post">
                        <div class="columns is-centered mb-0">
                            <div class="column is-4">
                                    <input type="hidden" class="input" name="username">
                                <div class="column">
                                    <!-- svelte-ignore a11y-label-has-associated-control -->
                                    <label>Total sequenced:</label>
                                    <input class="input" type="number" name="Total_sequenced"  required="required">                                
                                </div>
                                <div class="column">
                                    <!-- svelte-ignore a11y-label-has-associated-control -->
                                    <label class="lable">Last week:</label>
                                    <input class="input" type="number" name="Sequenced_last_week"  required="required">                                
                                </div>                            
                        
                            
                                <div class="column">
                                    <!-- svelte-ignore a11y-label-has-associated-control -->
                                    <label class="lable">IGIB SFTP:</label>
                                    <input class="input" type="number" name="Uploaded_IGIB_SFTP"  required="required">                                
                                </div>
                            </div>
                            <div class="column is-4">
                                <div class="column">
                                    <!-- svelte-ignore a11y-label-has-associated-control -->
                                    <label class="lable">NIBMG DataHub:</label>
                                    <input class="input" type="number" name="Uploaded_NIBMG_DataHub"  required="required">                                
                                </div>
                                <div class="column">
                                    <!-- svelte-ignore a11y-label-has-associated-control -->
                                    <label class="lable">GISAID:</label>
                                    <input class="input" type="number" name="Uploaded_GISAID"  required="required">                                
                                </div>    
                                <div class="column">
                                    <label for="lable">Any collaboration:</label>
                                    <input class="input" id="lable" type="text" name="Any_collaboration"  required="required">                                
                                </div>

                            </div>
                        </div>

                        <div class="column is-4 is-offset-4 mt-0 pt-0">
                            <div class="column">
                                <button class="button is-fullwidth  is-primary">Submit</button>
                            </div>
                        </div>  
            </form>
        </div>
        <section class="hero">
            <div class="hero-body">
                <div class="table-container">
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
                        {#each $content as data}
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
                            <td>
        
                                <div style="width:100px;">
                                        <!-- <form action="{% url 'update' data.id %}" method="">
                                            {% csrf_token %} -->
                                            <input id="pointer" type="submit" value="update">
                                        <!-- </form> -->
                                        <!-- <form action="{% url 'delete' data.id %}" method="POST">
                                            {% csrf_token %} -->
                                            <input id="pointer" type="submit" value="delete"
                                            style="background-color: crimson; font:bold;">
                                        <!-- </form> -->
                                </div>
                            </td>
                        </tr>
                        {/each}
                    </tbody>
                </table>
        </div>
    </section>
</body>
</html>