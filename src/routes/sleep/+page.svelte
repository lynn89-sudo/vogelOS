<script>
    import { base } from "$app/paths";
    import Navbar from "$lib/navbar.svelte";

    import { onMount } from "svelte";

    let tutorial = $state(false)

    let score = $state(0);
    let days = $state(0);
    let average = $state(0)

    onMount(function() {
        if (localStorage.getItem("sleep/score") == null) {
            setTimeout(function() {tutorial = true;}, 2000)

            localStorage.setItem("sleep/score", 0);
            localStorage.setItem("sleep/days", 0);
            localStorage.setItem("sleep/average", 0);
            localStorage.setItem("sleep/sleeping", false);
        }
    })

    onMount(function() {
        score = localStorage.getItem("sleep/score");
        days = localStorage.getItem("sleep/days");
        average = localStorage.getItem("sleep/average");
    })


</script>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

    :global(body) {
        background-color: rgb(73, 48, 60);
        font-family: Montserrat;
        text-align: center;

        padding-left: 40px;
        padding-right: 40px;

        color: white;
    }

    #tutorial {
        position: absolute;
        z-index: 1000;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        background-color: rgba(55, 55, 99, 0.971);
        color: white;
        h1, h3 {
            margin-left: 20px;
            margin-right: 20px;
        }

        button {
            border-radius: 360px;
            border: none;
            cursor: pointer;
            span {
                vertical-align: -5px;
            }
        }
    }
    #content {
        background-color: rgb(88, 53, 73);
        padding: 20px;
        border-radius: 15px;
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
{#if tutorial}
    <div id="tutorial">
        <button style="position: absolute; top: 20px; right: 20px" onclick = {function() {tutorial = false; let montre = new Date(); localStorage.setItem("pinged", montre.getTime()/60000);}}><span class="material-symbols-outlined">cancel</span></button>
        <br><br>
        <h1>Using Sleep Tracker</h1>
        <h3><em>Track your hours of sleep and set reminders for when you wake up</em></h3>
        <br>
        <h5>Note: This website is in development and not all features are complete</h5>
    </div>
{/if}
<br>
<h1 style="font-weight: 800">SLEEP TRACKER</h1>
<span class="material-symbols-outlined" style="font-size: 80px; padding: 0;">hotel</span>
<br><br>
<div id="content">
    <h4 style="padding: 0px;">SLEEP SCORE</h4>
    <h1 style="padding: 0px; font-size: 50px">{score}</h1>
    <div id="deleteButton"><button onclick = { function() {window.location.href = `${base}/sleep/night/reminders`} }>Go to Sleep</button></div>
</div>


