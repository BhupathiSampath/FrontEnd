<script>
    import {goto} from "$app/navigation"
import { post } from "./todos/index.json";
    let email ='', password =''

    const submit = async () => {
        // await fetch('http://10.10.6.73/loginview', {
            await fetch("http://localhost:8000/api/login/", {
            method: 'POST',
            headers: {'Content-Type':'application/json'},
            credentials: 'include',
            // credentials: true,
            body: JSON.stringify({
                email,
                password
            })
            
        });

        await goto("/sequenceddata");
    }

    
</script>
<div class="container">
    <form on:submit|preventDefault={submit} class="box" style="margin-bottom: 10px; box-sizing: border-box;">
        <h1>Login here</h1><br>
        <div class="field">
        <!-- svelte-ignore a11y-label-has-associated-control -->
        <label class="label">Email</label>
        <div class="control">
            <input bind:value={email} class="input" type="email" name="email" placeholder="e.g. alex@example.com" required="required">
        </div>
        </div>
    
        <div class="field">
        <!-- svelte-ignore a11y-label-has-associated-control -->
        <label class="label">Password</label>
        
        <div class="control">
            <input bind:value={password} class="input" id="id_password" type="password" name="password" placeholder="********"  required="required">
            <i class="far fa-eye-slash" id="togglePassword" ></i>
        </div>
        </div>
        <div class="column is-fullwidth"><button class="button is-primary is-fullwidth" type="submit">Sign in</button></div>
        <div>Don't have an account? <a href="/Registration">Register</a></div>
    </form>
</div>


<style>
    .container {
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    /* top: 200px; */
    /* bottom: 200px; */
    /* border-style:hidden; */
    /* border-style: double; */
    /* position: absolute; */
}
i{
    position: absolute;
    right: 15px;
    transform: translate(0,50%);
    top: 15%;
    cursor: pointer;
}
</style>
<!-- <script>
    const togglePassword = document.querySelector('#togglePassword');
      const password = document.querySelector('#id_password');

    togglePassword.addEventListener('click', function (e) {
        // toggle the type attribute
        const type = password.getAttribute('type') === 'password' ? 'text' : 'password';
        const icon = type == 'password' ? 'far fa-eye-slash' : 'far fa-eye'
        password.setAttribute('type', type);
        // toggle the eye slash icon
        togglePassword.className = icon
});
</script> -->