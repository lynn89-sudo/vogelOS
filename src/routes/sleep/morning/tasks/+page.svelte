<script>
    import { base } from "$app/paths";
    import { onMount } from "svelte";

    let tutorial = $state(false)

    let name = $state("");


    onMount(function() {
        name = localStorage.getItem("name");
        localStorage.setItem("sleep/sleeping", false);
        let days = localStorage.getItem("sleep/days");
        localStorage.setItem("sleep/days", (parseInt(days)+1));
        let score = localStorage.getItem("sleep/score");
        localStorage.setItem("sleep/score", (parseInt(score)+50));
    })


</script>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&icon_names=arrow_circle_down,arrow_circle_right,auto_stories,cancel,guardian,heart_smile,help,home,hotel,info,lock_person,mode_heat,moon_stars,sunny,sync,timer,trophy" />
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

    :global(body) {
       background-color: rgb(58, 140, 170);
        font-family: Montserrat;
        text-align: center;

        padding-left: 40px;
        padding-right: 40px;

        color: white;
    }

    #content {
        background-color: rgb(53, 63, 88);
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
<br>
<h1 style="font-weight: 800">TO-DO</h1>
<h2>Let's get some tasks done {name}</h2>
<br>
<div id="content">
    <h2><em>Feature coming soon</em></h2>
</div>
<br><br>
<div id="deleteButton"><button onclick = { function() {window.location.href = `${base}/`} }>All done!</button></div>



