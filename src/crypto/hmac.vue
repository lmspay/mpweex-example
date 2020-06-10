<template>
    <div class="wrapper">
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">HmacMD5 Hex</text>
        </div>
        <div class="pannel">
            <text class="content">{{hexBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">HmacMD5 Base64</text>
        </div>
        <div class="pannel">
            <text class="content">{{base64Buf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">HmacMD5 UrlSafeBase64</text>
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
                crypto.hmac({
                    algorithm: 'HmacMD5',
                    key: '313233343536',
                    data: '313233343536',
                    keyType: 'hex',
                    contentType: 'hex',
                    resultType: resultType
                }, (e) => {
                    // 检查hex输出
                    if(resultType == 'hex' && e.data != '30CE71A73BDD908C3955A90E8F7429EF') {
                        this[resultType + "Buf"] = '计算异常\n期望值:30CE71A73BDD908C3955A90E8F7429EF\n实际值:' + e.data;
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