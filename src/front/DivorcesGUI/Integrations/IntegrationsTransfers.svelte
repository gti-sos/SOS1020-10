<script>

import Button from "sveltestrap/src/Button.svelte";
import  {pop} from "svelte-spa-router";



async function loadGraph(){


    const raw_data1 = await fetch("/api/v2/global-divorces");
    const raw_data2 = await fetch("/api/v3/global-transfers");

    let data = await raw_data1.json();
    let data2 = await raw_data2.json();


    let countries = Array.from(new Set(data.map((d) => {return d.country+" "+d.year;})));
    let divorces = Array.from(new Set(data.map((d) => {return d.divorce;})));


   

    let teams = Array.from(new Set(data2.map(t => {return t.team + " " + t.year;})));
    let signing = Array.from(new Set(data2.map(t => {return t.signing;})));

    let teams_countries =teams.concat(countries);

     var salto = [];
    for(var i = 0; i<teams.length;i++){
        salto[i] = 0;
    }
    divorces = salto.concat(divorces);
    
    console.log("ARRAY "+teams_countries);


    
   

    Highcharts.chart('container', {
    chart: {
        type: 'column'
    },
    title: {
        text: 'Número de divorcios por paises y fichajes por equipo de fútbol'
    },
    subtitle: {
        text: 'Para visualizar los datos de los fichajes desactive los divorcios.'
    },
    xAxis: {
        categories: teams_countries,
        crosshair: true
    },
    yAxis: {
     //   tickInterval: 10,
        min: 0,
        title: {
            text: 'Nº de divorcios y de fichajes'
        }
    },
    tooltip: {
        headerFormat: '<span style="font-size:10px">{point.key}</span><table>',
        pointFormat: '<tr><td style="color:{series.color};padding:0">{series.name}: </td>' +
            '<td style="padding:0"><b>{point.y:.0f} </b></td></tr>',
        footerFormat: '</table>',
        shared: true,
        useHTML: true
    },
    plotOptions: {
        column: {
            pointPadding: 0.2,
            borderWidth: 0
        }
    },
    series: [{
        name:'Número de Divorcios',
        data: divorces
    },
    {
        name: 'Número de fichajes',
        data: signing
    }
    
    ],
});
}


</script>

<svelte:head><script src="https://code.highcharts.com/highcharts.js"></script>
<script src="https://code.highcharts.com/highcharts.js"></script>
<script src="https://code.highcharts.com/modules/exporting.js"></script>
<script src="https://code.highcharts.com/modules/export-data.js"></script>
<script src="https://code.highcharts.com/modules/accessibility.js" on:load = "{loadGraph}"></script>
</svelte:head>



<main>
    <h2>Integración API Fichajes</h2>

    <figure class="highcharts-figure">
        <div id="container"></div>
        <p class="highcharts-description">
            Gráfico de columnas que compara el número de divorcios por paises y años con el número de ficahjes de equipos de fútbol.
            Estos datos no tienen ningún tipo de relación. 
            Debido al alto número de divorcios, los fichajes no se aprecian en la gráfica, por lo que para visualizarlos hay que
            desactivar los divorcios de la gráfica pinchando en número de divorcios.
        </p>
    </figure>
    <div>
<Button outline color="secondary" on:click="{pop}" > <i class="fas fa-arrow-circle-left"></i> Atrás </Button>
</div>
</main>

<style>.highcharts-figure, .highcharts-data-table table {
    min-width: 310px; 
    max-width: 900px;
    margin: 1em auto;
}

#container {
    height: 700px;
}

.highcharts-data-table table {
	font-family: Verdana, sans-serif;
	border-collapse: collapse;
	border: 1px solid #EBEBEB;
	margin: 10px auto;
	text-align: center;
	width: 100%;
	max-width: 500px;
}
.highcharts-data-table caption {
    padding: 1em 0;
    font-size: 1.2em;
    color: #555;
}
.highcharts-data-table th {
	font-weight: 600;
    padding: 0.5em;
}
.highcharts-data-table td, .highcharts-data-table th, .highcharts-data-table caption {
    padding: 0.5em;
}
.highcharts-data-table thead tr, .highcharts-data-table tr:nth-child(even) {
    background: #f8f8f8;
}
.highcharts-data-table tr:hover {
    background: #f1f7ff;
}
</style>