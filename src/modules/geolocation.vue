<template>
    <div>
        <div class="group center">
            <div class="panel">
                <div style="flex-direction: row;">
                    <text class="text lab">定位次数：</text>
                    <text class="text">{{times}}</text>
                </div>
                <div style="flex-direction: row;">
                    <text class="text lab">坐标提供：</text>
                    <text class="text">{{provider}}</text>
                </div>
                <div style="flex-direction: row;">
                    <text class="text lab">方位角：</text>
                    <text class="text">{{bearing}}</text>
                </div>
                <div style="flex-direction: row;">
                    <text class="text lab">速度：</text>
                    <text class="text">{{speed}}</text>
                </div>
                <div style="flex-direction: row;">
                    <text class="text lab">精度：</text>
                    <text class="text">{{accuracy}}</text>
                </div>
                <div style="flex-direction: row;">
                    <text class="text lab">经度：</text>
                    <text class="text">{{lng}}</text>
                </div>
                <div style="flex-direction: row;">
                    <text class="text lab">纬度：</text>
                    <text class="text">{{lat}}</text>
                </div>
            </div>
        </div>
        <div class="group">
            <mpwx-btn class="btn" label='获取定位' id="0" @onBtnClicked="getLocation"></mpwx-btn>
            <mpwx-btn class="btn" label='监听定位' id="1" @onBtnClicked="watch"></mpwx-btn>
            <mpwx-btn class="btn" label='停止监听' id="2" @onBtnClicked="clearWatch"></mpwx-btn>
        </div>
    </div>
</template>

<script>
    const geo = weex.requireModule('geo');
    const modal = weex.requireModule('modal')
    import MpwxBtn from "../mpwx-btn"
    export default {
        components : {MpwxBtn},
        data () {
            return {
                keys: '[]',
                times: 0,
                lng: '---',
                lat: '---',
                provider: '---',
                speed: '---',
                accuracy: '---',
                bearing: '---'
            }
        },
        methods: {
            getLocation () {
                geo.get(event => {
                    if(event.result == 'ok') {
                        this.times++;
                        this.lng = event.longitude;
                        this.lat = event.latitude;
                        this.provider = event.provider;
                        this.speed = event.speed;
                        this.accuracy = event.accuracy;
                        this.bearing = event.bearing;
                    }
                });
            },
            watch() {
                geo.watch({
                    "maximumAge": 1000,
                    "model": "highAccuracy"
                }, event => {
                    if(event.result == 'ok') {
                        this.times++;
                        this.lng = event.longitude;
                        this.lat = event.latitude;
                        this.provider = event.provider;
                        this.speed = event.speed;
                        this.accuracy = event.accuracy;
                        this.bearing = event.bearing;
                    }
                });
            },
            clearWatch() {
                geo.clearWatch();
            }
        }
    }
</script>

<style scoped>
    .panel {
        flex-direction: column;
        justify-content: center;
        border-width: 2px;
        border-style: solid;
        border-color: rgb(162, 217, 192);
        background-color: rgba(162, 217, 192, 0.2);
        padding-top: 10px;
        padding-bottom: 10px;
    }
    .group {
        flex-direction: column;
        width: 650px;
        margin-left: 50px;
        margin-top: 50px;
    }
    .center {
        justify-content: center;
    }
    .text {
        font-size: 32px;
        text-align: center;
        padding-left: 25px;
        padding-right: 25px;
        color: #41B883;
    }
    .lab {
        width: 250px;
        text-align: right;
    }
    .btn {
        margin-bottom: 12px;
        margin-top: 12px;
    }
</style>