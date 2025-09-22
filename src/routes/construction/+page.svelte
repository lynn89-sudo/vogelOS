<script>
    import { base } from "$app/paths";
    import { onMount } from "svelte";

    onMount(
        function() {
            setTimeout(function() {window.location.href = `${base}/`;}, 3500)
        }
    )
</script>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');

    :global(body) {
        background-color: rgb(73, 48, 60);
        font-family: Montserrat;
        text-align: center;

        padding-left: 40px;
        padding-right: 40px;

        color: white;
    }
</style>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&icon_names=build_circle" />
<br>
<h1 style="font-weight: 800">UNDER CONSTRUCTION</h1>
<h3><em>This page is under development and is not yet ready</em></h3>
<br>
<span class="material-symbols-outlined" style="font-size: 100px;">
build_circle
</span>
<br>
<h3>You are being re-directed to the homepage</h3>


