<template>
    <div class="wrapper">
        <text style="margin-bottom: 20px; font-size: 32px;">媒体音量，当前音量： {{value}}</text>
        <mpwx-btn class="btn" label="增加" id="0" @onBtnClicked="onBtnClicked"></mpwx-btn>
        <mpwx-btn class="btn" label="减少" id="1" @onBtnClicked="onBtnClicked"></mpwx-btn>
    </div>
</template>

<script>
    import MpwxBtn from "../mpwx-btn"
    const volume = weex.requireModule('volume');
    export default {
        components : {MpwxBtn},
        data: {
            value: -1
        },
        beforeMount: function() {
            var self = this;
            volume.get(function (res) {
                self.value = parseFloat(res.volume);
                self.value = Math.floor(self.value * 100) / 100;
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
                        volume.set(self.value, function (res) {
                            self.value = parseFloat(res.volume);
                            self.value = Math.floor(self.value * 100) / 100;
                        });
                        break;
                    case "1":
                        self.value -= 0.1;
                        self.value = Math.floor(self.value * 100) / 100;
                        if(self.value < 0.001) {
                            self.value = 0;
                        }
                        volume.set(self.value, function (res) {
                            self.value = parseFloat(res.volume);
                            self.value = Math.floor(self.value * 100) / 100;
                        });
                        break;
                }
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        flex: 1;
        padding: 40px;
    }
    .btn {
        margin-bottom: 12px;
        margin-top: 12px;
    }
</style>