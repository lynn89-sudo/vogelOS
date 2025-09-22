<script>
    import { onMount } from "svelte";
    import { base } from "$app/paths";
    import Navbar from "$lib/navbar.svelte";

    let greetings = [
        "Hoi",
        "Hallo",
        "Hey",
        "Welcome"
    ]
    let greeting = greetings[Math.floor((Math.random()*4))]
    let greeting2 = $state("");
    let name = $state("");
    let day = $state(false);
    //console.log(clock.getHours());

    let tutorial = $state(false);

    let streak = $state(0);
    let streakAdd = $state("days");

    let buttonSelect = $state(0);
    let buttonSelect_title = $state("");
    let buttonSelect_desc = $state("");
    let buttonSelect_path = $state("");
    $effect(function() {
        if (buttonSelect == 1) {
            buttonSelect_title = "Sleep";
            buttonSelect_desc = "Log your sleep: track sleep hours and set reminders for the morning";
            buttonSelect_path = "sleep";
        }
        else if (buttonSelect == 2) {
            buttonSelect_title = "Logs";
            buttonSelect_desc = "Log for different activities: exercise, test grades, volunteering, and more";
            buttonSelect_path = "construction";
        }
        else if (buttonSelect == 3) {
            buttonSelect_title = "Pomodoro Timer";
            buttonSelect_desc = "Better manage your time and boost productivity";
            buttonSelect_path = "construction";
        }
    });

    onMount(function() {
        let clock = new Date();
        let sky = document.getElementById("sky");
        if (clock.getHours() < 7 || clock.getHours() > 18) {
            document.body.style = `background-color: black; color: white;`;
            document.getElementById("nameTitle").style = "color: pink";
            if (clock.getHours() < 7) {
                greeting2 = "You should sleep";
            }
            else {
                greeting2 = "Good evening";
            }

            if (clock.getHours() > 21) {
                greeting2 = "You should sleep soon";
            }
        }
        else {
            document.body.style = `background-color: skyblue; color: navy`;
            day = true;
            document.getElementById("streakIcon").innerText = "sunny"
            if (clock.getHours() < 12) {
                greeting2 = "Good morning";
            }
            else {
                greeting2 = "Good afternoon";
            }
        }
    })

    onMount(function() {
        name = localStorage.getItem("name");
        document.getElementById("title").classList.remove("init");
        document.getElementById("streakDisplay").classList.remove("init");
    })

    onMount(function() {
        streak = localStorage.getItem("streak");
        if (streak == 1) {
            streakAdd = "day";
        }
    })

    let loaded = $state(false);
    onMount(function() {
        setTimeout(function() {
            document.getElementById("screenLoading").classList.remove("init")
        }, 700);
        setTimeout(function() {
            loaded = true;
        }, 1500);
    })

    onMount(function() {
        if (localStorage.getItem("origin") == localStorage.getItem("pinged")) {
            setTimeout(function() {tutorial = true;}, 3000);
        }
    })
