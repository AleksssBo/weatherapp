<template>
    <div class="info">
        <div class="info-block">
            <h4>Ветер:</h4>
            <p>{{speed}} м/с,западный</p>
        </div>

        <div class="info-block">
            <h4>Давление:</h4>
            <p>{{press}} мм.рт.ст</p>
        </div>

        <div class="info-block">
            <h4>Влажность:</h4>
            <p>{{humi}}%</p>
        </div>

        <div class="info-block">
            <h4>Вероятность дождя:</h4>
            <p>{{rain}}%</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: "weatherInfo",
        props: ['speed', 'humi', 'press', 'rain', 'none']
    }
</script>

<style scoped>
    .info {
        display: flex;
        margin-bottom: 12vh;
        width: 100%;
        flex-wrap: wrap;
        padding-left: 101px;
    }


    .info-block {
        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 1.3vw;
        line-height: 22px;
        flex-basis: 25%;
        color: rgba(255, 255, 255, 0.6);
        mix-blend-mode: normal;
    }

    p {
        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 1.8vw;
        line-height: 30px;
        margin-top: 10px;

        color: #FFFFFF;
    }

    @media only screen and (min-width: 320px) and (max-width: 736px) {
        .info-block {
            flex-basis: 50%;
            font-size: 4vw;
            margin-bottom: 5.2vh;
            line-height: 20px;
        }

        .info-block:nth-child(2n+1) {
            padding-left: 22px;

        }

        .info {
            padding-left: 0px;
            align-items: center;
            margin-bottom: 0.9vh;
            justify-content: space-between;
            width: 100%;
        }

        p {
            font-size: 4.8vw;
            line-height: 18px;
            margin-top: 2px;
        }
    }
</style>
