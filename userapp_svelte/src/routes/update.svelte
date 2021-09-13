<script>
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
    // import SidebarNav from "../components/SidebarNav.svelte";
	import { navigate } from "svelte-routing";
    // let localToken = localStorage.getItem("token")
    export let id;
    let Total_sequenced;
    let Sequenced_last_week;
    let Uploaded_IGIB_SFTP;
    let Uploaded_NIBMG_DataHub;
    let Uploaded_GISAID;
    let Any_collaboration;
    // onMount(() => {
    //     getdata();
    // });
    // async function getdata() {
    //     await fetch(`http://localhost:8000/api/updatedata/${id}/`, {
    //         method: "GET",
    //         headers: {'Content-Type':'application/json'},
    //         credentials: 'include',
    //         })
    //     .then(handleErrors)
    //     .then(response => response.json())
    //     .then(data => {
    //         Total_sequenced = data.Total_sequenced;
    //         Sequenced_last_week = data.Sequenced_last_week;
    //         Uploaded_IGIB_SFTP = data.Uploaded_IGIB_SFTP;
    //         Uploaded_NIBMG_DataHub = data.Uploaded_NIBMG_DataHub;
    //         Uploaded_GISAID = data.Uploaded_GISAID;
    //         Any_collaboration = data.Any_collaboration;
    //     });
    // }
    async function editdata() {
        let postObj = {
            "username": username,
            "Total_sequenced": Total_sequenced,
            "Sequenced_last_week": Sequenced_last_week,
            "Uploaded_IGIB_SFTP": Uploaded_IGIB_SFTP,
            "Uploaded_NIBMG_DataHub": Uploaded_NIBMG_DataHub,
            "Uploaded_GISAID": Uploaded_GISAID,
            "Any_collaboration": Any_collaboration
        };
        await fetch(`http://localhost:8000/api/updatedata/${id}/`, {
            method: "PUT",
            method : 'POST',
            headers : {'content-type':'application/json'},
            credentials : 'include',
            body: JSON.stringify(postObj)
        })
        .then(handleErrors)
        .then(response => response.json())
        .then(response => navigate(`/data/${response.id}`, { replace: true }))
    }
</script>




<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.9.3/css/bulma.min.css">
    <title>Update</title>
</head>
<body>
    
    <div class="container">
                <form >
                    <h1><b>Update your data here</b></h1>
                            <div class="columns is-centered mb-0">
                                <div class="column is-6">
                                        <input type="hidden" class="input" name="username" value="sampath" hidden>
                                    <div class="column">
                                        <label>Total sequenced:</label>
                                        <input class="input" type="number" name="Total_sequenced"  required="required">                                
                                    </div>
                                    <div class="column">
                                        <label class="lable">Last week:</label>
                                        <input class="input" type="number" name="Sequenced_last_week"  required="required">                                
                                    </div>                            
                            
                                
                                    <div class="column">
                                        <label class="lable">IGIB SFTP:</label>
                                        <input class="input" type="number" name="Uploaded_IGIB_SFTP"  required="required">                                
                                    </div>
                                </div>
                                <div class="column is-6">
                                    <div class="column">
                                        <label class="lable">NIBMG DataHub:</label>
                                        <input class="input" type="number" name="Uploaded_NIBMG_DataHub"  required="required">                                
                                    </div>
                                    <div class="column">
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
                                    <button on:click={editdata} class="button is-fullwidth  is-primary">Update</button>
                                </div>
                            </div>
                            <!-- </div>   -->
                </form>
            </div>
</body>
</html>