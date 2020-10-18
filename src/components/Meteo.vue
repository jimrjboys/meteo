<template>
<div class="container">
    <h1 class="my-4">App meteo avec vue.js</h1>
    <div class="form-group mb-5">
        <label for="position">
            Entrer le nom de votre ville
        </label>
        <input id="position" type="text" class="form-control" v-model="requete" @keypress.enter="geMeteo">
    </div>
    <div class="w-75 m-auto" v-if="temps">
        <h3 class="text-center">Position : {{ temps.name }} </h3>
        <div class="card text-center p-5">
            <p class="text-afficage">
                Temperature : {{temps.main.temp.toFixed() }}
            </p>
            <p class="text-afficage">
                Temp : {{ temps.weather[0].description }}
            </p>
        </div>
    </div>
</div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Meteo',
    data() {
        return {
            requete: '',
            temps: undefined,
            api_code: 'e5eeea518b679ae55befc8cbb010b1fa',
            url_recherche: 'https://api.openweathermap.org/data/2.5/weather?'
        }
    },
    methods: {
        geMeteo() {
            axios
                .get(`${this.url_recherche}q=${this.requete}&units=metric&APPID=${this.api_code}&lang=fr`)
                .then(reponse => {
                    // console.log(reponse)
                    this.temps = reponse.data;
                    console.log(this.temps);
                })
            this.requete = ''
        }
    },
}
</script>

<style>
.text-afficage {
    font-size: 30px;
    font-weight: 300;
    line-height: 1.2;
}
</style>
