<script>
    import { base } from "$app/paths";

    import { onMount } from "svelte";

    let tutorial = $state(false)

    let name = $state("");


    onMount(function() {
        name = localStorage.getItem("name");
        setTimeout(function() {
            document.body.style = `background-color: rgb(58, 140, 170);`; 
        }, 1500);
    })


</script>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&icon_names=arrow_circle_down,arrow_circle_right,auto_stories,cancel,guardian,heart_smile,help,home,hotel,info,lock_person,mode_heat,moon_stars,sunny,sync,timer,trophy" />
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

    :global(body) {
        background-color: rgb(0, 0, 0);
        transition: background-color 1s ease-in-out, color 1s ease-in-out;
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
<button id="back" onclick = {function() {window.location.href = `${base}/sleep/night/sleeping`}} title="Return"><span class="material-symbols-outlined">arrow_circle_right</span></button>
<h1 style="font-weight: 800">Good Morning</h1>
<h2>Rise and shine {name}</h2>
<br>
<div id="deleteButton"><button onclick = { function() {window.location.href = `${base}/sleep/morning/tasks`} }>Let's Go</button></div>



