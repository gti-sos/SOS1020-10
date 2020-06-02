<script>

    import Button from "sveltestrap/src/Button.svelte";
    import  {pop} from "svelte-spa-router";
    import ListGroup from "sveltestrap/src/ListGroup.svelte";
    import ListGroupItem  from "sveltestrap/src/ListGroupItem.svelte";
    
    const URL_BASE = "api/v2/global-suicides";
           
    async function loadGraph(){
    
    const resData = await fetch(URL_BASE);
    let MyData = await resData.json();
    
    let countries = Array.from(MyData.map((d) => {return d.country;}));
    console.log("countries:");
    console.log(countries);

    let length_coords = Array.from(MyData.map((d) => {return parseFloat(d.lengthCoord);}));
    console.log("length coords:");
    console.log(length_coords);
  
    const URL_BASE_EXT = "/users";
    console.log("fetch a " + URL_BASE_EXT);
    
    const resData_Ext = await fetch(URL_BASE_EXT);
    console.log("resData_Ext:");
    console.log(resData_Ext);
    let MyData_Ext = await resData_Ext.json();
    console.log("Mydata ext.json():");
    console.log(MyData_Ext);

    let lng_coord = [];
    MyData_Ext.forEach(aux => lng_coord.push(parseFloat(aux.address.geo.lng)));
    console.log("Datos estraidos:");
    console.log(lng_coord);

    Highcharts.chart('container', {
        chart: {
            type: 'bar'
        },
        title: {
            text: 'Integración con Api Externa 2. (vía proxy)'
        },
        subtitle: {
            text: 'La relacion entre los datos no tiene lógica.'
        },
        xAxis: {
            categories: countries,
            title: {
                text: null
            }
        },
        yAxis: {
            min: -180,
            title: {
                text: 'Datos de coordenadas longitud de distintas APIs',
                align: 'high'
            },
            labels: {
                overflow: 'justify'
            }
        },
        tooltip: {
            valueSuffix: 'Coordenada Longitud'
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
            x: -250,
            y: 650,
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
            name: 'Coord.Longitud API_Int',
            data: length_coords
        },
         {
            name: 'Coord.Longitud API_Ext',
            data: lng_coord
        }]
    });
    }

    </script>
    
    <svelte:head>
        <script src="https://code.highcharts.com/highcharts.js"></script>
        <script src="https://code.highcharts.com/modules/series-label.js"></script>
        <script src="https://code.highcharts.com/modules/exporting.js"></script>
        <script src="https://code.highcharts.com/modules/export-data.js"></script>
        <script src="https://code.highcharts.com/modules/accessibility.js" on:load="{loadGraph}" defer></script>
    </svelte:head>
    
    <main>
        <h2>Integración con Api Externa 2</h2>
        <Button color="info" on:click="{pop}">Atrás</Button>
        <figure class="highcharts-figure">
            <div id="container"></div>
            <p class="highcharts-description">
                El gráfico muestra valores de la api interna y de una externa. No tienen relación.
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
    