<template>
    <scroller class="wrapper" show-scrollbar="false">
        <div style="height: 40px;"></div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">标准Base64编码</text>
        </div>
        <div class="pannel">
            <text class="content">{{base64EBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">标准Base64解码</text>
        </div>
        <div class="pannel">
            <text class="content">{{base64DBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Url Safe Base64编码</text>
        </div>
        <div class="pannel">
            <text class="content">{{urlSafeBase64EBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">Url Safe Base64解码</text>
        </div>
        <div class="pannel">
            <text class="content">{{urlSafeBase64DBuf}}</text>
        </div>
        <div style="height: 40px;"></div>
    </scroller>
</template>

<script>
    const crypto = weex.requireModule("crypto");
    module.exports = {
        data: {
            base64EBuf: 'SDK版本太低，不支持',
            base64DBuf: 'SDK版本太低，不支持',
            urlSafeBase64EBuf: 'SDK版本太低，不支持',
            urlSafeBase64DBuf: 'SDK版本太低，不支持'
        },
        created() {
            if(parseInt(WXEnvironment.weexVersionCode) < 2802) {
                // SDK版本太低
                return;
            }
            crypto.base64({
                data: 'FEF161626FFE11',
                forEncode: true,
                contentType: 'hex'
            }, (e) => {
                this.base64EBuf = e.data;
                crypto.base64({
                    data: this.base64EBuf,
                    forEncode: false,
                    contentType: 'base64',
                    resultType: 'hex'
                }, (ex) => {
                    this.base64DBuf = ex.data;
                });
            });

            crypto.base64({
                data: 'FEF161626FFE11',
                forEncode: true,
                contentType: 'hex',
                resultType: 'urlSafeBase64'
            }, (e) => {
                this.urlSafeBase64EBuf = e.data;
                crypto.base64({
                    data: this.urlSafeBase64EBuf,
                    forEncode: false,
                    contentType: 'urlSafeBase64',
                    resultType: 'hex'
                }, (ex) => {
                    this.urlSafeBase64DBuf = ex.data;
                });
            });
        },
        methods: {
            
        }
    }
</script>

<style scoped>
    .wrapper {
        background-color: white;
    }
    .title_root {
        flex-direction: row;
        align-items: center;
        padding-left: 40px;
        padding-right: 40px;
    }
    .tdot {
        width: 20px;
        height: 20px;
        background-color: #0088fb;
        border-radius: 10px;
    }
    .tlab {
        font-size: 32px;
        font-weight: bold;
        margin-left: 20px;
    }
    .pannel {
        flex-direction: column;
        margin-top: 20px;
        margin-bottom: 20px;
        background-color: #F2F2F2;
        border-radius: 10px;
        padding: 40px;
        margin-left: 40px;
        margin-right: 40px;
    }
    .content {
        font-size: 26px;
        color: #666;
    }
</style>