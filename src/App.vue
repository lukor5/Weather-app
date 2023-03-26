<template>
    <link rel="stylesheet" 
        href="https://use.fontawesome.com/releases/v5.2.0/css/all.css" 
        integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ" 
        crossorigin="anonymous">
  <div class="main">
  <HeaderContainer/>
  <div class="weather">
    <button @click="callNextForecast('before')" class="btn"><i class="fas fa-arrow-left fa-lg"/></button>
  <SearchContainer  ref="SearchContainerRef"/>
  <button @click="callNextForecast('next')" class="btn"><i class="fas fa-arrow-right fa-lg"/></button>
  </div>
  <FooterContainer/>
</div>

</template>


<script>

import SearchContainer from './components/SearchContainer.vue';
import FooterContainer from './components/FooterContainer.vue';
import HeaderContainer from './components/HeaderContainer.vue';

export default {
  name: 'App',
  components: {
    HeaderContainer,
    SearchContainer,
    FooterContainer
  },
  methods: {
      callNextForecast(direction) {
          this.$refs.SearchContainerRef.nextForecast(direction);
        }
          
        }
      }


</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #acb5be;

}

.main {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background-image: url("~@/assets/background.jpg");
  min-height: 100vh;
}

.weather {
  display: flex;
  align-items: center;
  justify-content: center;
}


.weather button {
  border: 1px solid black;
  background-color: transparent;
  border-radius: 50px;
  margin-inline: 10px;
  padding: 10px;
}

.weather button:hover {
  color: white;
  border-color: white;
}

body {

  margin: 0px;


}
</style>
