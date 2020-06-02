<script>

import Button from "sveltestrap/src/Button.svelte";
import  {pop} from "svelte-spa-router";



async function loadGraph(){


    const raw_data1 = await fetch("/api/v2/global-divorces");
    const raw_data2 = await fetch("https://free-nba.p.rapidapi.com/stats?page=0&per_page=25", {
	"method": "GET",
	"headers": {
		"x-rapidapi-host": "free-nba.p.rapidapi.com",
		"x-rapidapi-key": "a840bd129amshc11fafac1946f1fp1bbcd7jsn69488be18e23"
	}
});

    

    let data = await raw_data1.json();
    let data2 = await raw_data2.json();
    console.log(data2);

    let countries = Array.from(new Set(data.map((d) => {return d.country+" "+d.year;})));
    let divorces = Array.from(new Set(data.map((d) => {return d.divorce;})));

    let datas = data2["data"];
    let players = [];
    let pts = [];
    
    for(var i = 0; i<datas.length; i++){
        let obj = datas[i]["player"];
        players[i] = obj["first_name"];
        pts[i]= datas[i]["pts"];


    }
    let obj = datas[2]["team"]["full_name"];
    let obj1 = datas[20]["team"][["full_name"]];
    let play = obj+" - "+obj1;

    let players_countries =players.concat(countries);

     var salto = [];
    for(var i = 0; i<players.length;i++){
        salto[i] = 0;
    }
    divorces = salto.concat(divorces);
    


    
   

    Highcharts.chart('container', {
    chart: {
        type: 'column'
    },
    title: {
        text: 'Número de divorcios por paises y puntos anotados por cada jugador del partido '+play+' de la NBA'
    },
    subtitle: {
        text: 'Para visualizar uno de los datos solo seleccione el campo a eliminar.'
    },
    xAxis: {
        categories: players_countries,
        crosshair: true
    },
    yAxis: {
     //   tickInterval: 10,
        min: 0,
        title: {
            text: 'Nº de divorcios y puntos anotados por cada jugador del partido '+play+' de la NBA'
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
        name: 'Puntos anotados por cada jugador en el partido '+play,
        data: pts
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
    <h2>Integración API Externa NBA</h2>

    <figure class="highcharts-figure">
        <div id="container"></div>
        <p class="highcharts-description">
            Gráfico de columnas que compara el número de divorcios por paises y puntos anotados por cada jugador en un partido de la nba.
            Estos datos no tienen ningún tipo de relación. Para visualizar los puntos elimine los datos de divorcios de la tabla. 
        
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