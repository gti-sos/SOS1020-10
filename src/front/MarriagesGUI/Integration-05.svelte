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
    
    
    // Datos del grupo 5
    const URL_BASE_grupo_05 = "/api/v1/books-exports";
    const resData_2 = await fetch(URL_BASE_grupo_05);
    console.log("fetch a " + URL_BASE_grupo_05);
    let MyData_2 = await resData_2.json();
    let avg_2 = Array.from(new Set(MyData_2.map((d) => {return d.exp_book;})));
    console.log("Datos libros exportados Diego:");
    console.log(avg_2);

    
    Highcharts.chart('container', {
        chart: {
            type: 'bar'
        },
        title: {
            text: 'Relacion libros exportados  y matrimonios registrados.'
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
                text: 'Matrimonios/Libros',
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
            name: 'Libros Exportados',
            data: avg_2
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
                Se muestran los datos de libros exportados del grupo 05 junto con los datos de matrimonios registrados.
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