<script>
    import { base } from "$app/paths";
    import Navbar from "$lib/navbar.svelte";

    import { onMount } from "svelte";

    onMount(function() {
        if (localStorage.length == 0) {
            window.location.href = `${base}/create`;
        }
    });
    
    function deleteAll() {
        for (let i = 0; i < localStorage.length; i++) {
            let key = localStorage.key(i);
            localStorage.removeItem(key);

            i--;
        }

        document.getElementById("deleteLabel").innerHTML = "<em>All data stored on this browser has been deleted. You will have to create a new account or upload a save file to continue using this website.</em>"
        document.getElementById("deleteButton").innerHTML = ""
    }
</script>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0&icon_names=lock_person" />
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

    :global(body) {
        background-color: rgb(86, 62, 88);
        font-family: Montserrat;
        text-align: center;

        padding-left: 40px;
        padding-right: 40px;

        color: white;
    }

    button {
        font-family: Montserrat;
        padding: 10px;
        border-radius: 20px;
        cursor: pointer;
        font-weight: 800;
    }
</style>
<Navbar />
<br>
<h1 style="font-weight: 800">Data Privacy and Storage</h1>
<h3 style="font-weight: 500">All data on VogelOS is stored locally, in your browser</h3>
<span class="material-symbols-outlined" style="font-size: 80px; background-color: rgb(187, 128, 255); padding: 20px; border-radius: 360px;">
lock_person
</span>
<br><br><br>
<h4>All your data on this website is stored locally on your browser's storage. Unless you insert userscripts into webpages on this app, your data will remain on the computer. To delete all data for this app from your browser, use the button at the bottom of this page.</h4>
<br><br>
<h5 id="deleteLabel">Click here to delete all data stored on the browser</h5>
<div id="deleteButton"><button onclick = { deleteAll }>Delete All</button></div>

