<template>
  <div id="app" :class="typeof weather.main !='undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
      <div class="search-box">
         <form class="search-bar" @submit.prevent="click" >
       
          <input type="text" class="search-input" placeholder="Search..."
          v-model= "query"/>
          <button class="search-button" type="submit"><img src="./assets/search-icon.png"></button>
          
         </form>     
        
      </div>
      <div class="weather-wrap" v-if=" typeof weather.main !='undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}} </div>
          <div class="date">{{dateBuilder()}}</div>
        </div>
        <div class="weather-box" >
          <div class="temp">{{Math.round(weather.main.temp)}}℃</div>
          <div class="weather">{{weather.weather[0].main}}</div>
      </div>
        
      </div>
      
      <div class="response">
        <div>{{weather.message}}</div>
        
      </div>
    </main>

  </div>
</template>

<script >
 

export default {
  
  name: 'App',
    data(){
      return{
        api_key:'d78fd1588e1b7c0c2813576ba183a667',
        url_base:"https://api.openweathermap.org/data/2.5/",
        query: '',
        weather: [],
        status:''
      }
    },
    methods: {
         
      click(){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
            .then(res=>{
              res.json().then(res => {
                // set res vào 1 state
             
                this.weather = res
                console.log(this.weather);
              })
            }).catch(err => {
              this.weather = err
              console.log(err);
            })
      },
     
      dateBuilder (){
        let d= new Date();
        let months = ["January", "February", "March", "April", "May", "June", "July", "August","September", "October", "November", "December"];
        let days = ["Sunday", "Monday", "Tueday", "Wednesday", "Thursday", "Friday", "Saturday"];

        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();

        return `${day} ${date} ${month} ${year}`;
      },

    }
}
</script>

<style src="./style.css">
 

</style>
