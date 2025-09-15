<script>
    let vogels = ["imke", "eefje"];
    let vogel = $state(vogels[Math.floor(Math.random()*2)])

    import { base } from "$app/paths";
    function nav (route) {
        if (route == 1) {
            window.location.href = `${base}/`
        }
    }
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
    }
    #navbar:hover {
        #vogel {
            margin-top: 80px;
        }
        #buttons {
            display: block;
            top: 20%;
        }
    }
    #spacing {
        height: 70px;
    }
</style>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&icon_names=arrow_circle_down,emergency_heat,guardian,home,lock_person,mode_heat" />
<div id="navbar">
    <h1 id="buttons">
        <button class="material-symbols-outlined" onclick = {nav(1)}>home</button>
        <button class="material-symbols-outlined">guardian</button>
    </h1>
    <img id="vogel" src="vogels/{ vogel }.png" alt="Bird"/>

</div>
<div id="spacing"></div>