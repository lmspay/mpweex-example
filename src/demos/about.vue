<template>
    <div class="wrapper">
        <div class="panel">
            <image class="icon" :src="icon"></image>
            <text class="title">{{title}}</text>
            <text class="desc">{{desc}}</text>
            <div class="sp" style="margin-top: 80px;"></div>
            <!--<div class="cell">-->
                <!--<text class="key">MPID</text>-->
                <!--<text class="value">{{mpid}}</text>-->
            <!--</div>-->
            <!--<div class="sp1"></div>-->
            <div class="cell">
                <text class="key">程序版本</text>
                <text class="value">{{version}}</text>
            </div>
            <div class="sp1"></div>
            <div class="cell">
                <text class="key">服务类目</text>
                <text class="value">{{category}}</text>
            </div>
            <div class="sp1"></div>
            <div class="cell">
                <text class="key">主体信息 </text>
                <text class="value">{{company}}</text>
            </div>
            <div class="sp"></div>
        </div>

        <text :class="['btn','btn'+easterEgg]" @click="enterMP">进入小程序</text>
    </div>
</template>

<script>
    const navigator = weex.requireModule('navigator');
    const modal = weex.requireModule('modal');
    module.exports = {
        data: {
            title: '',
            desc: '',
            icon: '',
            mpid: '',
            category: '',
            company: '',
            version: ''
        },
        computed: {
            easterEgg() {
                var eggShow = WXEnvironment.eggShow || "false";
                if(eggShow === "true") {
                    return "_egg";
                }
                return "_normal";
            }
        },
        created: function() {
            var self = this;
            navigator.getMpParams(function (params) {
                self.title = (params["mininame"] === undefined) ? '' : params["mininame"];
                self.desc = (params["mpdesc"] === undefined) ? '' : params["mpdesc"];
                self.icon = (params["logo"] === undefined) ? '' : 'mposs://' + params["logo"];
                self.mpid = (params["mpid"] === undefined) ? '' : params["mpid"];
                self.category = (params["category"] === undefined) ? '' : params["category"];
                self.company = (params["companyname"] === undefined) ? '' : params["companyname"];
                self.version = (params["version"] === undefined) ? '' : params["version"];
            });
        },
        methods: {
            enterMP: function () {
                navigator.pop();
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        align-items: center;
        background-color: #F2F2F2;
    }
    .panel {
        align-items: center;
        background-color: white;
    }

    .icon {
        margin-top: 80px;
        width: 160px;
        height: 160px;
        border-radius: 80px;
    }
    .title {
        margin-top: 40px;
        font-size: 48px;
        padding-left: 20px;
        padding-right: 20px;
    }
    .desc {
        margin-top: 20px;
        font-size: 32px;
        color: gray;
        padding-left: 20px;
        padding-right: 20px;
    }

    .sp {
        background-color: #e2e2e2;
        width: 750px;
        height: 1px;
    }

    .sp1 {
        background-color: #e2e2e2;
        width: 720px;
        height: 1px;
        align-self: flex-end;
    }

    .cell {
        flex-direction: row;
        align-items: flex-start;
        align-self: flex-start;
        padding: 30px;
    }

    .key {
        font-size: 32px;
        width: 190px;
    }

    .value {
        font-size: 32px;
        color: gray;
        width: 500px;
    }

    .btn {
        margin-top: 40px;
        font-size: 32px;
        height: 88px;
        width: 700px;
        border-radius: 20px;
        text-align: center;
        color: white;
        line-height: 88px;
    }
    .btn_normal {
        background-color: #1AB667;
    }
    .btn_egg {
        background-color: #df253f;
    }
    .btn_normal:active {
        background-color: #17A05A;
    }
    .btn_egg:active {
        background-color: #aa0624;
    }
</style>