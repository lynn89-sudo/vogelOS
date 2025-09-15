<script>
    let vogels = ["imke", "eefje"];
    let vogel = $state(vogels[Math.floor(Math.random()*2)])

    import { base } from "$app/paths";
    function nav (route) {
        if (route == 1) {
            window.location.href = `${base}/`;
        }
        if (route == 2) {
            window.location.href = `${base}/account`;
        }
    }

    import { onMount } from "svelte";
    onMount(function() {
        setTimeout(function() {
            document.getElementById("buttons").classList.remove("init");
            document.getElementById("vogel").classList.remove("init");
            document.getElementById("navbar").classList.remove("init");
        }, 1000)
    })

    onMount(function() {
        if (localStorage.getItem("accountCreated") == null || localStorage.getItem("accountCreated") == "false") {
            window.location.href = `${base}/create`;
        }
        else {
            
        }
    }) 
</script>
<style>
    #navbar {
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        height: 70px;
        background-color: rgba(207, 156, 164, 0.679);
        color: white;
        cursor: pointer;
        transition: background-color 0.5s;

        overflow: hidden;

        #vogel {
            display: inline-block;
            position: relative;
            right: 0;
            margin-top: 5px;
            width: 80px;
            transition: margin-top 1.5s;

        }

        #buttons {
            position: absolute;
            top: -100%;
            left: 50%;
            transform: translate(-50%, -50%);
            transition: opacity 1.5s, top 1.3s;

            button {
                background-color: rgb(109, 44, 92);
                color: white;
                border: pink;
                cursor: pointer;
                padding: 7px;
                border-radius: 360px;
                transition: padding 0.3s, background-color 1s;
            }
            button:hover {
                padding: 10px;
                background-color: rgb(80, 2, 63);
            }
        }
        #buttons.init {
            display: block;
            top: 20%;
        }
        #vogel.init {
            margin-top: 80px;
        }
    }
    #navbar:hover {
        background-color: rgba(207, 156, 164, 0.911);
        #vogel {
            margin-top: 80px;
        }
        #buttons {
            display: block;
            top: 20%;
        }
    }
    #navbar.init {
        background-color: rgba(207, 156, 164, 0.911);
    }
    #spacing {
        height: 70px;
    }
</style>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&icon_names=arrow_circle_down,emergency_heat,guardian,home,lock_person,mode_heat,moon_stars,sunny" />
<div id="navbar" class="init">
    <h1 id="buttons" class="init">
        <button class="material-symbols-outlined" onclick = {nav(1)}>home</button>
        <button class="material-symbols-outlined" onclick = {nav(2)}>guardian</button>
    </h1>
    <img id="vogel" class="init" src="vogels/{ vogel }.png" alt="Bird"/>

</div>
<div id="spacing"></div>