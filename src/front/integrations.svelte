<script>

 import Button from "sveltestrap/src/Button.svelte";
 import  {pop} from "svelte-spa-router";

</script>

<main>
	
    <h2>Integraciones del grupo SOS1920-10</h2>
    <Button color="info" on:click="{pop}">Atrás</Button>
	<body>

	<p></p>
    <p></p>
    <p></p>
    <h4>Integraciones de Suicidios Globales</h4>
	<div class="div-home">
		<button type="button"   class="btn btn-primary"  onclick="window.location.href='#/integrations_suicides'">Int. G02</button>
		<button type="button"   class="btn btn-primary"  onclick="window.location.href='#/integrations_suicides2'">Int. G01</button>
        <button type="button"   class="btn btn-primary"  onclick="window.location.href='#/integrations_suicides3'">Int. G26</button>
        <button type="button"   class="btn btn-primary"  onclick="window.location.href='#/integrations_suicides4'">Int. G22</button>
        <button type="button"   class="btn btn-primary"  onclick="window.location.href='#/integrations_suicides_external'">Int. Ext_1</button>
        <button type="button"   class="btn btn-primary"  onclick="window.location.href='#/integrations_suicides_external2'">Int. Ext_2</button>
    </div>
    


    <p></p>
    <p></p>
    <h4>Integraciones de Matrimonios Globales</h4>
	<div class="div-home">
		<button type="button"   class="btn btn-danger"  onclick="window.location.href='#/Marriages/Integration-01'">Int. G01</button>
		<button type="button"   class="btn btn-danger"  onclick="window.location.href='#/Marriages/Integration-05'">Int. G05</button>
        <button type="button"   class="btn btn-danger"  onclick="window.location.href='#/Marriages/Integration-21'">Int. G21</button>
        <button type="button"   class="btn btn-danger"  onclick="window.location.href='#/Marriages/Integration-26'">Int. G26</button>
        <button type="button"   class="btn btn-danger"  onclick="window.location.href='#/Marriages/Integration-Ext-1'">Int. Ext_1</button>
        <button type="button"   class="btn btn-danger"  onclick="window.location.href='#/Marriages/Integration-Ext-2'">Int. Ext_2</button>
	</div>
    <p></p>
    <p></p>
    <h4>Integraciones de Divorcios Globales</h4>
    <div class="div-home">
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsTransfers'">Int. G26</button>
        <button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsUnivregs'">Int. G24</button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsSugarConsume'"> Int. G30</button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsEnergy'">Int. G09</button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsCompetitivity'"> Int. G25</button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsNBA'"> Int. Ext. NBA </button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsINE'"> Int. Ext. INE </button>


	</div>

</body>
</main>