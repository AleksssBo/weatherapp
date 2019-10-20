<template>
    <div class="app" :style="{'background': color}">
        <div class="loader" :class="{none: preload}">
            <div class="l_main">
                <div class="l_square"><span></span><span></span><span></span></div>
                <div class="l_square"><span></span><span></span><span></span></div>
                <div class="l_square"><span></span><span></span><span></span></div>
                <div class="l_square"><span></span><span></span><span></span></div>
            </div>
        </div>

        <div class="none-wrap" :class="{none: none}" :style="{'background': color}">
            <selectCity
                    :onSelect="onSelect"
                    :onCitySelected="onCitySelected"
                    :city="city"/>

            <temp :deg="deg"
                  :descr="description"
                  :icon="icon"/>

            <weatherInfo :press="press"
                         :humi="humi"
                         :rain="rain"
                         :speed="speed"/>
        </div>

    </div>
</template>

<script>

    import selectCity from "@/components/selectCity"
    import temp from "@/components/temp"
    import weatherInfo from "@/components/weatherInfo"
    import axios from "axios";

    export default {
        name: 'App',

        data() {
            return {

                fahr: 0,
                cel: 0,
                deg: 0,
                speed: 0,
                humi: 0,
                rain: 0,
                press: 0,
                cities: {},
                results: [],
                url: 'https://api.openweathermap.org/data/2.5/weather?q=',
                selectCityName: '',
                city: 'Армавир',
                description: '',
                API: '&appid=f3e7382ccfb772a9e3bc1a5a34243035',
                icon: '',
                color: '#498CEC',
                none: true,
                preload: false

            }
        },

        components: {
            selectCity,
            temp,
            weatherInfo
        },

        methods: {
            onSelect(data) {
                if (data.fahrActive) {
                    this.deg = this.fahr
                } else {
                    this.deg = this.cel
                }
            },

            onCitySelected(data) {

                let city = data.selectCityName.trim()
                this.none = data.none
                this.preload = data.preload

                let URL = this.url + city + ',RU&units=metric' + this.API + '&lang=ru'
                console.log(URL)

                axios.get(URL).then(response => {
                    this.city = city
                    this.results = response.data
                    this.cel = this.results.main.temp
                    this.speed = this.results.wind.speed
                    this.humi = this.results.main.humidity
                    this.rain = this.results.clouds.all
                    this.press = Math.round(this.results.main.pressure * 0.75006375541921)
                    this.icon = this.results.weather[0].icon


                    this.deg = this.cel
                    this.fahr = Math.round((9 / 5) * this.cel + 32)


                    this.description = this.results.weather[0].description

                    if (this.description == 'ясно') this.color = '#498CEC'
                    else this.color = '#7290B9'

                    URL = ''

                })

                setTimeout(() => {
                    this.none = false
                    this.preload = true
                }, 3000)
            }
        },

        // default data about weather
        mounted() {

            let URL = this.url + this.city + ',RU&units=metric' + this.API + '&lang=ru'
            console.log(URL)

            axios.get(URL).then(response => {
                this.results = response.data
                this.cel = this.results.main.temp
                this.speed = this.results.wind.speed
                this.humi = this.results.main.humidity
                this.rain = this.results.clouds.all
                this.press = Math.round(this.results.main.pressure * 0.75006375541921)
                this.icon = this.results.weather[0].icon


                this.deg = this.cel
                this.fahr = Math.round((9 / 5) * this.cel + 32)

                this.description = this.results.weather[0].description
                this.description = this.description[0].toUpperCase() + this.description.substring(1)

                if (this.description == 'Ясно') this.color = '#498CEC'
                else this.color = '#7290B9'

                URL = ''

                setTimeout(() => {
                    this.none = false
                    this.preload = true
                }, 2000)
            })
        },
    }
</script>

