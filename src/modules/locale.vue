<template>
    <div class="wrapper">
        <div class="panel"><text class="text">{{language}}-{{region}}</text></div>
    </div>
</template>

<script>
    const locale = weex.requireModule("locale");
    module.exports = {
        data: {
            language: "-",
            region: "-",
        },
        beforeMount: function() {
            var self = this;
            locale.getLanguage(function (res) {
                self.language = res.language;
                self.region = res.region;
            });
        },
        methods: {}
    }
</script>

<style scoped>
    .wrapper {
        align-items: center;
        padding: 40px;
    }
    .panel {
        width: 650px;
        height: 100px;
        flex-direction: column;
        justify-content: center;
        border-width: 2px;
        border-style: solid;
        border-color: rgb(162, 217, 192);
        background-color: rgba(162, 217, 192, 0.2);
    }
    .text {
        font-size: 50px;
        text-align: center;
        padding-left: 25px;
        padding-right: 25px;
        color: #41B883;
    }
</style>