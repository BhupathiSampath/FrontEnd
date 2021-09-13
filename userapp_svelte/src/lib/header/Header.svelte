<script>
	import {onMount} from 'svelte'
    onMount(() => {
        const burgerIcon = document.querySelector('#burger')
        const navbarMenu = document.querySelector('#nav-links')
        burgerIcon.addEventListener('click', () => {
          navbarMenu.classList.toggle('is-active');
        });
  });
	import { page } from '$app/stores';
	// import { authenticated } from "/home/icgc_sub/Desktop/svelteproject/userapp_svelte/src/lib/header/stores/auth.js";
	// // import {authenticated} from '/home/icgc_sub/Desktop/svelteproject/userapp_svelte/src/stores/auth.js'
	// let auth = false;
	// authenticated.subscribe(a => auth = a);
	import {goto} from "$app/navigation"
    // let email ='', password =''

    const logout = async () => {
        await fetch('http://localhost:8000/api/logoutview', {
            method: 'POST',
            headers: {'Content-Type':'application/json'},
            credentials: 'include',
        });
        await goto("/")
    }
</script>
<head>
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.13.0/css/all.min.css">
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css" >
	<!-- //web font -->
	</head>
	<nav class="navbar has-shadow">
		<a class="navbar-burger" id="burger">
			<span></span>
			<span></span>
			<span></span>
		</a>
		<div class="navbar-menu" id="nav-links">
			<div class="navbar-end">
				
				<!-- <ul> -->
					<a class:active={$page.path === '/Registration'} class="navbar-item" sveltekit:prefetch href="/Registration">Register</a>
					<a class:active={$page.path === '/Login'} class="navbar-item" sveltekit:prefetch href="/Login">Login</a>
					<a href="/#/" class="navbar-item" on:click={logout}>Logout</a>
					<a class:active={$page.path === '/'} class="navbar-item" sveltekit:prefetch href="/">Dashboard</a>
					<a class:active={$page.path === '/sequenceddata'} class="navbar-item" sveltekit:prefetch href="/sequenceddata">Home</a>
					<!-- <a class="navbar-item" href="product">About product</a>
					<a class="navbar-item" class:active={$page.path === '/'} sveltekit:prefetch href="/">Home</a>
					<a class:active={$page.path === '/about'} sveltekit:prefetch href="/about">About</a>
					<a class:active={$page.path === '/todos'} sveltekit:prefetch href="/todos">Todos</a> -->
				<!-- </ul> -->
					
		</div>
	</nav>
<!-- <header>
	<div class="corner">
		<a href="https://kit.svelte.dev">
			<img src={logo} alt="SvelteKit" />
		</a>
	</div>

	<nav>
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L1,2 C1.5,3 1.5,3 2,3 L2,0 Z" />
		</svg>
		<ul>
			<li class:active={$page.path === '/'}><a sveltekit:prefetch href="/">Home</a></li>
			<li class:active={$page.path === '/about'}><a sveltekit:prefetch href="/about">About</a></li>
			<li class:active={$page.path === '/todos'}><a sveltekit:prefetch href="/todos">Todos</a></li>
		</ul>
		<svg viewBox="0 0 2 3" aria-hidden="true">
			<path d="M0,0 L0,3 C0.5,3 0.5,3 1,2 L2,0 Z" />
		</svg>
	</nav>

	<div class="corner">
		TODO put something else here? github link?
	</div>
</header> -->

<!-- <style>
	header {
		display: flex;
		justify-content: space-between;
	}

	.corner {
		width: 3em;
		height: 3em;
	}

	.corner a {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100%;
	}

	.corner img {
		width: 2em;
		height: 2em;
		object-fit: contain;
	}

	nav {
		display: flex;
		justify-content: center;
		--background: rgba(255, 255, 255, 0.7);
	}

	svg {
		width: 2em;
		height: 3em;
		display: block;
	}

	path {
		fill: var(--background);
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: var(--background);
		background-size: contain;
	}

	li {
		position: relative;
		height: 100%;
	}

	li.active::before {
		--size: 6px;
		content: '';
		width: 0;
		height: 0;
		position: absolute;
		top: 0;
		left: calc(50% - var(--size));
		border: var(--size) solid transparent;
		border-top: var(--size) solid var(--accent-color);
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 1em;
		color: var(--heading-color);
		font-weight: 700;
		font-size: 0.8rem;
		text-transform: uppercase;
		letter-spacing: 10%;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--accent-color);
	}
</style> -->
