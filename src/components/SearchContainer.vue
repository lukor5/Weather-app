<template>
    <div class="main-wrapper">
        <div class="search-wrapper">
            <input type="text" v-model="searchInput" placeholder="Search...">
            <button @click="search()">Search</button>
        </div>
        <div class="weather-wrapper">
            <div class="hourly-weather">
                <h4 style="text-align: left;">{{ searchResult && searchResult.list[count].dt_txt }}</h4>
                <h2 style="display: flex; align-items: center;"><img id="icon" style="align-self: flex-start"
                        src="">{{ searchResult && searchResult.city.name }}</h2>
                <h3>{{ searchResult && searchResult.list[count].main.temp }} °C</h3>
                <div class="weather-details">
                    <div id="wind">
                        <h3>wind</h3>
                        <h4>{{ searchResult && searchResult.list[count].wind.speed }} km/h</h4>
                    </div>
                    <div id="pressure">
                        <h3>pressure</h3>
                        <h4>{{ searchResult && searchResult.list[count].main.pressure }} Pa</h4>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'SearchContainer',
    data() {
        return {
            searchInput: '',
            apiUrl: 'https://api.openweathermap.org/data/2.5/forecast',
            iconUrl: 'https://openweathermap.org/img/wn/',
            searchParam: 'q',
            apiKey: 'd6cfdfada691e9bb8e47627e9fcdf079',
            searchResult: null,
            count: null,
            iconId: '',
        }
    },
    methods: {
        async search() {
            try {

                const response = await axios.get(`${this.apiUrl}?${this.searchParam}=${this.searchInput}&appid=${this.apiKey}&units=metric&limit=5`,);
                this.searchResult = response.data
                console.log(response.data)
                this.count = 0;
                this.getIcon();
            } catch (error) {
                console.error(error);
            }

        },

        async nextForecast(direction){
            if (this.count != null){

            if (direction=="next" && this.count < this.searchResult.list.length - 1){
          this.count++;  
          this.getIcon();
            }
            else if (direction=="before" && this.count > 0){
                this.count--;
                this.getIcon();
            }
        }
        },
        async getIcon(){
            this.iconId = this.searchResult.list[this.count].weather[0].icon
            document.getElementById('icon').src = `${this.iconUrl}${this.iconId}@2x.png`
            console.log(this.iconId)
        }
    }
}

</script>
<style lang ="scss" scoped>
.search {}

.main-wrapper {
    display: flex;
    flex-direction: column;
    align-self: center;
    max-width: 70%;
    background-color: rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    padding: 10px;
}




.search-wrapper input {
    background-color: transparent;
    color: white;
    border-style: none;
    margin: 10px;
    padding: 10px;
    border-bottom: 1px solid white;
    max-width: 70%;
}

button {
    padding: 10px;
    margin-left: 10px;
    border-style: none;
    color: white;
    background-color: rgba(0, 0, 0, 0.6);
}

.weather-wrapper {}

.hourly-weather {
    text-align: center;
}

.weather-details {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    column-gap: 10px;
    flex-wrap: wrap;
    background-color: rgba(0, 0, 0, 0.3);
    border-radius: 20px;

}

button:hover {
    background-color: rgba(0, 0, 0, 0.3);

}
</style>