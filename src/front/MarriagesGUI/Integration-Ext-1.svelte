<script>
    import Button from "sveltestrap/src/Button.svelte";
    import  {pop} from "svelte-spa-router";	


    
    const URL_BASE = "api/v3/global-marriages";
       
    async function loadGraph(){
    

        //Mis datos
    const resData = await fetch(URL_BASE);
    let MyData = await resData.json();
    
    let countries = Array.from(new Set(MyData.map((d) => {return d.country+" "+d.year;})));
    let avg_ms = Array.from(new Set(MyData.map((d) => {return d.avg_m;})));
    let avg_wms = Array.from(new Set(MyData.map((d) => {return d.avg_wms;})));
    let marriages = Array.from(new Set(MyData.map((d) => {return d.marriages;})));
    console.log(MyData)
    
    //Integracion con la api externa
  
    const resData_4 = await fetch("https://restcountries.eu/rest/v2/?fields=name;area");
    let MyData_4 = await resData_4.json();
    let avg_4 = Array.from(new Set(MyData_4.map((d) => {return d.area;})));
    console.log("Datos areas de paises :");
    console.log(MyData_4);
    let areas=[]
    let max=marriages.length

    //Para que tengamos el mismo numero de datos y la grafica se pinte "correctamente"
    for (let index = 0; index < max; index++) {
        areas.push(avg_4[index])    
    }
    console.log(areas)

    
    Highcharts.chart('container', {
        chart: {
            type: 'bar'
        },
        title: {
            text: 'Relacion entre matrimonios  y area de los paises.'
        },
      
        xAxis: {
            categories: countries,
            title: {
                text: null
            }
        },
        yAxis: {
            min: 0,
            title: {
                text: 'Matrimonios/Area',
                align: 'high'
            },
            labels: {
                overflow: 'justify'
            }
        },
        tooltip: {
            valueSuffix: 'Personas'
        },
        plotOptions: {
            bar: {
                dataLabels: {
                    enabled: true
                }
            }
        },
        legend: {
            layout: 'vertical',
            align: 'right',
            verticalAlign: 'top',
            x: -40,
            y: 350,
            floating: true,
            borderWidth: 1,
            backgroundColor:
                Highcharts.defaultOptions.legend.backgroundColor || '#FFFFFF',
            shadow: true
        },
        credits: {
            enabled: false
        },
        series: [{
            name: 'Matrimonios',
            data: marriages
        }, {
            name: 'Area',
            data: areas
        }]
    });
    }


    
    </script>
    
    <svelte:head>
        <script src="https://code.highcharts.com/highcharts.js" defer></script>
        <script src="https://code.highcharts.com/modules/series-label.js"  defer></script>
        <script src="https://code.highcharts.com/modules/exporting.js"  defer></script>
        <script src="https://code.highcharts.com/modules/export-data.js"  defer></script>
        <script src="https://code.highcharts.com/modules/accessibility.js" on:load="{loadGraph}" defer></script>
    </svelte:head>
    
    <main>
        <h2>Integraciones con SOS1920</h2>
        <Button color="info" on:click="{pop}">Atrás</Button>
        <figure class="highcharts-figure">
            <div id="container"></div>
            <p class="highcharts-description">
                Se muestran los datos areas de paises de una API externa junto con los datos de matrimonios registrados.
            </p>
        </figure>

    


    </main>
    
    <style>
    .highcharts-figure, .highcharts-data-table table {
        min-width: 310px; 
        max-width: 1000px;
        margin: 1em auto;
    }
    
    #container {
        height: 1000px;
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