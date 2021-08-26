<script>
    import {onMount} from 'svelte';
    
    onMount(async () => {
        const response = await fetch('http://127.0.0.1:8000/userview', {
        headers: {'Content-Type':'application/json'},
        credentials: 'include',
        });
        
        const content = await response.json();
        console.log(content)
    });
    
    </script>