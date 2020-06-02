<script>

import Button from "sveltestrap/src/Button.svelte";
import  {pop} from "svelte-spa-router";

</script>

<main>
	
    <h2>Enlace a los vídeos del grupo SOS1920-10</h2>
    <Button color="info" on:click="{pop}">Atrás</Button>
    <p></p>
    <iframe width="560" height="315" src="https://youtu.be/-W06s122NXA"  allowfullscreen></iframe>

</main>