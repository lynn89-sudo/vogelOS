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
    let name = $state("");
    //console.log(clock.getHours());

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
        if (clock.getHours() < 10) {
            //sky.background = "skies/night.png";
        }
    })

    onMount(function() {
        name = localStorage.getItem("name");
        document.getElementById("title").classList.remove("init");
    })
</script>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');


    :global(body) {
        background-color: rgb(217, 157, 166);
        font-family: Montserrat;
        text-align: center;
    }
    #sky {
        position: absolute;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        z-index: -1000;
    }
    #title.init {
        opacity: 0;
    }
    #title {
        opacity: 1;
        transition: opacity 2s ease-in-out;
    }
</style>
<Navbar />
<div id="sky" alt="Sky Background"></div>
<h1 id="title" class="init">{ greeting } <span style="color: purple">{ name }</span>!</h1>