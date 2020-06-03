<script>

import Button from "sveltestrap/src/Button.svelte";
import  {pop} from "svelte-spa-router";



async function loadGraph(){


    const raw_data1 = await fetch("/api/v2/global-divorces");
    const raw_data2 = await fetch("https://servicios.ine.es/wstempus/js/es/DATOS_TABLA/t20/p274/serie/prov/p02/02006.px?tip=AM", {
	"method": "GET"
});

    

    let data = await raw_data1.json();
    let data2 = await raw_data2.json();
    console.log(data2);

    let countries = Array.from(new Set(data.map((d) => {return d.country+" "+d.year;})));
    let divorces = Array.from(new Set(data.map((d) => {return d.divorce;})));

    let casas = [];
    let valor = [];
    
    for(var i = 9; i<18; i++){
        let obj = data2[i]["Nombre"];
        casas[i-9] = obj;
        valor[i-9] = data2[i]["Data"][0]["Valor"];

    }
    console.log("Casas "+casas);

    console.log("Valor "+valor);

    let casas_countries = casas.concat(countries);

     var salto = [];
    for(var i = 0; i<casas.length;i++){
        salto[i] = 0;
    }
    divorces = salto.concat(divorces);
    


    
   

    Highcharts.chart('container', {
    chart: {
        type: 'column'
    },
    title: {
        text: 'Número de divorcios por paises y número de personas que viven en casas de menos de 46m2 en toda España'
    },
    subtitle: {
        text: 'Para visualizar uno de los datos solo seleccione el campo a eliminar.'
    },
    xAxis: {
        categories: casas_countries,
        crosshair: true
    },
    yAxis: {
     //   tickInterval: 10,
        min: 0,
        title: {
            text: 'Nº de divorcios y número de personas que viven en casas de menos de 46m2 en toda España'
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
        name: 'Número de personas que viven en casas de menos de 46m2 ',
        data: valor
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
    <h2>Integración API Externa Número de hogares por comunidades y ciudades autónomas según tamaño de hogar y superficie útil de la vivienda.</h2>

    <figure class="highcharts-figure">
        <div id="container"></div>
        <p class="highcharts-description">
            Gráfico de columnas que compara el número de divorcios por paises y número de personas que viven en casas de menos de 46m2 en toda España.
            Estos datos no tienen ningún tipo de relación. Para visualizar los puntos elimine los datos de divorcios de la tabla. 
        </p>
        <p>En este caso he seleccionado los datos de las casas de menos de 46m2 en toda España para que la gráfica no fuera demasidado grande. </p>
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