<template>
    <div class="wrapper">
        <mpwx-btn label="返回上一级" id="0" @onBtnClicked="onClicked"></mpwx-btn>
    </div>
</template>

<script>
    import MpwxBtn from "../mpwx-btn"
    var navigator = weex.requireModule('navigator');
    export default {
        components: {MpwxBtn},
        methods: {
            onClicked(event) {
                navigator.pop();
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