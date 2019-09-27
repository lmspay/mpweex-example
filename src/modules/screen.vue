<template>
    <scroller>
        <text class="split">屏幕亮度(0-1)</text>
        <div class="wrapper">
            <text style="margin-bottom: 20px; font-size: 32px;">当前亮度： {{value}}</text>
            <mpwx-btn class="btn" label="增加" id="0" @onBtnClicked="onBtnClicked"></mpwx-btn>
            <mpwx-btn class="btn" label="减少" id="1" @onBtnClicked="onBtnClicked"></mpwx-btn>
        </div>
        <text class="split">屏幕方向: {{orientation}}</text>
        <div class="wrapper">
            <mpwx-btn class="btn" label="横屏" id="2" @onBtnClicked="onBtnClicked"></mpwx-btn>
            <mpwx-btn class="btn" label="右横屏 (如果支持)" id="3" @onBtnClicked="onBtnClicked"></mpwx-btn>
            <mpwx-btn class="btn" label="左横屏 (如果支持)" id="4" @onBtnClicked="onBtnClicked"></mpwx-btn>
            <mpwx-btn class="btn" label="竖屏" id="5" @onBtnClicked="onBtnClicked"></mpwx-btn>
        </div>
    </scroller>
</template>

<script>
    import MpwxBtn from "../mpwx-btn"
    const screen = weex.requireModule('screen');
    export default {
        components : {MpwxBtn},
        data: {
            value: -1,
            orientation: "unknown"
        },
        beforeMount: function() {
            var self = this;
            screen.get(function (res) {
                self.value = parseFloat(res.brightness);
                self.value = Math.floor(self.value * 100) / 100;
            });
            screen.getOrientation(function (res) {
                self.orientation = res.orientation;
            });
        },
        methods: {
            onBtnClicked(e) {
                const { id } = e;
                var self = this;
                switch (id) {
                    case "0":
                        self.value += 0.1;
                        self.value = Math.floor(self.value * 100) / 100;
                        if(self.value > 1.001) {
                            self.value = 1.0;
                        }
                        screen.set(self.value, function (res) {
                            self.value = parseFloat(res.brightness);
                            self.value = Math.floor(self.value * 100) / 100;
                        });
                        break;
                    case "1":
                        self.value -= 0.1;
                        self.value = Math.floor(self.value * 100) / 100;
                        if(self.value < 0.001) {
                            self.value = 0;
                        }
                        screen.set(self.value, function (res) {
                            self.value = parseFloat(res.brightness);
                            self.value = Math.floor(self.value * 100) / 100;
                        });
                        break;
                    case "2":
                        screen.lockOrientation("landscape", function (res) {
                            self.orientation = res.orientation;
                        });
                        break;
                    case "3":
                        screen.lockOrientation("landscape-primary", function (res) {
                            self.orientation = res.orientation;
                        });
                        break;
                    case "4":
                        screen.lockOrientation("landscape-secondary", function (res) {
                            self.orientation = res.orientation;
                        });
                        break;
                    case "5":
                        screen.lockOrientation("portrait", function (res) {
                            self.orientation = res.orientation;
                        });
                        break;
                }
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        padding: 40px;
    }
    .btn {
        margin-bottom: 12px;
        margin-top: 12px;
    }
    .split {
        background-color: #eee;
        font-size: 26px;
        height: 60px;
        padding-left: 40px;
        line-height: 60px;
        color: #666;
    }
</style>