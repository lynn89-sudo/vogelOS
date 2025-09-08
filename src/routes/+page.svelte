<script>
    import { onMount } from "svelte";
    import { base } from "$app/paths";

    onMount(function() {
        if (localStorage.getItem("accountCreated") == null || localStorage.getItem("accountCreated") == "false") {
            window.location.href = `${base}/create`;
        }
        else {
            console.log(localStorage.getItem("accountCreated") == false);
        }
    }) 
</script>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap');


    :global(body) {
        background-color: lightpink;
        font-family: Montserrat;
        text-align: center;
    }
</style>

<h1>logged in</h1>
<h3>This page does not work yet</h3>