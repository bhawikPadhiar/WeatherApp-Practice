<template>
 <v-container>
  <h1 class="display-1 text-xs">Weather APP{{ weatherAppId }}</h1>
  <v-flex>
    <v-card>
        <v-card-text class="grey">
          <v-flex>
            <h4>Temperature
            </h4>
            <h1>{{ weather1.name }}</h1>
          </v-flex>
        </v-card-text>
        
      </v-card>
  </v-flex>
  <v-form >
    <v-flex xs12>
      <v-text-field v-model="city" white label="Enter City Name" solo></v-text-field>
    </v-flex>
    <v-flex xs12>
      <v-text-field v-model="statecode" white label="Enter state name" solo></v-text-field>
    </v-flex>
    <v-flex xs12>
      <v-text-field v-model="countrycode" white label="Enter Country Name" solo></v-text-field>
    </v-flex>
    <v-btn type="button" @click="cityName">submit</v-btn>
  </v-form>

<div>
  {{ weather1 }}
  {{ weather2 }}
</div>
  <!-- <div v-for="longs in lon" :key="lon"> -->
    <!-- <li>{{ longs.lat }}</li> -->
<!-- <input type="hidden" v-model="longs.lat"> -->
  <!-- </div> -->
 </v-container>
</template>

<script>  
export default {
  data(){
return{
 
  city:'',
  statecode:'',
  countrycode:'',
  weather1:'',
  lat:'',
  lons:'',
  lonss:'',
  lats:'',
  weather2:'',
  weatherAppId:process.env.weatherAppId
}
  },

  mounted(){
  //   this.$axios.$get(`https://api.openweathermap.org/data/2.5/weather?lat=${this.lat}.34&lon=${this.lons}.99&appid=7d204b6be5a940240ce6b858e7b5e54c`)
  //    .then(res=> console.log(res))
  
},

  created(){

    console.log(process.env.weatherAppId)
    
  },

  methods:{
    async cityName(){
    await this.$axios.$get(`http://api.openweathermap.org/geo/1.0/direct?q=${this.city},${this.statecode},${this.countrycode}
    &limit=5&appid=${this.weatherAppId}`)
    .then( res =>  {
          // console.log(res)
          let array = res;
          array.forEach(element => {
            this.lat=element.lat;
             this.lons=element.lon;
             this.lats=element.lat;
             this.lonss=element.lon;
          });
    //       this.$axios.$get(`https://api.openweathermap.org/data/2.5/weather?lat=${this.lat}.34&lon=${this.lons}&appid=7d204b6be5a940240ce6b858e7b5e54c`)
    //  .then(res=> console.log(res,'weatherdetail'))
     this.$axios.$get(`https://api.openweathermap.org/data/2.5/weather?lat=${this.lat}&lon=${this.lons}&appid=${process.env.weatherAppId}`)
     .then(res=> this.weather1=res),
     this.$axios.$get(`https://api.openweathermap.org/data/2.5/weather?lat=${this.lats}&lon=${this.lonss}&appid=${process.env.weatherAppId}`)
     .then(res=> this.weather2=res)
    
    });
        //   this.$axios.$get(`https://api.openweathermap.org/data/2.5/weather?lat=${this.lat}.34&lon=${this.lons}.99&appid=7d204b6be5a940240ce6b858e7b5e54c`)
        // .then(res=> console.log(res))
    
      }
    //   async weatherReport(){
    //     this.$axios.$get(`https://api.openweathermap.org/data/2.5/weather?lat=${this.lat}.34&lon=${this.lons}.99&appid=7d204b6be5a940240ce6b858e7b5e54c`)
    //  .then(res=> console.log(res))
    //   }

  },

}
</script>
