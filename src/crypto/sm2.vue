<template>
    <scroller class="wrapper" show-scrollbar="false">
        <div style="height: 40px;"></div>
        <div class="title_root">
            <div class="tdot"></div>
            <text class="tlab">SM2 Plain</text>
        </div>
        <div class="pannel">
            <text class="content">{{plainBuf}}</text>
        </div>
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
        <div style="height: 40px;"></div>
    </scroller>
</template>

<script>
    const crypto = weex.requireModule("crypto");
    module.exports = {
        data: {
            plainBuf: '',
            hexBuf: 'SDK版本太低，不支持',
            base64Buf: 'SDK版本太低，不支持',
            urlSafeBase64Buf: 'SDK版本太低，不支持',
            resultTypes: ['hex', 'base64', 'urlSafeBase64']
        },
        created() {
            if(parseInt(WXEnvironment.weexVersionCode) < 2802) {
                // SDK版本太低
                this.plainBuf = 'SDK版本太低，不支持';
                return;
            }
            for(let idx in this.resultTypes) {
                this.runAlg(this.resultTypes[idx]);
            }
        },
        methods: {
            runAlg(resultType, outBuf) {
                crypto.sm2({
                    algorithm: 'SM2WithSM3/C1C2C3',
                    key: '020148E6AF89A0E132E4E7CDA26DF2C2AEB53B741FD00AE85C78CF6EBA13E939B1',
                    forEncryption: true,
                    data: '616263',
                    keyType: 'hex',
                    contentType: 'hex',
                    resultType: resultType
                }, (e) => {
                    if(resultType == 'hex') {
                        this.runDecrypt(e.data);
                    }
                    this[resultType + "Buf"] = e.data;
                });
            },
            runDecrypt(ciphers) {
                crypto.sm2({
                    algorithm: 'SM2WithSM3/C1C2C3',
                    key: '6B8B4567327B23C6643C98696633487374B0DC5119495CFF2AE8944A625558EC',
                    forEncryption: false,
                    data: ciphers,
                    keyType: 'hex',
                    contentType: 'hex',
                    resultType: 'hex'
                }, (e) => {
                    // 检查hex输出
                    if(e.data != '616263') {
                        this.plainBuf = '计算异常\n期望值:616263\n实际值:' + e.data;
                    }else {
                        this.plainBuf = e.data;
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