<style>

    html {
        height: 100vh;
    }

    .app {
        width: 100vw;
        height: 100vh;
        /*display: flex;*/
    }

    * {
        margin: 0;
        padding: 0;
        transition: .5s;
        outline: none;
        box-sizing: border-box;
    }

    .none-wrap {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        height: 100%;
    }

    .none {
        display: none;
    }

    body {
        height: 100vh;
        position: relative;
    }


    .loader{height:100vh;width:100vw}
    .loader .l_main{position:absolute;top:50%;left:50%;width:172px;height:128px;margin:0;-webkit-transform:translate(-50%,-50%);transform:translate(-50%,-50%)}
    @media (max-width:550px){.loader{-webkit-transform:scale(0.75);transform:scale(0.75)}}
    @media (max-width:440px){.loader{-webkit-transform:scale(0.5);transform:scale(0.5)}}
    .l_square{position:relative}
    .l_square:nth-child(1){margin-left:0px}
    .l_square:nth-child(2){margin-left:44px}
    .l_square:nth-child(3){margin-left:88px}
    .l_square:nth-child(4){margin-left:132px}
    .l_square span{position:absolute;top:0px;left:20px;height:36px;width:36px;border-radius:2px;background-color:#FFFFFF}
    .l_square span:nth-child(1){top:0px}
    .l_square span:nth-child(2){top:44px}
    .l_square span:nth-child(3){top:88px}
    .l_square:nth-child(1) span{-webkit-animation:animsquare1 2s infinite ease-in;animation:animsquare1 2s infinite ease-in}
    .l_square:nth-child(2) span{-webkit-animation:animsquare2 2s infinite ease-in;animation:animsquare2 2s infinite ease-in}
    .l_square:nth-child(3) span{-webkit-animation:animsquare3 2s infinite ease-in;animation:animsquare3 2s infinite ease-in}
    .l_square:nth-child(4) span{-webkit-animation:animsquare4 2s infinite ease-in;animation:animsquare4 2s infinite ease-in}
    .l_square span:nth-child(1){-webkit-animation-delay:0.00s;animation-delay:0.00s}
    .l_square span:nth-child(2){-webkit-animation-delay:0.15s;animation-delay:0.15s}
    .l_square span:nth-child(3){-webkit-animation-delay:0.30s;animation-delay:0.30s}
    @-webkit-keyframes animsquare1{0%,5%,95%,100%{-webkit-transform:translate(0px,0px) rotate(0deg);transform:translate(0px,0px) rotate(0deg)}30%,70%{-webkit-transform:translate(-40px,0px) rotate(-90deg);transform:translate(-40px,0px) rotate(-90deg)}}
    @keyframes animsquare1{0%,5%,95%,100%{-webkit-transform:translate(0px,0px) rotate(0deg);transform:translate(0px,0px) rotate(0deg)}30%,70%{-webkit-transform:translate(-40px,0px) rotate(-90deg);transform:translate(-40px,0px) rotate(-90deg)}}
    @-webkit-keyframes animsquare2{0%,10%,90%,100%{-webkit-transform:translate(0px,0px) rotate(0deg);transform:translate(0px,0px) rotate(0deg)}35%,65%{-webkit-transform:translate(-40px,0px) rotate(-90deg);transform:translate(-40px,0px) rotate(-90deg)}}
    @keyframes animsquare2{0%,10%,90%,100%{-webkit-transform:translate(0px,0px) rotate(0deg);transform:translate(0px,0px) rotate(0deg)}35%,65%{-webkit-transform:translate(-40px,0px) rotate(-90deg);transform:translate(-40px,0px) rotate(-90deg)}}
    @-webkit-keyframes animsquare3{0%,15%,85%,100%{-webkit-transform:translate(0px,0px) rotate(0deg);transform:translate(0px,0px) rotate(0deg)}40%,60%{-webkit-transform:translate(-40px,0px) rotate(-90deg);transform:translate(-40px,0px) rotate(-90deg)}}
    @keyframes animsquare3{0%,15%,85%,100%{-webkit-transform:translate(0px,0px) rotate(0deg);transform:translate(0px,0px) rotate(0deg)}40%,60%{-webkit-transform:translate(-40px,0px) rotate(-90deg);transform:translate(-40px,0px) rotate(-90deg)}}
    @-webkit-keyframes animsquare4{0%,20%,80%,100%{-webkit-transform:translate(0px,0px) rotate(0deg);transform:translate(0px,0px) rotate(0deg)}45%,55%{-webkit-transform:translate(-40px,0px) rotate(-90deg);transform:translate(-40px,0px) rotate(-90deg)}}
    @keyframes animsquare4{0%,20%,80%,100%{-webkit-transform:translate(0px,0px) rotate(0deg);transform:translate(0px,0px) rotate(0deg)}45%,55%{-webkit-transform:translate(-40px,0px) rotate(-90deg);transform:translate(-40px,0px) rotate(-90deg)}}



</style>
