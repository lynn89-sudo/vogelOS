<script>
    import { base } from "$app/paths";
    import Navbar from "$lib/navbar.svelte";

    import { onMount } from "svelte";

    let name = $state("");
    let streak = $state(0);
    let streakAdd = $state("days");

    onMount(function() {
        name = localStorage.getItem("name");
        streak = localStorage.getItem("streak");
        if (streak == 1) {
            streakAdd = "day";
        }
    });

    let nameEntered = $state(false);
    let inputed = $state("");

    $effect(function() {
        nameEntered = inputed.trim() !== "";
    });

    function processInput() {
        if (nameEntered) {
            localStorage.setItem("name", inputed); 
            window.location.href = `${base}/account`;
        }
    }

</script>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0&icon_names=lock_person" />
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

    :global(body) {
        background-color: rgb(91, 90, 164);
        font-family: Montserrat;
        text-align: center;

        padding-left: 40px;
        padding-right: 40px;

        color: white;
    }
    .faq {
        background-color: rgb(40, 40, 88);
        padding: 20px;
        border-radius: 100px;
        transition: box-shadow 0.5s ease-in-out;
        margin-bottom: 50px;
    }
    .faq:hover {
        box-shadow: 0px 10px 0px 10px rgba(0, 0, 0, 0.785);
    }
</style>
<Navbar />
<br>
<h1 style="font-weight: 800">FAQ</h1>
<span class="material-symbols-outlined" style="font-size: 80px;">
info
</span>
<br><br><br>
<div class="faq">
    <h3>What's the counter on my home page and account manager?</h3>
    <h4>VogelOS does not count your progress with a streak system. Instead, the counter signifies the amount of days, since starting, that you've made your personalized goals!</h4>
    <span class="material-symbols-outlined" style="font-size: 30px;">mode_heat</span>
</div>
<div class="faq">
    <h3>How are my personalized goals set?</h3>
    <h4>VogelOS collects data on your sleep patterns and daily habits, then pushes you to gradually improve your habits.</h4>
    <span class="material-symbols-outlined" style="font-size: 30px;">heart_smile</span>
</div>

