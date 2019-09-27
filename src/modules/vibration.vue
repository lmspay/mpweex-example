<template>
    <div class="wrapper">
        <mpwx-btn style="margin-bottom: 20px;" label="Vibration" id="0" @onBtnClicked="onBtnClicked"></mpwx-btn>
    </div>
</template>

<script>
    import MpwxBtn from "../mpwx-btn"
    const vibration = weex.requireModule('vibration');
    module.exports = {
        components : {MpwxBtn},
        methods: {
            onBtnClicked(e) {
                vibration.vibrate();
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        flex: 1;
        padding: 40px;
    }
</style>