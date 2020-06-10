<template>
    <scroller class="wrapper" show-scrollbar="false">
        <div style="height: 40px;"></div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">SM2 Hex</text>
        </div>
        <div class="pannel">
            <text class="content">{{hexBuf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">SM2 Base64</text>
        </div>
        <div class="pannel">
            <text class="content">{{base64Buf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">SM2 UrlSafeBase64</text>
        </div>
        <div class="pannel">
            <text class="content">{{urlSafeBase64Buf}}</text>
        </div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">SM2 Verify</text>
        </div>
        <div class="pannel">
            <text class="content">{{verifyBuf}}</text>
        </div>
        <div style="height: 40px;"></div>
    </scroller>
</template>

<script>
    const crypto = weex.requireModule("crypto");
    module.exports = {
        data: {
            verifyBuf: 'SDK版本太低，不支持',
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
                crypto.sm2SignOrVerify({
                    algorithm: 'SM3WithSM2',
                    key: '6B8B4567327B23C6643C98696633487374B0DC5119495CFF2AE8944A625558EC',
                    forSigning: true,
                    data: '616263',
                    keyType: 'hex',
                    contentType: 'hex',
                    resultType: resultType
                }, (e) => {
                    if(resultType == 'hex') {
                        this.runVerify(e.data);
                    }
                    this[resultType + "Buf"] = e.data;
                });
            },
            runVerify(ciphers) {
                crypto.sm2SignOrVerify({
                    algorithm: 'SM3WithSM2',
                    key: '020148E6AF89A0E132E4E7CDA26DF2C2AEB53B741FD00AE85C78CF6EBA13E939B1',
                    forSigning: false,
                    data: '616263',
                    signData: ciphers,
                    signDataType: 'hex',
                    keyType: 'hex',
                    contentType: 'hex',
                    resultType: 'hex'
                }, (e) => {
                    if(e.ok) {
                        this.verifyBuf = '验签成功';
                    }else {
                        this.verifyBuf = '验签失败';
                    }
                });
            }
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