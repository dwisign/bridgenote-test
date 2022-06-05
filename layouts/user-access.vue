<template>
    <div class="user-access">
        <b-row>
            <b-col lg="5">
                <b-container class="bv-example-row bv-example-row-flex-cols">
                    <b-row class="user-access-row">
                        <b-col align-self="center" lg="8" offset-lg="2" class="pl-4 pr-4">
                            <div class="box">
                                <div class="text-center">
                                    <img src="/logo-color.svg" alt="" width="250" /><br><br>
                                </div>
                                <nuxt class="mt-3"/>
                            </div>
                        </b-col>
                    </b-row>
                </b-container>
            </b-col>
        </b-row>
    </div>
</template>

<style lang="scss" scoped>
    .user-access{
        background: url(/bg.png) center center no-repeat;
        background-size: cover;
        height: 100vh;
        .user-access-row{
            height: 100vh;
            .box{
                border-radius: 30px;
                padding: 30px 15px;
                background: rgb(255,255,255);
                background: linear-gradient(90deg, rgba(255,255,255,0.9) 100%, rgba(255,255,255,0.9) 100%);
            }
        }
    }
</style>
