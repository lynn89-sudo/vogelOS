<script>
    import { onMount } from "svelte";
    import { base } from "$app/paths";

    import Navbar from "$lib/navbar.svelte";
    import { error } from "@sveltejs/kit";

    let name = $state("");
	let nameEntered = $state(false);

    $effect(function() {
        nameEntered = name.trim() !== "";
    });

    onMount(function() {
        localStorage.setItem("accountCreated", false);
        setTimeout(function() {
            document.getElementById("content").classList.remove("invisible");
        }, 2000);
        setTimeout(function() {
            document.getElementById("mask").classList.remove("on");
        }, 3000);
    });

    function processInput(set) {
        if (set == 1) {
            localStorage.setItem("name", name);
            document.getElementById("innercontent").innerHTML = `
            <h3>Personal Questions</h3>
                <form onsubmit={ function() { processInput(2) } }>
                    <label for="sleepInput">How many hours of sleep on average do you get each night?</label><br>
                    <input type="number" id="sleepInput" min=0 max=24 style="font-family: Montserrat; padding: 10px; border-radius: 20px; cursor: pointer; margin-top: 20px; margin-bottom: 20px;" required>
                    <br><input type=submit style=" padding: 10px; border-radius: 20px; cursor: pointer; font-family: Montserrat; font-weight: 800;" value="Done!">
                </form>
            `;
        }
        else {

        }
    }
</script>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0&icon_names=arrow_circle_down,guardian" />
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

    :global(body) {
       background-color: rgb(86, 62, 88);
        font-family: Montserrat;
        text-align: center;

        color: white;

        a {
            color: white;
        }
    }

    input {
        font-family: Montserrat;
        padding: 10px;
        border-radius: 20px;
        cursor: pointer;
        margin-top: 20px;
    }

    @keyframes welcome {
        0% {
            font-size: 30px;
        }
        50% {
            font-size: 50px;
            transform: rotate(5deg);
        }
        100% {
            font-size: 30px;
            transform: rotate(0deg);
        }
    }

    #welcome {
        color: rgb(236, 150, 161);
    }


    #welcome span {
        display: inline-block;
        animation: welcome 3s ease-in-out;
    }

    #welcome span:nth-child(2) { animation-delay: 0.1s; }
    #welcome span:nth-child(3) { animation-delay: 0.2s; }
    #welcome span:nth-child(4) { animation-delay: 0.3s; }
    #welcome span:nth-child(5) { animation-delay: 0.4s; }
    #welcome span:nth-child(6) { animation-delay: 0.5s; }
    #welcome span:nth-child(7) { animation-delay: 0.6s; }


    #content {
        opacity: 1;
        transition: opacity 2s;
    }
    #content.invisible {
        opacity: 0;
    }

    #mask {
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        opacity: 0;
        display: none;

        user-select: none;
        -webkit-user-drag: none;
        -moz-user-select: none;
    }
    #mask.on {
        display: block;
    }
    .material-symbols-outlined {
        font-size: 50px;
    }

    @keyframes pulse {
        0% {
            font-size: 30px;
        }
        50% {
            font-size: 35px;
        }
        100% {
            font-size: 30px;
        }
    }

    #arrow {
        animation: pulse infinite 3s ease-in-out;
    }

    #submitInput {
        font-weight: 800;
        opacity: 0;
    }
    #submitInput.visible {
        opacity: 1;
    }

</style>

<div id="mask" class="on"><h1>Mask</h1></div>
<Navbar/>
<br>
<h1 id="welcome"><span>w</span><span>e</span><span>l</span><span>c</span><span>o</span><span>m</span><span>e</span></h1>
<br>
<div id="content" class="invisible">
    <span class="material-symbols-outlined">
    guardian
    </span>
    <h3 style="margin-bottom: 0;">Let's make you an account</h3>
    <h5 style="margin-top: 0;"><em>All data is stored locally on this device. <a href="{ base }/privacy">Learn More</a></em></h5>
    <span class="material-symbols-outlined" id="arrow">
    arrow_circle_down
    </span>
    <br><br>
    <div id="innercontent">
        <form onsubmit={ function() {processInput(1)} }>
            <input type = "text" id="nameInput" placeholder="What's your name?" aria-placeholder="Input box to enter a name to create the user account" bind:value = { name }> 
            <br><input type="submit" id="submitInput" class:visible={ nameEntered } value="Lets Go!">
        </form>
    </div>
</div>