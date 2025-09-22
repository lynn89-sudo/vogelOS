<script>
    import { base } from "$app/paths";

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

    function sleep() {
        let clock = new Date();
        localStorage.setItem("pinged", (clock.getTime()))
        localStorage.setItem("sleep/sleeping", true);
        window.location.href = `${base}/sleep/night/sleeping`
    }
</script>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&icon_names=arrow_circle_down,arrow_circle_right,auto_stories,cancel,guardian,heart_smile,help,home,hotel,info,lock_person,mode_heat,moon_stars,sunny,sync,timer,trophy" />
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
    button#back {

        border-radius: 360px;
        border: none;
        cursor: pointer;
        position: absolute;
        top: 15px;
        left: 15px;
        span {
            vertical-align: -5px;
            transform: rotate(180deg);
        }
    }
</style>
<br>
<button id="back" onclick = {function() {window.location.href = `${base}/sleep`}} title="Return"><span class="material-symbols-outlined">arrow_circle_right</span></button>
<h1 style="font-weight: 800">SET REMINDERS</h1>
<h2>You can set reminders or a to-do list for when you wake up</h2>
<br>
<div id="content">
    <h2><em>Feature coming soon</em></h2>
    <div id="deleteButton"><button onclick = { sleep }>Go to Sleep</button></div>
</div>


