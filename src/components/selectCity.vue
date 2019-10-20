<template>
    <div class="selectCity">


        <div class="location">
            <div class="wrap">
                <h2 class="city-name" v-bind:class="{active: active}">{{ city }}</h2>
                <div class="degrees mobile"
                     v-on:click="select"
                     v-bind:class="{activeLeft: celActive,
                                    activeRight: fahrActive,
                                    activeMobile: active}">

                    <div class="cel deg"
                         v-bind:class="{degActive: celActive}"
                         v-on:click="celActive = true; fahrActive = false">C
                    </div>

                    <div class="fahr deg"
                         v-bind:class="{degActive: fahrActive}"
                         v-on:click="fahrActive = true; celActive = false">F
                    </div>

                </div>
            </div>

            <div class="geo-wrap" v-bind:class="{active: active}">
                <div class="wrap">
                    <span class="change" v-on:click="activeSearch = true; active = false">Сменить город</span>
                    <span class="geo"><img src="@/assets/img/geo.png" alt="">Мое местоположение</span>
                </div>
            </div>
            <form @submit.prevent="" v-bind:class="{active: activeSearch}">
                <input type="text" class="search" v-model="selectCityName">
                <button v-on:click="selectCity">OK</button>
            </form>

        </div>


        <div class="degrees" v-on:click="select" v-bind:class="{activeLeft: celActive, activeRight: fahrActive}">
            <div class="cel deg"
                 v-bind:class="{degActive: celActive}"
                 v-on:click="celActive = true; fahrActive = false">C
            </div>
            <div class="fahr deg"
                 v-bind:class="{degActive: fahrActive}"
                 v-on:click="fahrActive = true; celActive = false">F
            </div>
        </div>


    </div>
</template>

<script>
    export default {
        name: "selectCity",
        props: ['onSelect', 'onCitySelected', 'city'],

        data() {
            return {
                celActive: true,
                fahrActive: false,
                activeSearch: false,
                active: true,
                selectCityName: '',
                none: false,
                preload: true

            }
        },

        methods: {
            select() {
                this.onSelect({
                    celActive: this.celActive,
                    fahrActive: this.fahrActive
                })
            },

            selectCity() {
                this.activeSearch = false;
                this.active = true
                this.none = true
                this.preload = false

                if (this.selectCityName != '') this.onCitySelected({
                    selectCityName: this.selectCityName[0].toUpperCase() + this.selectCityName.substring(1),
                    none: this.none,
                    preload: this.preload
                })
                this.selectCityName = ''

                this.none = false
                this.preload = true
            },


        }
    }
</script>

<style scoped>
    .none {
        display: none;
    }

    .selectCity {
        display: flex;
        /*justify-content: space-between;*/
        align-items: flex-start;
        width: 100vw;
        position: relative;
    }

    .location {
        width: 100%;
        padding-left: 99px;
    }

    .search {
        width: 100%;
        height: 100%;


        background: #FFFFFF;
        border-radius: 8px;
        border: none;


        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 30px;
        line-height: 36px;
        /* identical to box height */

        padding-left: 32px;
        padding-right: 105px;


        color: #000000;
    }

    .search:focus {
        outline: none;
        box-shadow: 0px 2px 8px rgba(0, 0, 0, 0.15);
    }

    .flexAct {
        display: flex;
    }

    form {
        position: relative;
        width: 579px;
        height: 86px;
        margin-top: 81px;
        margin-left: 0px;
        display: none;
    }

    button {
        position: absolute;
        /*right: -135px;*/
        top: 0;
        right: 0;
        background: transparent;
        border: none;

        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 27px;
        line-height: 36px;
        /* identical to box height */


        color: #1086FF;
        cursor: pointer;
        height: 100%;
        width: 105px;
    }

    .city-name {
        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 50px;
        line-height: 60px;
        color: #FFFFFF;
        margin-bottom: 9px;
        margin-top: 75px;
        display: none;
    }

    span {
        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 18px;
        line-height: 22px;


        color: #FFFFFF;

        mix-blend-mode: normal;
        opacity: 0.6;
    }

    .change {
        margin-right: 29px;
        margin-left: 2px;

        cursor: pointer;
    }

    .change:hover {
        opacity: 0.8;
    }

    .wrap {
        display: flex;
        width: 100%;
        justify-content: space-between;
        align-items: center;
    }

    .geo-wrap {
        display: none;
    }

    .geo-wrap .wrap {
        justify-content: flex-start;
    }

    .geo {
        display: flex;
        align-items: center;
    }

    .geo img {
        margin-right: 11.5px;
    }

    .degrees {
        display: flex;
        margin-top: 81px;
        margin-right: 75px;


        border: 1px solid rgba(255, 255, 255, 0.4);
        box-sizing: border-box;
        border-radius: 8px;

        position: relative;
    }

    .mobile {
        display: none;
    }

    .activeLeft::before {
        content: 'o';

        position: absolute;

        left: -17.5px;
        top: -4px;

        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 11px;
        line-height: 22px;
        /* identical to box height */


        color: #FFFFFF;

        mix-blend-mode: normal;
        opacity: 0.4;
    }

    .activeRight::after {
        content: 'o';

        position: absolute;

        right: -17.5px;
        top: -4px;

        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 11px;
        line-height: 22px;
        /* identical to box height */


        color: #FFFFFF;

        mix-blend-mode: normal;
        opacity: 0.4;
    }

    .deg {
        padding: 2px 13px;

        font-family: Lato;
        font-style: normal;
        font-weight: normal;
        font-size: 18px;
        line-height: 22px;
        color: #FFFFFF;
        opacity: 0.4;

        cursor: pointer;
    }

    .deg:first-child {
        border-bottom-left-radius: 8px;
        border-top-left-radius: 8px;
    }

    .deg:last-child {
        border-bottom-right-radius: 8px;
        border-top-right-radius: 8px;
    }

    .degActive {
        background: rgba(255, 255, 255, 0.2);
        opacity: 1 !important;
    }

    .active {
        display: block !important;
    }


    @media only screen and (min-width: 320px) and (max-width: 736px) {
        .location {
            padding-left: 19px;
            width: 100vh;
        }

        .degrees {
            margin-right: 23px;
            margin-top: 0px;
            display: none;
        }

        .mobile {
            display: none;
        }

        .activeMobile {
            display: flex;
        }

        .city-name {
            font-size: 30px;
            margin-top: 19px;
            line-height: 36px;
        }

        span {
            font-size: 15px;
        }

        form {
            width: 100vw;
            height: 53px;
            margin-left: 0;
            margin-top: 27px;
            margin-left: -19px;
            text-align: center;
        }

        button {
            right: 18px;
            font-size: 15px;
            line-height: 18px;
            color: #1086FF;
            width: 53px;
        }

        .search {
            width: 90%;
            /*padding: 0;*/
            padding-right: 54px;
            padding-left: 18px;

            font-size: 15px;
            line-height: 18px;
            margin: auto;
        }

    }
</style>
