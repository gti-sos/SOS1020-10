<script>import Button from "sveltestrap/src/Button.svelte";
import  {pop} from "svelte-spa-router";</script>
<main>
<h1 align= "center">Integraciones</h1>
	<div align= "center" class="div-home">
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsTransfers'">Int. G26</button>
        <button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsUnivregs'">Int. G24</button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsSugarConsume'"> Int. G30</button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsEnergy'">Int. G09</button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsCompetitivity'"> Int. G25</button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsNBA'"> Int. Ext. NBA </button>
		<button type="button"   class="btn btn-success"  onclick="window.location.href='#/globalDivorcesAPI/IntegrationsINE'"> Int. Ext. INE </button>


	</div>
	<div align="center"><Button style="margin-top: 10px;" outline color="secondary" on:click="{pop}" > <i class="fas fa-arrow-circle-left"></i> Atrás </Button>
</div>
</main>