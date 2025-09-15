<script>
    import { base } from "$app/paths";
    import Navbar from "$lib/navbar.svelte";

    import { onMount } from "svelte";

    let name = $state("");
    let streak = $state(0);
    let streakAdd = $state("days");

    onMount(function() {
        name = localStorage.getItem("name");
        streak = localStorage.getItem("streak");
        if (streak == 1) {
            streakAdd = "day";
        }
    });

    let nameEntered = $state(false);
    let inputed = $state("");

    $effect(function() {
        nameEntered = inputed.trim() !== "";
    });

    function processInput() {
        if (nameEntered) {
            localStorage.setItem("name", inputed); 
            window.location.href = `${base}/account`;
        }
    }

</script>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0&icon_names=lock_person" />
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

    :global(body) {
        background-color: rgb(56, 24, 32);
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

    #submitInput {
        font-weight: 800;
        opacity: 0;
    }
    #submitInput.visible {
        opacity: 1;
    }

    input {
        font-family: Montserrat;
        padding: 10px;
        border-radius: 20px;
        cursor: pointer;
        margin-top: 20px;
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
<br>
<div id="innerInput">
    <form onsubmit={ function() {processInput()} }>
        <input type = "text" id="nameInput" placeholder="Change your name" aria-placeholder="Input box to enter a name to create the user account" bind:value = { inputed }> 
        <br><input type="submit" id="submitInput" class:visible={ nameEntered } value="Looks good!">
    </form>
</div>
<br><br>
<h3>_______</h3><br>
<div style="background-color: rgb(119, 30, 51); border-radius: 50px; text-align: center; padding: 10px; width: 60%; margin-left: 20%; margin-right: 20%;">
    <h1><span id="streakIcon" class="material-symbols-outlined" style="font-size: 50px; margin-bottom: 0; padding-bottom: 0;">mode_heat</span></h1>
    <h1 id="streakDisplay" style="margin-top: 0;" class="init"><span style="padding: 10px; border-radius: 360px;">{ streak } { streakAdd }</span></h1>
</div>
