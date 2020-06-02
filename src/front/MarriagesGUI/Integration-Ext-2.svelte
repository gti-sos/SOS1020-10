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
  
    const resData_4 = await fetch("https://covid-193.p.rapidapi.com/statistics", {
            "method": "GET",
            "headers": {
                "x-rapidapi-host": "covid-193.p.rapidapi.com",
                "x-rapidapi-key": "3990991345msh0d2713751056f00p1756fbjsn62042961a8d5",
                "useQueryString": true
            }
        })
    let MyData_4 = await resData_4.json(); //Todos los datos de la respuesta

    let NewArray= MyData_4.response; // Nos quedamos con la informacion de los casos

    //Cogemos tantos elementos como tenemos en la grafica
    let covid=[]
    let max=marriages.length
    for (let index = 0; index < max; index++) {
        covid.push(NewArray[index])
        
    }
    console.log(covid)

    //Nos quedamos solamente con el dato de contagios totales por pais 
    let avg_4 = Array.from(new Set(covid.map((d) => {return d.cases.total})));

    console.log("Datos contagiados por paises :");
    console.log(avg_4)
  
    
    Highcharts.chart('container', {
        chart: {
            type: 'bar'
        },
        title: {
            text: 'Relacion entre matrimonios  y numero de contagiados por covid.'
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
                text: 'Matrimonios/Contagiados',
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
            name: 'Contagiados totales',
            data: avg_4
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
                Se muestran los datos de contagiados de covid  junto con los datos de matrimonios registrados.
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