<template>
  <q-page class="flex column">
    <div class = "col q-pt-lg q-px-md">
   <q-input 
     v-model="search"
    placeholder="Search"
    dark
    borderless
    >
    <!-- <q-input bottom-slots v-model="text" label="Label" counter maxlength="12" :dense="dense"> -->
        <template v-slot:before>
          <q-icon @click= "getLocation"
          name ="my_location" />
        </template>

        <template v-slot:hint>
          Field hint
        </template>

        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
   </div>  
   <template v-if= "weatherData">
       <div class="col text-white text-center">
   <div class="text-h4 text-weight-light">
   Manchester
   </div>
   <div class="text-h6 text-weight-light">
   Rain
   </div>
   <div class="text-h1 text-weight-thin
   q-my-lg relative-position">
      <span>8</span>
      <span class ="text-h4 relative-position degree">
      &deg;</span>
      
   </div>
   </div>
   <div class = "col text-center">
    <img src ="https://www.fillmurray.com/100/100" alt="Bill">
   </div>
   </template>
   <template v-else>
<div class="class col text-center text-white">
  <div class="col text-h2 text-weight-thin">
    Quasar<br>Weather
  </div>
   <q-btn 
   class="col" 
    flat
    @click= "getLocation" >
      <q-icon left size="3em" name="my_location" />
      <div>Find My my location</div>
    </q-btn>
</div>

</template>
   <div class="col skyline"></div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
   data(){
    return {
      search: '',
      weatherData: null,
       lat:null,
       lon:null,
       apiUrl: 'http://api.openweathermap.org/data/2.5/weather',
       apiKey: '5a1a4539d1d6d6d1e291b1a6141c242b'
    }
},
methods: {
  getLocation(){
    //console.log('getLocation')
    navigator.geolocation.getCurrentPosition(position => {
      console.log('position: ',position)
      this.lat = position.coords.latitude
      this.lon = position.coords.longtitude
       this.getWeatherByCoords()
    })
  },
  getWeatherByCoords() {
    this.$axios(`${ this.apiUrl } ?lat=${ this.lat}&lon=${ this.lon}&appid=${ this.apiKey }& units=metrics`).then(response => {
      console.log('response: ',response)
    })
  }

}
}
</script>
<style lang= "sass">
.q-page
  background: linear-gradient(to bottom, #136a8a, #267871),
  .degree
    top: -44px
  .skyline
    flex: 0 0 100px
    background: url(../statics/skyline.png)
    background-size: contain
    background-position: center bottom
</style>