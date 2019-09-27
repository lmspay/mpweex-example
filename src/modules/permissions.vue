<template>
    <div class="wrapper">
        <mpwx-btn class="btn" label="Check Permission" id="0" @onBtnClicked="doCheck"></mpwx-btn>
        <text class="txt">{{check}}</text>
        <mpwx-btn class="btn" label="Request Permission" id="1" @onBtnClicked="doRequest"></mpwx-btn>
        <text class="txt">{{request}}</text>
    </div>
</template>

<script>
    var permissions = weex.requireModule("permissions");
    import MpwxBtn from "../mpwx-btn"
    module.exports = {
        components : {MpwxBtn},
        data: {
            check: "",
            request: "",
        },
        methods: {
            doCheck: function (event) {
                var self = this;
                permissions.checkPermission("android.permission.ACCESS_NETWORK_STATE", function (e) {
                    self.check = e;
                });
            },
            doRequest: function (event) {
                var self = this;
                permissions.requestPermission("android.permission.ACCESS_FINE_LOCATION",
                    {
                        "title":"权限申请",
                        "message":"两码事小程序需要访问您的位置",
                        "okTitle": "确定",
                        "cancelTitle": "取消"
                    }, function (e) {
                    self.request = e;
                });
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
    .txt {
        font-size: 32px;
    }
</style>