<template>
    <div class="wrapper">
        <div class="panel"><text class="text">网络类型: {{type}}</text></div>
    </div>
</template>

<script>
    const network = weex.requireModule("network");
    module.exports = {
        data: {
            type: "---"
        },
        beforeMount: function() {
            var self = this;
            network.status(function (res) {
                self.type = res.type;
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