<script>
    import {goto} from "$app/navigation"
    let username ='', email ='', password ='', password2 =''

    const submit = async () => {
        await fetch('http://127.0.0.1:8000/registerview', {
            method : 'POST',
            headers : {'content-type':'application/json'},
            body : JSON.stringify({
                username,
                email,
                password,
                password2
            })
        });

        // await goto("/Login")
    }

    
</script>

<div class="container">
    <form on:submit|preventDefault={submit} class="box">
        <!-- {% csrf_token %} -->
        <h1>Register here</h1><br>
        <div class="field">
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label class="label">Username</label>
            <div class="control">
                <input bind:value={username} class="input" type="text" name="username" placeholder="username" required="required">
            </div>
        </div>
        <div class="field">
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label class="label">Email</label>
            <div class="control">
                <input bind:value={email} class="input" type="email" name="email" placeholder="Email" required="required">
            </div>
        </div>
        <div class="field">
        <!-- svelte-ignore a11y-label-has-associated-control -->
        <label class="label">Password</label>
        <div class="control">
            <input bind:value={password} class="input" id="id_password" type="password" name="password1" placeholder="Password"  required="required">
            <i class="far fa-eye-slash" id="togglePassword" ></i>
        </div>
        </div>
        <div class="field">
            <!-- svelte-ignore a11y-label-has-associated-control -->
            <label class="label">Confirm Password</label>
            <div class="control">
                <input bind:value={password2} class="input" id="is_password" type="password" name="password2" placeholder="Confirm Password" required="required">
                <i class="far fa-eye-slash" id="togglePassword1" ></i>
            </div>
        </div>
        <div class="column is-fullwidth"><button class="button is-primary is-fullwidth">SIGNUP</button></div>
        <div>Already have an account? <a href="/Login">Login here</a></div>
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
<!-- 
<script>
    let togglePassword = document.querySelector('#togglePassword');
    let password = document.querySelector('#id_password');
    
    togglePassword.addEventListener('click', function (e) {
        // toggle the type attribute
        let type = password.getAttribute('type') === 'password' ? 'text' : 'password';
        const icon = type == 'password' ? 'far fa-eye-slash' : 'far fa-eye'
        password.setAttribute('type', type);
        // toggle the eye slash icon
        togglePassword.className = icon
    });
    
    const togglePassword1 = document.querySelector('#togglePassword1');
      const password1 = document.querySelector('#is_password');
    
    togglePassword1.addEventListener('click', function (e) {
        // toggle the type attribute
        const type = password1.getAttribute('type') === 'password' ? 'text' : 'password';
        const icon = type == 'password' ? 'far fa-eye-slash' : 'far fa-eye'
        password1.setAttribute('type', type);
        // toggle the eye slash icon
        togglePassword1.className = icon
    });
</script> -->