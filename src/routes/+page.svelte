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
    let streakAdd = $state("days");

    onMount(function() {
        let clock = new Date();
        let sky = document.getElementById("sky");
        if (clock.getHours() < 7 || clock.getHours() > 18) {
            document.body.style = `background-color: black; color: white;`;
            document.getElementById("nameTitle").style = "color: pink";

            if (clock.getHours() < 7) {
                greeting2 = "Good morning";
                document.getElementById("streakIcon").innerText = "sunny"
            }
            else {
                greeting2 = "Good evening";

                if (clock.getHours() > 21) {
                    greeting2 = "You should sleep soon";
                }
            }
        }
        else {
            document.body.style = `background-color: skyblue; color: navy`;
            if (clock.getHours() < 12) {
                greeting2 = "Good morning";
                document.getElementById("streakIcon").innerText = "sunny"
            }
            else {
                greeting2 = "Good afternoon";
                document.getElementById("streakIcon").innerText = "sunny"
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
</script>
<!-- svelte-ignore css_unused_selector -->
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

</style>
<Navbar />
{#if !loaded}
    <div id="screenLoading" class="init">
        <h2 style="margin-top: 100px;">Loading...</h2>
        <span class="material-symbols-outlined">sync</span>
        <h5><em>Spreading birdseed on the ground to feed the vogels...</em></h5>
    </div>
{/if}
<br>
<div id="sky" style="" alt="Sky Background"></div>
<h1 id="title" class="init">{ greeting } <span id="nameTitle" style="">{ name }</span>!</h1>
<h3 id="greeting" style="margin-top: 0">{ greeting2 }</h3>
<h1><span id="streakIcon" class="material-symbols-outlined" style="font-size: 110px; margin-bottom: 0; padding-bottom: 0;">moon_stars</span></h1>
<h1 id="streakDisplay" style="margin-top: 0;" class="init">{ streak } { streakAdd }</h1>
<div id="tasks">
    <h3>Next Task</h3>
    <h5><em>Nothing for now</em></h5>
</div>
<div id="forest"><h1>[forest goes here]</h1></div>