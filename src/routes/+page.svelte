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
    //console.log(clock.getHours());

    let streak = $state(0);

    onMount(function() {
        if (localStorage.getItem("accountCreated") == null || localStorage.getItem("accountCreated") == "false") {
            window.location.href = `${base}/create`;
        }
        else {
            console.log(localStorage.getItem("accountCreated") == false);
        }
    }) 

    onMount(function() {
        let clock = new Date();
        let sky = document.getElementById("sky");
        if (clock.getHours() < 7 || clock.getHours() > 18) {
            document.body.style = `background-color: black; color: white;`;
            document.getElementById("nameTitle").style = "color: pink";

            if (clock.getHours() < 7) {
                greeting2 = "Good morning";
            }
            else {
                greeting2 = "Good evening";
                document.getElementById("streakIcon").innerText = "emergency_heat"
            }
        }
        else {
            document.body.style = `background-color: skyblue; color: navy`;
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
    })
</script>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');


    :global(body) {
        background-color: rgb(217, 157, 166);
        font-family: Montserrat;
        text-align: center;
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
    }

    #streakDisplay.init {
        
        opacity: 0;
        transform: rotate(4deg);
    }
    #streakDisplay {
        opacity: 1;
        transition: opacity 1s;
    }
</style>
<Navbar />
<div id="sky" style="" alt="Sky Background"></div>
<h1 id="title" class="init">{ greeting } <span id="nameTitle" style="">{ name }</span>!</h1>
<h3 id="greeting" style="margin-top: 0">{ greeting2 }</h3>
<h1><span id="streakIcon" class="material-symbols-outlined" style="font-size: 110px; margin-bottom: 0; padding-bottom: 0;">mode_heat</span></h1>
<h1 id="streakDisplay" style="margin-top: 0;" class="init">{ streak }</h1>
<div id="forest"><h1>[forest goes here]</h1></div>