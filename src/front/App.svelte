<script>
	import Router from 'svelte-spa-router';

	import Home from './Home.svelte';   // Sera donde se pueda seleccionar a que API acceder 
	import NotFound from './NotFound.svelte';
	import about from './about.svelte';

	//Rutas de Marriages
	import globalMarriages from './MarriagesGUI/App.svelte'; // Sera donde se carga la tabla de datos 
	import EditMarriage from './MarriagesGUI/EditMarriage.svelte';
	import MarriagesChart from './MarriagesGUI/MarriagesChart.svelte';
	import MarriagesPieChart from './MarriagesGUI/MarriagesPieChart.svelte';
	import MarriagesIntegration26 from  './MarriagesGUI/Integration-26.svelte';
	import MarriagesIntegration21 from  './MarriagesGUI/Integration-21.svelte';
	import MarriagesIntegration05 from  './MarriagesGUI/Integration-05.svelte';
	import MarriagesIntegration01 from  './MarriagesGUI/Integration-01.svelte';
	import MarriagesIntegrationExt1 from  './MarriagesGUI/Integration-Ext-1.svelte';
	import MarriagesIntegrationExt2 from  './MarriagesGUI/Integration-Ext-2.svelte';

	//Rutas de Suicides
	import SuicidesTable from './global-suicides_GUI/App.svelte';
	import editSuicide from './global-suicides_GUI/editSuicide.svelte';
	import EmptyTable from './global-suicides_GUI/EmptyTable.svelte';
	import suicidesGraph from './global-suicides_GUI/global-suicides_Graph.svelte';
	import suicidesGraph2 from './global-suicides_GUI/global-suicides_Graph2.svelte';
	import integrations_suicides from './global-suicides_GUI/integrations_suicides.svelte';
	import integrations_suicides2 from './global-suicides_GUI/integrations_suicides2.svelte';
	import integrations_suicides3 from './global-suicides_GUI/integrations_suicides3.svelte';
	import integrations_suicides4 from './global-suicides_GUI/integrations_suicides4.svelte';
	import integrations from './integrations.svelte';
	import analytics from './analytics.svelte';
	import integrations_suicides_external from './global-suicides_GUI/integrations_suicides_external.svelte';
	import integrations_suicides_external2 from './global-suicides_GUI/integrations_suicides_external2.svelte';
	

		//Rutas de Divorces
	import globalDivorces from './DivorcesGUI/App.svelte';  
	import EditDivorce from './DivorcesGUI/EditDivorce.svelte';
	import DivorcesGraph from './DivorcesGUI/DivorcesGraph.svelte';
	import DivorcesGraph2 from './DivorcesGUI/DivorcesGraph2.svelte';
	
	import IntegrationsDivorce from './DivorcesGUI/Integrations/Integrations.svelte';

	import IntegrationsTransfers from './DivorcesGUI/Integrations/IntegrationsTransfers.svelte';
	import IntegrationsUnivregs from './DivorcesGUI/Integrations/IntegrationsUnivregs.svelte';
	import IntegrationsSugarConsume from './DivorcesGUI/Integrations/IntegrationsSugarConsume.svelte';
	import IntegrationsEnergy from './DivorcesGUI/Integrations/IntegrationsEnergy.svelte';
	import IntegrationsCompetitivity from './DivorcesGUI/Integrations/IntegrationsCompetivity.svelte';
	import IntegrationsNBA from './DivorcesGUI/Integrations/IntegrationsNBA.svelte';
	import IntegrationsINE from './DivorcesGUI/Integrations/IntegrationsINE.svelte';


	const routes = {
		"/": Home,
		"/global-marriages/:country/:year": EditMarriage,
		"/globalMarriagesAPI":globalMarriages,
		"/MarriagesChart":MarriagesChart,
		"/MarriagesPieChart":MarriagesPieChart,
		"/Marriages/Integration-26":MarriagesIntegration26,
		"/Marriages/Integration-21":MarriagesIntegration21,
		"/Marriages/Integration-01":MarriagesIntegration01,
		"/Marriages/Integration-05":MarriagesIntegration05,
		"/Marriages/Integration-Ext-1":MarriagesIntegrationExt1,
		"/Marriages/Integration-Ext-2":MarriagesIntegrationExt2,


		"/global-suicides_API" : SuicidesTable,
		"/suicide/:countryName": editSuicide,
		"/empty": EmptyTable,

		"/globalDivorcesAPI/:country/:year": EditDivorce,
		"/globalDivorcesAPI":globalDivorces,
		"/globalDivorcesAPI/DivorcesGraph": DivorcesGraph,
		"/globalDivorcesAPI/DivorcesGraph2": DivorcesGraph2,
		"/globalDivorcesAPI/Integrations": IntegrationsDivorce,

		"/globalDivorcesAPI/IntegrationsTransfers": IntegrationsTransfers,
		"/globalDivorcesAPI/IntegrationsUnivregs": IntegrationsUnivregs,
		"/globalDivorcesAPI/IntegrationsSugarConsume": IntegrationsSugarConsume,
		"/globalDivorcesAPI/IntegrationsEnergy": IntegrationsEnergy,
		"/globalDivorcesAPI/IntegrationsCompetitivity": IntegrationsCompetitivity,
		"/globalDivorcesAPI/IntegrationsNBA": IntegrationsNBA,
		"/globalDivorcesAPI/IntegrationsINE": IntegrationsINE,


		"/suicidesGraph": suicidesGraph, 
		"/suicidesGraph2": suicidesGraph2,
		"/integrations_suicides": integrations_suicides,
		"/integrations_suicides2": integrations_suicides2,
		"/integrations_suicides3": integrations_suicides3,
		"/integrations_suicides4": integrations_suicides4,
		"/integrations": integrations,
		"/analytics": analytics,
		"/integrations_suicides_external": integrations_suicides_external,
		"/integrations_suicides_external2": integrations_suicides_external2,
		"/about": about,
		
		"*": NotFound
	};
</script>

<main>
	<Router {routes} />
</main>