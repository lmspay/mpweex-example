<template>
    <div class="wrapper">
        <text style="font-size: 32px;">当前电量： {{value}}</text>
        <text style="font-size: 32px;">是否充电： {{isPlugged}}</text>
    </div>
</template>

<script>
    import MpwxBtn from "../mpwx-btn"
    const battery = weex.requireModule('battery');
    export default {
        components : {MpwxBtn},
        data: {
            value: -1,
            isPlugged: false,
        },
        beforeMount: function() {
            var self = this;
            battery.status(function (res) {
                self.value = res.level;
                self.isPlugged = res.isPlugged;
            });
        }
    }
</script>

<style scoped>
    .wrapper {
        flex: 1;
        padding: 40px;
    }
</style>