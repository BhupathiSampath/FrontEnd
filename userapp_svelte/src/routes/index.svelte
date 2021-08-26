<script>
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
	  fetch("http://127.0.0.1:8000/dashboard")
	  .then(response => response.json())
	  .then(data => {
			console.log(data);
		apiData.set(data);
	  }).catch(error => {
		console.log(error);
		return [];
	  });
	});
	</script>
<head>
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.13.0/css/all.min.css">
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css" >
	<!-- //web font -->
</head>
	<!-- <nav class="navbar has-shadow is-dark">
		<a class="navbar-burger" id="burger">
			<span></span>
			<span></span>
			<span></span>
		</a>
		<div class="navbar-menu" id="nav-links">
			<div class="navbar-end">
				<a class="navbar-item" href="/#/registration">Register</a>
				<a class="navbar-item" href="/#/login">Login</a>
				<a class="navbar-item" href="/">About us</a>
				<a class="navbar-item" href="product">About product</a>
			</div>
		</div>
	</nav> -->
	<!-- <Router routes={{
		'/login': Login,
		'/registration': registration}} /> -->
	<div class="container"><h1 class="is-size-3 has-text-centered has-text-weight-bold">Dashboard</h1></div>
	<div class="table-container">
	<table class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth">
		<thead class="has-text-centered">
			<tr>
				<th rowspan="2">Username</th>
				<th rowspan="2">Date</th>
				
				<th rowspan="2">Total sequenced</th>
				<th rowspan="2">Sequenced last week</th>
				
				<th rowspan="2">Cumulative sequenced</th>
				<th colspan="3">Uploaded</th>
				<th rowspan="2">Any collaboration</th>
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
				<td>{data.username}</td>
				<td>{data.data_entry}</td>
				<td>{data.Total_sequenced}</td>
				<td>{data.Sequenced_last_week}</td>
				<td>{data.Cumulative_sequenced}</td>
				<td>{data.Uploaded_IGIB_SFTP}</td>
				<td>{data.Uploaded_NIBMG_DataHub}</td>
				<td>{data.Uploaded_GISAID}</td>
				<td>{data.Any_collaboration}</td>
			</tr>
			{/each}
		</tbody>
	</table>
	</div>
	
	
	
	