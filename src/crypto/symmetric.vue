<template>
    <div class="wrapper">
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">AES Hex</text>
        </div>
        <div class="pannel">
            <text class="content">{{hexBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">AES Base64</text>
        </div>
        <div class="pannel">
            <text class="content">{{base64Buf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">AES UrlSafeBase64</text>
        </div>
        <div class="pannel">
            <text class="content">{{urlSafeBase64Buf}}</text>
        </div>
    </div>
</template>

<script>
    const crypto = weex.requireModule("crypto");
    module.exports = {
        data: {
            hexBuf: 'SDK版本太低，不支持',
            base64Buf: 'SDK版本太低，不支持',
            urlSafeBase64Buf: 'SDK版本太低，不支持',
            resultTypes: ['hex', 'base64', 'urlSafeBase64']
        },
        created() {
            if(parseInt(WXEnvironment.weexVersionCode) < 2802) {
                // SDK版本太低
                return;
            }
            for(let idx in this.resultTypes) {
                this.runAlg(this.resultTypes[idx]);
            }
        },
        methods: {
            runAlg(resultType, outBuf) {
                crypto.symmetric({
                    algorithm: 'AES/CBC/PKCS7Padding',
                    key: '6B8B4567327B23C6643C986966334873',
                    iv: '56097B7E240371A01290986E00C171E2',
                    forEncryption: true,
                    data: '616263',
                    keyType: 'hex',
                    ivType: 'hex',
                    contentType: 'hex',
                    resultType: resultType
                }, (e) => {
                    // 检查hex输出
                    if(resultType == 'hex' && e.data != '5247CA45F3AC4C15DAFF8D9A15AF97EF') {
                        this[resultType + "Buf"] = '计算异常\n期望值:5247CA45F3AC4C15DAFF8D9A15AF97EF\n实际值:' + e.data;
                    }else {
                        this[resultType + "Buf"] = e.data;
                    }
                });
            }
        }
    }
</script>

<style scoped>
    .wrapper {
        padding: 40px;
    }
    .title_root {
        flex-direction: row;
        align-items: center;
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
    }
    .content {
        font-size: 26px;
        color: #666;
    }
</style>