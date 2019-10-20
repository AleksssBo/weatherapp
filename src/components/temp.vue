<template>

    <div class="main">

        <div class="temp">

            <img v-if="icon=='01n'||icon=='01d'" src="@/assets/img/sun.png" alt="">
            <img v-else-if="icon=='02n'||icon=='02d'||icon=='50n'||icon=='50d'" src="@/assets/img/partly_cloudy.png" alt="">
            <img v-else-if="icon=='03n'||icon=='03d'||icon=='04n'||icon=='04d'" src="@/assets/img/cloud.png" alt="">
            <img v-else-if="icon=='09n'||icon=='09d'||icon=='10n'||icon=='10d'||icon=='13d'" src="@/assets/img/rain.png" alt="">
            <img v-else-if="icon=='11n'" src="@/assets/img/storm.png" alt="">
            <div class="deg-temp">{{ Math.round(deg) }}°</div>

        </div>

        <h2 class="description"> {{ descr }} </h2>

    </div>

</template>

<script>
    export default {
        name: "temp",
        props: ['deg', 'descr', 'icon', 'none'],

        data() {
            return {}
        }
    }
</script>

<style scoped>
    .temp {
        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 17.9vh;
        line-height: 21vh;
        text-align: center;

        color: #FFFFFF;


        display: flex;
        justify-content: center;
        align-items: center;

    }

    .description {
        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 1.83vw;
        line-height: 2.2vw;
        text-align: center;
        margin-bottom: 23.43vh;

        color: #FFFFFF;
    }

    .main {
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        flex-direction: column;
    }

    @media only screen and (min-width: 320px) and (max-width: 736px) {
        .temp {
            font-size: 100px;
            font-family: Lato;
            font-weight: 300;
            line-height: 100px;
        }

        img {
            width: 130px;
            height: 130px;
        }

        .description {
            font-size: 4.8vw;
            margin-top: 20px;
            font-family: "Open Sans";
        }

        .deg-temp {
            /*margin-left: -10px;*/
        }
    }

</style>