</script>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');


    :global(body) {
        background-color: rgb(217, 157, 166);
        font-family: Montserrat;
        text-align: center;
    }

    @keyframes spin {
        0% {
            transform: rotate(0deg);
        }
        50% {
            transform: rotate(180deg);
        }
        100% {
            transform: rotate(360deg)
        }
    }
    #title.init {
        opacity: 0;
    }
    #title {
        opacity: 1;
        transition: opacity 2s ease-in-out;
        margin-bottom: 0;

        user-select: none;
        -webkit-user-drag: none;
        -moz-user-select: none;
    }
    #nameTitle {
        color: rgb(6, 67, 210);
    }

    #forest {
        position: absolute;
        bottom: 0;
        right: 0;
        left: 0;
        height: 150px;
        background-color: darkcyan;
        z-index: 999;

        opacity: 0.5;
    }

    #streakDisplay.init {
        
        opacity: 0;
        transform: rotate(4deg);
    }
    #streakDisplay {
        opacity: 1;
        transition: opacity 1s;
    }
    
    #screenLoading {
        opacity: 0;
        transition: opacity 0.4s ease-in-out;

        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;

        background-color: rgb(84, 45, 84);
        color: white;
        z-index: 1000;

        .material-symbols-outlined {
            font-size: 70px; 
            animation: spin 1s infinite;
        }

        h5 {
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translate(-50%, -50%);

        }
    }
    #screenLoading.init {
        opacity: 1;
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

            font-family: Montserrat;
            padding: 10px;
            border-radius: 20px;
            font-weight: 800;
            border: none;
            cursor: pointer;
            span {
                vertical-align: -5px;
            }
        }
    }

    #buttons {
        button {
            background-color: rgb(107, 97, 105);
            color: white;
            border: none;
            cursor: pointer;
            padding: 7px;
            border-radius: 360px;
            transition: font-size 0.2s ease-in-out, background-color 0.5s;
        }
        button.on {
            background-color: rgb(181, 112, 167);
        }
    }
    #buttons.day {
        button {
            background-color: rgb(36, 13, 101);
        }
        button.on {
            background-color: rgb(112, 121, 181);
        }
    }
    #buttonDesc {
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 0;

        visibility: collapse;
        opacity: 0;
        transition: visibility 1s, opacity 1.4s;
        button {
            background-color: rgb(110, 101, 108);
            color: white;
            border: none;
            cursor: pointer;
            padding: 7px;
            vertical-align: -3px;
            margin-left: 5px;
            border-radius: 360px;
            transition: font-size 0.2s ease-in-out, background-color 0.5s;
            display: inline-block;
        }
        button:hover {
            background-color: rgb(181, 112, 167);
        }
    }
    #buttonDesc.on {
        visibility: visible;
        opacity: 1;
    }
    #buttonDesc.day {
        button {
            background-color: rgb(36, 13, 101);
        }
        button:hover {
            background-color: rgb(112, 121, 181);
        }
    }

</style>
<Navbar />
{#if !loaded}
    <div id="screenLoading" class="init">
        <h2 style="margin-top: 100px;">Loading...</h2>
        <span class="material-symbols-outlined">sync</span>
        <h5><em>Spreading birdseed on the ground to feed the vogels...</em></h5>
    </div>
{/if}
{#if tutorial}
    <div id="tutorial">
        <button style="position: absolute; top: 20px; right: 20px" onclick = {function() {tutorial = false; let montre = new Date(); localStorage.setItem("pinged", montre.getTime());}}><span class="material-symbols-outlined">cancel</span></button>
        <br><br>
        <h1>Welcome to VogelOS</h1>
        <h3><em>Track your personal accomplishments, reinforce good habits, and watch your virtual forest grow</em></h3>
        <br>
        <h5>Note: This website is in development and not all features are complete</h5>
    </div>
{/if}
<br>
<div id="sky" style=""></div>
<h1 id="title" class="init">{ greeting } <span id="nameTitle" style="">{ name }</span>!</h1>
<h3 id="greeting" style="margin-top: 0">{ greeting2 }</h3>
<h1><span id="streakIcon" class="material-symbols-outlined" style="font-size: 80px; margin-bottom: 0; padding-bottom: 0;">moon_stars</span></h1>
<h2 id="streakDisplay" style="margin-top: 0;" class="init">{ streak } { streakAdd }</h2>
<h1 id="buttons" class:day = {day}>
    <button class="material-symbols-outlined" class:on = {buttonSelect == 1} onclick = {function() {buttonSelect = 1;}}>hotel</button>
    <button class="material-symbols-outlined" class:on = {buttonSelect == 2} onclick = {function() {buttonSelect = 2;}}>auto_stories</button>
    <button class="material-symbols-outlined" class:on = {buttonSelect == 3} onclick = {function() {buttonSelect = 3;}}>timer</button>
</h1>
<div id="buttonDesc" class:on = { buttonSelect != 0 } class:day = {day}>
    <h3>{buttonSelect_title} <button class="material-symbols-outlined" onclick = {function() {window.location.href = `${base}/${buttonSelect_path}`}}>arrow_circle_right</button></h3>
    <h5><em>{buttonSelect_desc}</em></h5>
</div>
<div id="forest"><h1>[forest goes here - in dev]</h1></div>