<template>
  <div id="app" :class="typeof weather.main != 'undefined' && 
  weather.main.temp > 16 ? 'warm' : ''">
    <main>
       <footer> 
 <p> DESENVOLVIDO E TODOS OS DIREITOS RESERVADOS A JEFFERSON DOUGLAS CURSO DESENVOLVIMENTO DE SISTEMAS SENAI BETIM </p> 
 </footer> 
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Digite o Nome de qualque cidade/pais/estado..."
          v-model="query"
          @keyup.enter="fetchWeather()" 
        /> <!-- com o keyup removemos o if que tínhamos abaixo nessa função -->
        
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}} </div>
          <div class="date">{{dateBuilder()}}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}°c</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
    <footer> 
 <p> DESENVOLVIDO E TODOS OS DIREITOS RESERVADOS A JEFFERSON DOUGLAS CURSO DESENVOLVIMENTO DE SISTEMAS SENAI BETIM </p> 
 </footer> 
  </div>
</template>

<script>

  export default {
    name: 'App',
    data () {
      return {
        api_key: 'cc8dccd293db616aed0baaf55609c94c',
        url_base: 'https://api.openweathermap.org/data/2.5/', 
        weather: {}
      }
    },
    methods: {
      fetchWeather () {
        /* removemos o if graças ao Vuejs keyup */
        //if (e.key == "Enter") {
          fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
            .then(res => {
              return res.json()
            }).then(this.setResults)
        //}
      },
      setResults (results) {
        this.weather = results;
      },
      /* Função para obter a data */
      dateBuilder () {
        let d = new Date();
        let months = ["Janeiro", "Fevereiro", "Março", "Abril",
        "Maio", "Junmho", "Julho", "Agosto", "Setembro", "Outubro",
        "Novembro", "Dezembro"];
        let days = ["Domingo", "Segunda-feira", "Terça-feira", "Quarta-feira",
        "Quinta-feira", "Sexta-feira", "Sabado"];

        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();

        return `${day} ${date} ${month} ${year}`;
      }
    }
  }

</script>



<style>

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    font-family: 'montserrat', sans-serif ;
  }

  #app {
    background-image: url('./assets/cold-bg.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }

  #app.warm {
    background-image: url('./assets/warm-bg.jpg');
  }

  main {
    min-height: 100vh;
    padding: 25px;

    background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
  }

  .search-box{
    width: 100%;
    margin-bottom: 30px;
  }

  .search-box .search-bar {
    display: block;
    width: 100%;
    padding: 15px;

    color: black;
    font-size: 20px;

    appearance: none;
    border: none;
    outline: none;
    background: none;

    box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
  }

  .search-box .search-bar:focus {
    box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.75);
    border-radius: 16px 0px 16px 0px;
  }

  .location-box .location {
    color:azure;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
    text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  }

  .location-box .date{
    color:azure;
    font-size: 20px;
    font-weight: 300;
    font-style: italic;
    text-align: center;
  }

  .weather-box {
    text-align: center;
  }

  .weather-box .temp {
    display: inline-block;
    padding: 10px 25px;
    color: azure;
    font-size: 102px;
    font-weight: 900;
    
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.25);
    border-radius: 16px;
    margin: 30px 0px;

    box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }

  .weather-box .weather {
    color:azure;
    font-size: 48px;
    font-weight:700;
    font-style: italic;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  }

</style>


