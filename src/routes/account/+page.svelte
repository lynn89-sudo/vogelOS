<script>
    import { base } from "$app/paths";
    import Navbar from "$lib/navbar.svelte";

    import { onMount } from "svelte";

    let name = $state("");

    onMount(function() {
        name = localStorage.getItem("name");
    });

</script>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0&icon_names=lock_person" />
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

    :global(body) {
        background-color: rgb(76, 33, 43);
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
<h1 style="font-weight: 800">ACCOUNT HOME</h1>
<h3 style="font-weight: 500">This account is under the name { name }</h3>
<span class="material-symbols-outlined" style="font-size: 80px;">
guardian
</span>
<br><br><br>
<div id="deleteButton"><button onclick = { function() {window.location.href = `${base}/privacy`} }>Privacy Information & Delete Account</button></div>

