<template>
    <scroller  show-scrollbar="false">
        <div class="group center">
            <div class="panel">
                <text class="text">{{value}}</text>
            </div>
        </div>
        <div class="group">
            <mpwx-btn class="btn" label='扫描二维码' id="0" @onBtnClicked="scan"></mpwx-btn>
        </div>
    </scroller>
</template>

<script>
    const scan = weex.requireModule('scan');
    var modal = weex.requireModule('modal');

    import MpwxBtn from "../mpwx-btn"
    export default {
        components : {MpwxBtn},
        data() {
            return {
                value: '---'
            }
        },
        methods: {
            scan () {
                var self = this;
                scan.scan({
                    base64: false
                }, function (e) {
                    if (e.result === 'success') {
                        self.value = e.data;
                    }
                });
            }
        }
    }
</script>

<style scoped>
    .panel {
        min-height: 100px;
        flex-direction: column;
        justify-content: center;
        border-width: 2px;
        border-style: solid;
        border-color: rgb(162, 217, 192);
        background-color: rgba(162, 217, 192, 0.2);
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
        font-size: 50px;
        text-align: center;
        padding-left: 25px;
        padding-right: 25px;
        color: #41B883;
    }
    .image {
        min-width: 200px;
        min-height: 200px;
        margin-top: 50px;
        align-self: center;
        width: 200px;
        height: 200px;
    }
    .btn {
        margin-bottom: 12px;
        margin-top: 12px;
    }
</style>